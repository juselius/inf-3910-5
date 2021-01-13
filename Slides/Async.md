<!-- .slide: data-background="#000000" -->
## Asynchronous computation

UiT INF-3910-5

---

### Introduction

Asynchronous operations are very important in modern programming:

* Non-blocking communication and I/O
* Concurrency and parallelism
* Promises, Tasks, Observables

---

### Non-blocking I/O

* A non-blocking operation returns immediately
* _Cannot return a value!_
* Must mutate state (somehow)
* Powerful combination in conjunction with `MailboxProcessor`

---

### Async continuation

`Async` is just a _continuation_ returning `unit`:

```fsharp
val f : a -> (b -> unit) -> unit

type Async<a> = (a -> unit) -> unit

val f : a -> Async<b>
```

---

### Composition

```fsharp
let trio
  (v : ('a -> unit) -> unit) =
  (f : 'a -> ('b -> unit) -> unit) =
  (g : 'b -> ('c -> unit) -> unit) =
  fun k ->
    v   (fun x ->
    f x (fun y ->
    g y k
    )
  )
```

---

### Composition

```fsharp
let trio
  (v : Async<'a>) =
  (f : 'a -> Async<'b>) =
  (g : 'b -> Async<'c>)=
  fun k ->
    v   (fun x ->
    f x (fun y ->
    g y k
    )
  )
```

---

### Chaining Async

The `Async<a>` type is a _monad_ in `a`:

```fsharp
let bind
  (v : (a -> unit) -> unit)
  (f : (a -> (b -> unit) -> unit)
  = fun k -> v (fun x -> f x k)

val bind =
  (v : Async<a>) -> (f : a -> Async<b>) -> (b : Async<b>)
```

---

### Computation expression

```fsharp
let thrice f x =
  async {
    let! x'  = f x
    let! x'' = f x'
    return! f x''
  }
  |> Async.ignore
  |> Async.Start
```

---

### Examples

---

<!-- .slide: data-background="#000000" -->
## End of async

Next: `MailboxProcessor`

