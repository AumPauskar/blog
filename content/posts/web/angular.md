+++
title = 'Angular basics'
date = 2025-07-22T11:54:45+07:00
tags = ["angular", "web", "javascript", "typescript", "frontend", "webdev", "programming", "html", "css", "node", "npm"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A short guide on angular"
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

# Angular basics

## What is angular and what workflows is it ideal at?
Angular is a platform and framework for building single-page client applications using HTML and TypeScript. Developed and maintained by Google. t is designed to make the development and testing of such applications easier by providing a framework for client-side MVC (Model-View-Controller) architecture.

Installing Angular from scratch involves setting up your development environment, which includes installing Node.js, the Angular CLI (Command Line Interface), and creating a new Angular project. Here’s a step-by-step guide to get you started:

### Step 1: Install Node.js

1. **Download Node.js**:
   - Go to the [Node.js official website](https://nodejs.org/).

2. **Install Node.js**:
   - Run the installer and follow the prompts. Make sure to check the box that says "Automatically install the necessary tools" if prompted.

3. **Verify Installation**:
   - Open a terminal (Command Prompt, PowerShell, or Terminal on macOS/Linux).
   - Run the following commands to check if Node.js and npm are installed correctly:
     ```bash
     node -v
     npm -v
     ```
   - Restart the machine if the following prompts are not working.

### Step 2: Install Angular CLI

The Angular CLI is a command-line tool that helps you create and manage Angular applications.

1. **Install Angular CLI Globally**:
   - In your terminal, run the following command:
     ```bash
     npm install -g @angular/cli
     ```
   - The `-g` flag installs the Angular CLI globally, making it accessible from any directory.

2. **Verify Angular CLI Installation**:
   - After installation, check the version of Angular CLI by running:
     ```bash
     ng version
     ```
   - This command should display the version of Angular CLI along with other Angular-related packages.

## Creating an Angular project

1. **Create a New Project**:
   - Navigate to the directory where you want to create your project. For example:
     ```bash
     cd path/to/your/projects
     ```
   - Run the following command to create a new Angular project (replace `my-angular-app` with your desired project name):
     ```bash
     ng new my-angular-app
     ```
     or you can use the following to open a new project on the same folder
     ```bash
     ng new my-angular-app --directory=.
     ```
   - You will be prompted to choose whether to add Angular routing and which stylesheet format to use (CSS, SCSS, SASS, LESS, etc.). Make your selections and press Enter. It is recommended to use **SCSS** for your first application

2. **Navigate to Your Project Directory**:
   - Change into your new project directory:
     ```bash
     cd my-angular-app
     ```

### Running the application

1. **Serve the Application**:
   - Run the following command to start the development server:
     ```bash
     ng serve
     ```
     If you want to serve and automatically open the same on the browser you can use the following
     ```bash
     ng serve --open
     ```
   - By default, the application will be served at `http://localhost:4200/`.


## Creating a basic application

### Creating components
Components are the building blocks of Angular applications. Each component encapsulates its own logic, template, and styles, making it reusable and maintainable.
- Creating a Component: To create a new component, you can use the Angular CLI. For example, to create a component named home:
```bash
ng generate component home
```

This command will create a new folder named home in the src/app directory, containing the following files:

- `home.component.ts`: The TypeScript file containing the component's logic.
- `home.component.html`: The HTML template for the component.
- `home.component.css`: The CSS styles for the component.
- `home.component.spec.ts`: The testing file for the component.

Here is a breakdown of `HomeComponents`
- Contents of `HomeComponent.ts`
   ```ts
   // home.component.ts
   import { Component } from '@angular/core';

   @Component({
   selector: 'app-home',
   templateUrl: './home.component.html',
   styleUrls: ['./home.component.css']
   })
   export class HomeComponent {
   title = 'Welcome to My Angular App!';
   }
   ```
- Contents of `home.component.html`
   ```html
   <!-- home.component.html -->
   <h1>{{ title }}</h1>
   <p>This is the home page of your Angular application.</p>
   ```

### Routing
Routing in Angular allows you to navigate between different views or components in your application without reloading the page. The Angular Router is responsible for this functionality.

**Setting Up Routing**\
Import the RouterModule: In your `app.routes.ts`, import RouterModule and define your routes.

```ts
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { RouterModule, Routes } from '@angular/router';
import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  // Add more routes here
];

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent
  ],
  imports: [
    BrowserModule,
    RouterModule.forRoot(routes) // Configure the router
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```