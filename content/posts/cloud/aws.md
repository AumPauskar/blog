+++
title = 'AWS'
date = 2025-10-13T18:34:50Z
tags = ["cloud", "aws"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A handbook in navigating, using AWS ande explaining the fundamentals"
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

# AWS

## Basic setup and IAM configuration
Creating an AWS account gives you access to the entire suite of Amazon Web Services. The first user you create is the **AWS Account Root User**. This user has **unrestricted access** to all resources in the account, including billing, and should **NEVER** be used for day-to-day tasks.

Immediately after account creation, the absolute most critical security step is to set up a secondary, secure user for daily operations using **AWS Identity and Access Management (IAM)**.

**IAM** is the service that manages access to AWS resources. It allows you to create **Users**, assign them to **Groups**, define **Roles**, and control what actions they can perform using **Policies**. The core principle is **Least Privilege**: granting only the permissions required to perform a task.

### Creating the AWS Account

1.  Visit the AWS Website: Go to the AWS homepage and click **"Create an AWS Account."**
2.  Provide Details: Enter your email address (this will be the **Root User** email), a strong password, and an AWS account name.
    * Best Practice: Use a secure, non-personal email (like a dedicated IT or admin email alias for business use).
3.  Contact Information: Enter your contact details, choose your account type (Personal/Business), and accept the AWS Customer Agreement.
4.  Payment Information: You'll need to provide a credit/debit card for billing verification. You are only charged if you use services outside the **Free Tier** limits.
5.  Identity Verification: Verify your phone number via a call or SMS.
6.  Support Plan: Select a support plan (the **Basic Support** plan is free and recommended for beginners).
7.  Sign-in: Once activated (it can take a few minutes), **Sign in to the AWS Management Console as the Root User.**

#### 🛑 **Critical Root User Security Steps (Do This Immediately!)**

1.  Enable Multi-Factor Authentication (MFA): From the IAM Dashboard, enable MFA for your **Root User**. This adds a layer of security, requiring a code from a virtual or hardware device in addition to your password.
2.  Do Not Use Root: Log out of the Root User. You should only use this account for the absolute most sensitive tasks, like changing the account's support plan or closing the account. **All daily work must be done via an IAM user.**

***

### Phase 2: Configuring an IAM User (for daily administrative use)

You must be signed in as the **Root User** for this setup.

#### Step 1: Create an IAM Group

Groups make it easier to manage permissions. Instead of assigning a policy to every user, you assign it to the group.

1.  In the AWS Console search bar, type **"IAM"** and go to the service dashboard.
2.  In the navigation pane, choose **User Groups**, then **Create group**.
3.  Name the group (e.g., `Administrators`).
4.  **Attach a Policy:** For your first administrative user group, search for and select the **`AdministratorAccess`** policy. This grants full administrative permissions, similar to the Root User, but through an IAM entity that can be restricted with MFA.
5.  Click **Create group**.

#### Step 2: Create a New IAM User

1.  In the IAM dashboard, choose **Users**, then **Create user**.
2.  **Specify User Details:**
    * Set the **User name** (e.g., `yourname-admin`).
    * Select **AWS Management Console access**.
    * Choose a **Custom password** and select **"Require password reset"** (optional, but good practice).
    * **Do NOT create an Access Key** yet, as this user is for console access.
3.  **Set Permissions:**
    * Select **"Add user to group"**.
    * Select the `Administrators` group you created in Step 1.
4.  **Review and Create:** Review the settings and click **Create user**.

#### Step 3: Enable MFA for the New IAM User

1.  Once the user is created, click on their name to go to the details page.
2.  Select the **Security credentials** tab.
3.  Next to **Multi-factor authentication (MFA)**, click **Manage**.
4.  Choose **Authenticator app** (e.g., Google Authenticator, Microsoft authenticator) and follow the on-screen steps to scan the QR code and assign the MFA device.

#### Step 4: Sign In as the IAM User

1.  Log out of the Root User.
2.  Sign back in using the **IAM User's login URL**, username, and password. This is now your daily-use account.
3.  **Do not use the Root User again** unless absolutely necessary!

## Setting up a billng account and staying within the free tier


This is arguably the most important non-technical topic for any new AWS user. Falling out of the Free Tier can lead to unexpected charges. The strategy to stay under the Free Tier is a combination of **monitoring, alerting, and resource discipline.**

***

## Topic: Managing Billing and Staying Within the AWS Free Tier

The **AWS Free Tier** is a collection of offerings that allows new customers to use select AWS services free of charge up to certain usage limits. It is designed for learning and small-scale testing. It consists of three parts:

1.  12 Months Free: Free usage up to a maximum amount for new accounts for 12 months after sign-up (e.g., 750 hours of a t2.micro EC2 instance).
2.  Always Free: Services that remain free up to a certain limit indefinitely (e.g., 10 custom metrics in Amazon CloudWatch).
3.  Free Trials: Short-term free access for certain services.

### Configure Automated Free Tier Alerts

This is your safety net. You'll set up two types of alerts: a default AWS alert and a custom budget alert.

#### Enable Default Free Tier Usage Alerts (The 85% Warning)

1.  Sign in to the **AWS Management Console** using your **IAM user**.
2.  Search for and navigate to the **Billing Dashboard**.
3.  In the left navigation pane, select **Billing preferences**.
4.  Find the **Free Tier Usage Alerts** setting. Ensure the checkbox is selected for **"Receive AWS Free Tier alerts."**
5.  *Optional but Recommended:* Add a backup email address to ensure you don't miss any critical notifications.

#### Create an AWS Budget (The Hard Stop Warning)

A cost budget for $0.01 is the most effective way to catch any charge.

1.  From the **Billing Dashboard**, navigate to **AWS Budgets** in the left navigation pane.
2.  Click **Create budget**.
3.  Choose budget type: Select **Cost budget** (start with the **Simplified template** for ease).
4.  Set budget details:
    - Budget name: `your-free-tier-budget-name`
    - Period: **Monthly**
    - Budget amount: Set a small amount, like **$0.01**. (This is a proactive measure; any cost, even a cent, will trigger the alert).
    - Start Month: Set to the current month.
5.  Configure alerts:
    - Alert Threshold: Set the threshold to **100%** of the budgeted amount (which is $0.01).
    - Trigger: Select **Actual cost**.
    - Notification: Enter your email address to receive the alert.
6.  Review and Create

### Step 2: Implement Resource Management Discipline

Alerts help, but manual discipline prevents the usage in the first place.

| Best Practice | Service / Scenario | Action to Prevent Charges |
| :--- | :--- | :--- |
| **Check Instance Size** | **Amazon EC2** (Virtual Servers) | **ALWAYS** launch a **`t2.micro`** (or `t3.micro` in some regions) instance and ensure the **OS is Linux** (Windows might have a different limit/cost). **STOP or TERMINATE** the instance when not in use. |
| **Delete Immediately** | **AWS Lambda, Amazon S3, RDS** | Do not rely on "stopping" for most services. **Delete/Terminate** resources when you are done. An **EBS Volume** (disk) often incurs cost even if the EC2 instance is stopped. |
| **Check Storage Class** | **Amazon S3** (Object Storage) | Most Free Tier limits are for **S3 Standard Storage**. Using other classes (like Infrequent Access or Glacier) can incur charges. |
| **Delete/Stop Databases**| **Amazon RDS** (Managed Databases) | **STOP** your RDS instance if not needed. Note that stopped databases are still billed for storage, so **DELETE** completely if it's just for testing. |
| **Be Region Aware** | **All Services** | The Free Tier limits are per-account, but usage is tracked per-region. If you launch one EC2 in North Virginia and one in Oregon, the hours are combined, but you must look out for regional data transfer costs. **Always use the same region for a project.** |
| **Monitor Network Usage**| **Data Transfer** | **Data transfer OUT** of AWS regions is the most common surprise charge. Data transfer **IN** is generally free. Minimizing data leaving the AWS network is key. |

### Step 3: Regular Cost Monitoring

1.  Use the Free Tier Page:
    - In the **Billing Dashboard**, click on **Free Tier** in the left navigation menu.
    - This page provides a clear summary of your usage against the limits for each service (e.g., 100/750 hours of EC2 used).
    - **Check this page daily or weekly.**
2.  Use Cost Explorer:
    - In the **Billing Dashboard**, navigate to **Cost Explorer**.
    - This tool allows you to visualize your spending.
    - **Enable Cost Explorer** (it may take 24 hours to populate data).
    - Create a report filtered to **"Unblended Cost"** and review it to ensure your actual cost remains $0.00.