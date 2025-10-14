+++
title = 'Terraform'
date = 2025-08-29T05:37:40Z
tags = ["terraform", "cloud"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A short tutorial on working of terraform"
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/content/posts/"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# Terraform 

Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp. It allows you to define and manage your infrastructure resources—such as virtual machines, networks, and databases—in human-readable configuration files. Instead of manually provisioning resources through a cloud provider's web console, you can use Terraform to automate the process, making it repeatable and less prone to error.


## Installing and verifying the installation
Terraform can be installed by visiting the hashicorp officail website, it is available for all major operating systems like windows, mac and linux. [Install | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/install).

To check the installation of terraform first restart the computer after installing, setting the bin as the environment variable and then type the following command

```bash
terraform -v // or terraform --version
```
## Basic commands
The basics of Terraform revolve around a few core concepts and commands that form the standard workflow. You'll use these to initialize a project, plan changes, and apply them.

- `terraform init`: This is the first command you run in a new Terraform directory. It initializes the working directory by downloading the necessary **providers** (plugins for interacting with cloud services) and modules defined in your configuration files. Think of it as preparing your project for action.
- `terraform plan`: This command creates an **execution plan**. It reads your configuration files, compares them to the current state of your infrastructure (using the state file), and shows you exactly what it will do if you proceed. It's a "dry run" that lets you review changes before they are applied, showing you what resources will be added, changed, or destroyed. 
- `terraform apply`: This command executes the plan created by `terraform plan`. It provisions or updates your infrastructure to match the desired state defined in your configuration files. After running `terraform apply`, Terraform creates or updates the **state file** to reflect the current state of your resources.
- `terraform destroy`: This command is used to clean up all the resources managed by your Terraform configuration. It's the inverse of `apply` and is useful for tearing down temporary environments or resources you no longer need. This command should be used with caution, as it permanently deletes resources.
- `terraform validate`: This command checks your configuration files for syntax errors and internal consistency. It does not check the state of your infrastructure or interact with any providers. It's a quick way to ensure your code is well-formed before you run a `plan` or `apply`.
- `terraform state list`: To see the current state

### The Workflow in a Nutshell

The typical Terraform workflow follows a simple, repeatable pattern:

1.  **Write:** Create your `.tf` configuration files.
2.  **Initialize:** Run `terraform init` to download providers.
3.  **Plan:** Run `terraform plan` to see what changes will be made.
4.  **Apply:** Run `terraform apply` to create or update your infrastructure.
5.  **Destroy:** When done, run `terraform destroy` to tear everything down.

## Terraform's extensive support
Terraform's core strength lies in its extensive ecosystem of "providers," which are plugins that allow it to interact with a vast array of platforms. Here's a brief rundown of some of the major cloud and technology providers it supports:

- Amazon Web Services (AWS): The most popular cloud provider and a cornerstone of Terraform's ecosystem. The AWS provider allows you to manage a wide range of services, including EC2 instances, S3 buckets, RDS databases, and more.
- Microsoft Azure: A major player in the cloud market, Azure has a robust Terraform provider for managing its resources like Virtual Machines, Azure Functions, and various networking components.
- Google Cloud Platform (GCP): Google's cloud service is fully supported, with a provider that lets you provision and manage Compute Engine, Cloud Storage, and Kubernetes Engine, among others.
- Other Cloud Providers: Terraform also supports many other public and private cloud providers, including **Oracle Cloud Infrastructure (OCI)**, **Alibaba Cloud**, **DigitalOcean**, and **VMware vSphere** for on-premises virtualization.
- SaaS and Other APIs: It's not just for clouds! Terraform can manage resources on a variety of other platforms like **Kubernetes**, **GitHub**, **Cloudflare**, and even tools like **Datadog** and **Splunk**.

## An example with GCE and terraform

```bash
# Define the required providers and their versions.
# This block tells Terraform that we need the Google Cloud provider.
terraform {
  required_providers {
    google = {
      source = "hashicorp/google"
      version = "4.51.0" # Use a compatible version
    }
  }
}

# Configure the Google Cloud provider.
# You need to replace "your-gcp-project-id" and "your-region" with your own values.
# The provider will use your locally configured gcloud CLI credentials to authenticate.
provider "google" {
  project = "your-gcp-project-id"
  region  = "us-central1"
}

# Define a Google Compute Engine (GCE) instance.
# This is a resource block that specifies the desired state of our VM.
resource "google_compute_instance" "default" {
  # The name of the GCE instance.
  name         = "terraform-instance-1"
  # The machine type (e.g., e2-medium, n1-standard-1).
  machine_type = "e2-medium"
  # The zone where the instance will be created.
  zone         = "us-central1-a"

  # Define the boot disk for the instance.
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }

  # Define the network interface. We'll use the default network.
  network_interface {
    network = "default"
    # An access config block adds an external IP address.
    access_config {
      # This block can be empty to assign a new ephemeral IP.
    }
  }
}

# Define an output variable to display the external IP address of the created instance.
# This is useful for getting information from your infrastructure after it's provisioned.
output "instance_ip_address" {
  description = "The external IP address of the created GCE instance."
  value       = google_compute_instance.default.network_interface[0].access_config[0].nat_ip
}
```

## Setting up terraform with AWS

### Configure AWS Credentials

First, you need to give Terraform permission to access your AWS account. The best way to do this is by creating an **IAM User** with programmatic access and the necessary permissions (e.g., `AdministratorAccess` for full control, or more restricted permissions for production environments).

1.  **Create an IAM User** in your AWS Console and get the **Access Key ID** and **Secret Access Key**.
2.  Open your terminal or command prompt and run the following command:
    ```bash
    aws configure
    ```
3.  Enter the credentials you just downloaded. This will store them in a secure file on your computer that Terraform can automatically use.
    ```
    AWS Access Key ID [None]: YOUR_ACCESS_KEY
    AWS Secret Access Key [None]: YOUR_SECRET_KEY
    Default region name [None]: us-east-1  # Or your preferred region
    Default output format [None]: json
    ```

### Create a Terraform Configuration File

Now, let's write some Terraform code.

1.  Create a new folder for your project.

2.  Inside that folder, create a new file named `main.tf`. This is where your configuration will live.

3.  Paste the following code into `main.tf`. This code tells Terraform to use the AWS provider and defines a simple S3 bucket resource.

    ```terraform
    # This block tells Terraform which providers we need.
    terraform {
      required_providers {
        aws = {
          source  = "hashicorp/aws"
          version = "~> 5.0"
        }
      }
    }

    # This configures the AWS provider, like setting the region.
    provider "aws" {
      region = "us-east-1"
    }

    # This is a "resource" block. It defines an AWS resource to create.
    # In this case, we are creating an S3 bucket.
    resource "aws_s3_bucket" "my_bucket" {
      # NOTE: S3 bucket names must be globally unique. Change this name!
      bucket = "my-unique-terraform-demo-bucket-20251014"

      tags = {
        Name        = "My Terraform Bucket"
        ManagedBy   = "Terraform"
      }
    }
    ```

    **Important**: Remember to change the `bucket` name to something unique.


### Initialize, Plan, and Apply

These are the three core commands you'll use with Terraform. Run them from your terminal inside the project folder you created.

1.  **Initialize the Directory**
    This command downloads the AWS provider plugin defined in your configuration.

    ```bash
    terraform init
    ```

    You should see a message saying "Terraform has been successfully initialized\!".

2.  **Create an Execution Plan**
    This command shows you what changes Terraform will make to your infrastructure without actually making them. It's a great way to review your work.

    ```bash
    terraform plan
    ```

    Terraform will output a plan showing it will create 1 new resource (the S3 bucket).

3.  **Apply the Changes**
    This command executes the plan and builds the resources in your AWS account.

    ```bash
    terraform apply
    ```

    Terraform will show you the plan again and ask for confirmation. Type **`yes`** and press Enter. After a few moments, your S3 bucket will be created.

To clean up and delete the resources you created, you can simply run `terraform destroy`.