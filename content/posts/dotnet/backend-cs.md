+++
title = 'ASP.NET'
date = 2025-07-22T12:18:47+07:00
tags = ["dotnet", "c#", "oops"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A simple document providing how the ASP.NET framework can be used to create web applications"
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

# ASP.NET

Basics of the code

```cs
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();

app.Run();
```

Explaination
Certainly! Let's break down the provided code snippet line by line. This code is typically found in the `Program.cs` file of an ASP.NET Core application and is part of the setup for a minimal API or web application.

### Code Breakdown

```csharp
var builder = WebApplication.CreateBuilder(args);
```
- **Explanation**: This line creates a new instance of a `WebApplicationBuilder`. The `CreateBuilder` method initializes the builder with the command-line arguments passed to the application (`args`). This builder is used to configure services and middleware for the application.

```csharp
builder.Services.AddEndpointsApiExplorer();
```
- **Explanation**: This line adds the **Endpoints API Explorer** service to the application's service collection. This service is used to discover and document the API endpoints in your application. It helps in generating metadata about the endpoints, which can be useful for tools like Swagger.

```csharp
builder.Services.AddSwaggerGen();
```
- **Explanation**: This line adds the **Swagger generator** to the service collection. Swagger is a tool that helps document and test APIs. By adding this service, you enable the generation of Swagger documentation for your API endpoints, which can be accessed via a web interface.

```csharp
var app = builder.Build();
```
- **Explanation**: This line builds the `WebApplication` instance using the configured builder. At this point, the application is ready to be configured with middleware and endpoints.

```csharp
if (app.Environment.IsDevelopment())
```
- **Explanation**: This line checks if the application is running in the **Development** environment. The `IsDevelopment()` method is part of the `IHostEnvironment` interface, which provides information about the hosting environment.

```csharp
{
    app.UseSwagger();
    app.UseSwaggerUI();
}
```
- **Explanation**: If the application is in the Development environment, these two lines enable Swagger middleware:
  - `app.UseSwagger()`: This middleware generates the Swagger JSON document that describes the API.
  - `app.UseSwaggerUI()`: This middleware sets up the Swagger UI, which is a web interface that allows you to interact with the API endpoints defined in your application. You can access it typically at `/swagger` in your browser.

```csharp
app.UseHttpsRedirection();
```
- **Explanation**: This line adds middleware that redirects HTTP requests to HTTPS. It ensures that all requests to the application are secure by enforcing the use of HTTPS.

```csharp
app.Run();
```
- **Explanation**: This line starts the application and begins listening for incoming HTTP requests. It is the final step in the application setup, and once this line is executed, the application is running and ready to handle requests.


## Making a simple CRUD application

In order to make a simple application we need to have two thinks working simultaneously, a .NET backend and a database that will manage the data. We will also be using an ORM (Object relational mapping), this reduces our dependencies on directly accessing the database and working with a wrapper.

- Content of `Program.cs` - basic driver code
    ```cs
    using Microsoft.EntityFrameworkCore;

    var builder = WebApplication.CreateBuilder(args);

    // Add services to the container.
    builder.Services.AddDbContext<ApplicationDbContext>(options =>
        options.UseNpgsql(builder.Configuration.GetConnectionString("DefaultConnection")));

    builder.Services.AddEndpointsApiExplorer();
    builder.Services.AddSwaggerGen();
    builder.Services.AddControllers();

    var app = builder.Build();

    if (app.Environment.IsDevelopment())
    {
        app.UseSwagger();
        app.UseSwaggerUI();
    }

    app.UseHttpsRedirection();
    app.UseAuthorization();
    app.MapControllers();

    app.MapGet("/", () => "Hello World!");

    app.Run();
    ```

- `Controllers/UserController.cs` - handles req
    ```cs
    using Microsoft.AspNetCore.Mvc;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    using Microsoft.EntityFrameworkCore;

    [ApiController]
    [Route("api/[controller]")]
    public class UsersController : ControllerBase
    {
        private readonly ApplicationDbContext _context;

        public UsersController(ApplicationDbContext context)
        {
            _context = context;
        }

        [HttpGet]
        public async Task<ActionResult<List<User>>> GetUsers()
        {
            return await _context.Users.ToListAsync();
        }

        [HttpPost]
        public async Task<ActionResult<User>> CreateUser(User user)
        {
            _context.Users.Add(user);
            await _context.SaveChangesAsync();
            return CreatedAtAction(nameof(GetUsers), new { id = user.Id }, user);
        }
    }
    ```
- `Data/ApplicationDbContext.cs` - middleman of communication to the DB
    ```cs
    using Microsoft.EntityFrameworkCore;

    public class ApplicationDbContext : DbContext
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
            
        }
        
        public DbSet<User> Users { get; set; }
    }
    ```