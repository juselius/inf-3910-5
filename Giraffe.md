<!-- .slide: data-background="#000000" -->
## ASP.NET Core and Giraffe

UiT INF-3910-5

---

### Overview

* Anatomy of web services
* Simple, in theory
* Huge topic

---

### Web request pipeline

![Web pipeline](web-pipeline.png)

---

### Functional pipelines

```fsharp
type HttpCtx = { ... }
type HttpFuncResult = Async<HttpCtx option>
type HttpFunc = HttpCtx -> HttpFuncResult

val (>>=) : HttpFuncResult -> HttpFunc -> HttpFuncResult
val (>=>) : HttpFunc -> HttpFunc -> HttpFunc

```

---

### Building web servers

* ASP.NET Core
* Giraffe
* _Saturn_
* _Suave_ (inspired by Haskell)

---

### Communication

* Thoth
* _Fable.Remoting_
* _Elmish.Bridge_

---

### ASP.NET Core

* Microsoft
* Performant
* Kestrel and IIS
* Large collection of components

### Architecture

* Middleware
* Builder pattern
* Delegates
* Dependency Injection
* Continuations

---

### Middleware

![Delegate pipeline](request-delegate-pipeline.png)

---

### Configuration

![Delegate pipeline](request-delegate-pipeline.png)

---

### Dependency Injection

![Delegate pipeline](request-delegate-pipeline.png)

---

### Giraffe

* ASP.NET Core Middleware
* Functional framework
* Inspired by Suave

---

### Using continuations

Composing pipelines causes a lot of (unnecessary) wrapping and unwrapping of
types:

* Poor performace
* Stack pressure

Explicit continuations avoids this, and:

* Early exit
* Tail-Call Optimization

---

### Demo

---

<!-- .slide: data-background="#000000" -->
## End of Fable

Next: `ASP.NET Core and Giraffe`

