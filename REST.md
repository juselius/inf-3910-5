<!-- .slide: data-background="#000000" -->
## Databases and REST

UiT INF-3910-5

---

### Overview

* Databases
* REST: Representational State Transfer
* CRUD: Create Read Update Delete

---

### Databases

* SQL vs. NoSQL
* SDKs vs. REST APIs
* Relational, Table, Graph, Document, Key-Value
* _Seven databases in seven weeks_

---

### SQL and FSharp

* Raw SQL
* Type providers
* Entity Framework Core

---

### Entity Framework Core

* Object-Relational Mapping
* Migrations
* Offline
* C#
* Pitfalls RTFM

```sh
dotnet tool install -g dotnet-ef
dotnet ef migration
dotnet ef database
dotnet ef dbcontext scaffold
```

---

### DbContext

```csharp
namespace Entity {
    public class DataContext : DbContext {
        public DbSet<Person> People { get; set; }
    }
    public class Person {
        [Key]
        public int PersonId { get; set; }
        public string FullName { get; set; }
        public int? Age { get; set; }
    }
}
```

---

### Migrations and updates

1. Create a migration
2. Update database

```sh
dotnet ef migration add Initial -s ../Server -c DataContext
dotnet ef database update -s ../Server
```

---

### Query CE and LINQ

* Language Itegrated Query

```fsharp
let ctx = Entity.DataContext ()
query {
    for i in ctx.People do
        where (i.FullName.Contains "bob")
}
|> Array.ofSeq
```

---

### Seq queries

```fsharp
let ex = [ 1; 2; 3 ]
query {
    for i in ex do
        where ( i > 1)
}
|> Array.ofSeq
```

---

### REST and CRUD

##### HTTP verbs

* GET
* UPDATE
* PUT/PATCH
* DELETE

---

### Demo

https://github.com/juselius/inf-3910-demos

---

<!-- .slide: data-background="#000000" -->
## End of REST

Next: `Testing`

