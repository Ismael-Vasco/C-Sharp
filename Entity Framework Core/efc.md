# Entity Framework Core

Este documento contiene **todas las operaciones posibles** sobre la entidad `User` usando **Entity Framework Core**, incluyendo CRUD, consultas avanzadas, asíncronas, SQL crudo y control de estados.


### 1. Instalar Dependencias
#### Microsoft.EntityFrameworkCore
```bash
dotnet add package Microsoft.EntityFrameworkCore --version <version>
```
#### 
```
```
### 2. Usar migraciones

Instala herramientas si no las tienes:
```bash
dotnet tool install --global dotnet-ef
```
Luego:
```bash
dotnet ef migrations add InitialCreate
```
```bash
dotnet ef database update
```

---

## 🔹 Crear (INSERT)

### Agregar un usuario
```csharp
db.users.Add(new User { FirstName = "Andres", LastName = "Lopez" });
db.SaveChanges();
```

## Agregar varios usuarios

```csharp
db.users.AddRange(
    new User { FirstName = "Laura", LastName = "Martinez" },
    new User { FirstName = "Carlos", LastName = "Ramirez" }
);
db.SaveChanges();

```

## Agregar un usuario de forma asíncrona
```csharp
await db.Users.AddAsync(new User { FirstName = "Maria", LastName = "Gomez" });
await db.SaveChangesAsync();

```

## Agregar muchos usuarios de forma asíncrona
```csharp
await db.users.AddRangeAsync(
    new User { FirstName = "Jose", LastName = "Lopez" },
    new User { FirstName = "Paula", LastName = "Sanchez" }
);
await db.SaveChangesAsync();

```

## Listar todos los usuarios

```csharp
return db.users.ToList();

```

## Buscar por ID

```csharp
return db.users.Find(1);

```

## Buscar por condición

```csharp
return db.users.Where(u => u.LastName == "Lopez").ToList();

```

## Primer usuario que cumpla condición

```csharp
return db.users.FirstOrDefault(u => u.Email == "andres@example.com");

```

## Obtener un único resultado

```csharp
return db.users.SingleOrDefault(u => u.Username == "andres");

```

## Contar usuarios

```csharp
return db.users.Count();

```

## Verificar existencia

```csharp
return db.users.Any(u => u.Email == "andres@example.com");

```


## Seleccionar campos específicos

```csharp
return db.users.Select(u => new { u.Id, u.Email }).ToList();

```

## Ordenamiento

```csharp
return db.Users.OrderBy(u => u.LastName).ThenBy(u => u.FirstName).ToList();
```

## Paginación

```csharp
return db.Users.OrderBy(u => u.Id).Skip(10).Take(5).ToList();
```

## Consultas sin tracking

```csharp
return db.Users.AsNoTracking().ToList();
```

## Incluir relaciones (Eager Loading)

```csharp
return db.Users.Include(u => u.Orders).ToList();
```

## Carga explícita (Explicit Loading)

```csharp
var user = db.Users.First();
db.Entry(user).Collection(u => u.Orders).Load();
```

## SQL Crudo

```csharp
return db.Users.FromSqlRaw("SELECT * FROM Users WHERE Edad > 25").ToList();
```

## SQL interpolado

```csharp
int edad = 25;
return db.Users.FromSqlInterpolated($"SELECT * FROM Users WHERE Edad > {edad}").ToList();
```


