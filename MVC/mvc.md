# Guide: Create a .NET MVC application with MySQL

This guide details the steps for setting up a .NET MVC application with MySQL, creating migrations, and displaying data in views.

---
## 1. Installing NuGet Packages
Run these commands in your project's root directory to install the MySQL drivers and design tools:

```bash
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Pomelo.EntityFrameworkCore.MySql
dotnet add package Microsoft.EntityFrameworkCore.Design
```
## 2. Configuring the Connection String
Edit `appsettings.json` to add your MySQL connection string:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Port=3306;Database=NombreTuDB;User=root;Password=TuPassword;"
  }
}
```

## 3. Creating the Model
In the `Models/` folder, create the `Users.cs` file:

```csharp
namespace MVCProject.Models;

public class Users
{
    public int Id { get; set; }
    public required string Name { get; set; }
    public required string Lastname { get; set; }
}
```

## 4. Creating the Data Context (DbContext)
Create a `Data/` folder and, inside it, the `ApplicationDbContext.cs` file:

```csharp
using Microsoft.EntityFrameworkCore;
using YourProject.Models;

namespace YourProject.Data;

public class ApplicationDbContext : DbContext
{
    public DbSet<Users> Users { get; set; }

    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) :base(options)
    {
    }

    // Tables configuration
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Users>()
            .Property(n => n.Name)
            .HasMaxLength(100)
            .IsRequired();
        
        modelBuilder.Entity<Users>()
            .Property(n => n.Lastname)
            .HasMaxLength(100)
            .IsRequired();
    }
}
```

## 5. Configuration in Program.cs
IMPORTANT! Register the service BEFORE the line `var app = builder.Build();`.

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddDbContext<MysqlContext>(options =>
    options.UseMySql(builder.Configuration.GetConnectionString("DefaultConnection"),
        ServerVersion.AutoDetect(builder.Configuration.GetConnectionString("DefaultConnection"))));

builder.Services.AddControllersWithViews();

var app = builder.Build();
```

## 6. Database Migrations
To create the database in MySQL from your C# code:

```bash
dotnet ef migrations add InitialCreate
dotnet ef database update
```

## 7. Creating a Controller
In the `Controllers/` folder, create the `HomeController.cs` file:

```csharp
using System.Diagnostics;
using Microsoft.AspNetCore.Mvc;
using MVCProject.Data;
using MVCProject.Models;

namespace MVCProject.Controllers;

public class HomeController : Controller
{
    private readonly MysqlContext _context;

    public HomeController(MysqlContext context)
    {
        _context = context;
    }

    public IActionResult Show()
    {
        List<Users> users = _context.Users.ToList();
        return View(users);
    }

    [ResponseCache(Duration = 0, Location = ResponseCacheLocation.None, NoStore = true)]
    public IActionResult Error()
    {
        return View(new ErrorViewModel { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier });
    }
}
```

## 8. Creating a View
In the `Views/` folder, create the `Show.cshtml` file:

```csharp
@model IEnumerable<MVCProject.Models.Users>

<table class="table">
    @foreach (var item in Model) {
        <tr>
            <td>@item.Id</td>
            <td>@item.Name</td>
            <td>@item.Lastname</td>
        </tr>
    }
</table>
```
