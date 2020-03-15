<!-- .slide: data-background="#000000" -->
## UiT INF-3910-5

#### Functional programming in F&num;

_The Corona edition_

--

<!-- .slide: data-background="#696969" -->
## Testing

- The audio is clear and crisp
- Code examples are readable
- These slides have been generated with _https://cicero.xyz_ and `reveal.js`

---

## Code blocks are no problem

Here we have some F# code:

```fsharp
let webApp (next: HttpFunc) (ctx: HttpContext) =
choose [
   POST >=> choose [
      route "/add" >=> addFile
   ]
   GET >=> choose [
      routef "/get/%s/%s" getFileClient
      route "/api/auth" >=> authorized >=> json "ok"
   ]
] next ctx
```

[Source](https://github.com/juselius/inf-3910-5)

---

## Images (1/2)

An image fetched from the web:

![Sample image](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4f/The_Young_Cicero_Reading.jpg/316px-The_Young_Cicero_Reading.jpg)

---

## Images (2/2)

An image stored alongside the slides:

![Sample image](Whiteboard.svg)
