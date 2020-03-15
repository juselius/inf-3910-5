<!-- .slide: data-background="#000000" -->
## UiT INF-3910-5

#### Functional programming in F\#

##### The Corona edition

--

<!-- .slide: data-background="#ff8888" -->
## Testing, testing

This is a test slide deck, just to check that everyting works

- A bullet point
- Another convincing argument
- These slides have been generated with _cicero.xyz_ and `remark.js`

---

## Code blocks are no problem

Here we have some F# code:

```fsharp
let webApp (next: HttpFunc) (ctx: HttpContext) =
// let config = ctx.GetService<IConfiguration>()
choose [
   POST >=> choose [
      route "/add" >=> addFile
      route "/upload" >=> addFileJS
   ]
   GET >=> choose [
      routex "(/?)" >=> htmlFile (publicPath + "/index.html")
      routef "/get/%s/%s" getFileClient
      route "/signin" >=> signIn >=> redirectTo false "/?signin"
      route "/signout" >=> signOut >=> redirectTo false "/?signout"
      //route "/api/test" >=> authorized >=> json "ok"
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
