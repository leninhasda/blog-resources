---
title: "Golang FileServer - Serving Static Files"
template: templates/post.pug
date: 2018-02-10
author: Lenin Hasda
keywords: go, goland, go-server, static, serving, go-render, rendering, go-template, template
---

It's been while since I started playing with Golang and it's really great for making apis and microservices. You can however serve static files pretty easily as well. Here is how.

Let's say you have a directory structure like following and you want to serve them as static files!

```
|- app
   |- static
      |- file-one.txt
      |- file-two.html
      |- file-three.css
  |- main.go
```

Now inside your `main.go` file type the following few lines:

```
package main

import (
	"net/http"
)

func main() {
	fs := http.FileServer(http.Dir("./static"))
	http.Handle("/", fs)

	http.ListenAndServe(":5000", nil)
}
```

That's it, open up a terminal and run the file:
```
go run main.go
```
And baam! You have a file server running on port `:5000`. If you browse `http://localhost:5000`  you will see the files from static folders listed on the browser.

What we are doing here is, we take the `static` directory and cast it as `http.Dir` and told the http that we want to use it as `http.FileServer`. Then in the root handler `/` we set the file server. Finally we started the server in port `5000` and done!

> Based on this I made a really simple file server app which is available at: https://github.com/leninhasda/go-serve
