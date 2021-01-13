<!-- .slide: data-background="#000000" -->
## Continuation-Passing Style (CPS)

UiT INF-3910-5

Part 1

---

### Introduction

* CPS is a style of programming
* CPS is isomorphic to _direct style_
* CPS is a powerful technique, to be used with care
* CPS lead to code which is hard to understand and maintain

---

### Why CPS?

In pure functional programming, CPS is useful for:

* Exceptions, threading, async computations, coroutines and flow control.

---

### Continuations

* A _continuation_ is essentially a _callback function_
* Continuation-passing is a powerful technique where _control_ is passed
  explicitly by the _caller_ to the _callee_ as a function
* The _callee_ does not return, but passes the result to the continuation
  instead

---

### Direct style vs. CPS

```fsharp
val f : a -> b
val fCps : a -> (cont: b -> r) -> r
```

OR:

```fsharp
type Cont<r,a> = (a -> r) -> r
val fCps : a -> Cont<r, b>
```

---

### Continuations (cont.)

* We can think of continuations as suspended computations: _They need a further
    function to complete_
* A more philosophical view is that _values_ are _meaningless_ until we _use_
    them

```fsharp
let five f = f 5 // or let five = (|>) 5
five string
```

---

### Continuations as callbacks

We can also think of continuations as _callbacks_:

```fsharp
val g :
  a                       ->
  (onError   : Cont<r,e>) ->
  (onSuccess : Cont<r,b>)
```

---

### Weird and wonderful

We can even do things like:

```fsharp
List.map ((|>) 2) [ (*) 2; (*) 3; (+) 42]
```

---

### Example: Pythagoras

```fsharp
let add = (+)

let square x = x * x

let pythagoras x y = add (square x) (square x)
```

---

### Example: Pythagoras CPS

```fsharp
let addCPS x y = fun f -> f (x + y)

let squareCPS x f =  f (x * x)

let pythagorasCPS x y f =
  squareCPS x (fun x' ->
  squareCPS y (fun y' ->
  addCPS x' y' f))
```

---

<!-- .slide: data-background="#000000" -->
## End of part 1

---

<!-- .slide: data-background="#000000" -->
## Continuation-Passing Style (CPS)

UiT INF-3910-5

Part 2: _Compositon_

---

### Recap

* A _continuation_ is a _callback function_
* The _callee_ passes the result to the continuation instead of returning

```fsharp
val f : a -> b

val f' : a -> (cont: b -> r) -> r
```

---

### Example: Thrice

```fsharp
let thrice f x = f (f (f x)) // x |> f |> f |> f

let thriceCPS (f : 'a -> ('b -> 'r) -> 'r) (x : 'a) =
  fun k ->
    f x (fun fx ->
    f fx (fun ffx ->
    f ffx k))
```

---

### Chaining continuations

`There is a pattern! Let's abstract!`

```fsharp
let chain
  (c : (a -> r) -> r)
  (f : (a -> (b -> r) -> r)
  = fun k -> c (fun x -> f x k)

val chain' :
  (s : Cont<r,a>) -> (f : a -> Cont<r,b>) -> (b : Cont<r,b>)
```

---

### The Cont<r,a> monad

The `Cont<r,a>` type is a _monad_ in `a`:

```fsharp
Cont.bind = chain
```

```fsharp
let thriceM f x = (|>) x >>= f >>= f >>= f
```

---

### The Cont<r,a> functor

`Cont<r,a>` is naturally also a functor in `a`:

```fsharp
Cont.map f x = fun g -> x (f >> g)

Cont.return x = fun f -> f x
```

---

### Computation expression for CPS

```fsharp
type ContBuilder() =
  member x.Bind(a,b) = a >>= b
  member x.Return a = Cont.return a
  member x.ReturnFrom a = a

let cont = ContBuilder()
```

---

### Computation expression (cont.)

```fsharp
let thrice f x =
  cont {
    let! x'  = f x
    let! x'' = f x'
    return! f x''
  }
```

---

<!-- .slide: data-background="#000000" -->
## End of part 2

Next: _Asynchronous computations_

