
go语言核心的http就是由```http.Server```实现的，路由控制是主要都交由

```ServeHTTP(w http.ResponseWriter, r *http.Request)```

下面实现了一个自定义的路由实现思路，拦截了```/hello```和```/bye```的路由，其他都是默认的输出

```go

package test

import (
	"io"
	"log"
	"net/http"
	"time"
)

var mux map[string]func(http.ResponseWriter, *http.Request)

func TestCustomHttpServer() {
	server := http.Server{
		Addr:        ":8080",
		Handler:     &myHandler{},
		ReadTimeout: 5 * time.Second,
	}
	mux = make(map[string]func(http.ResponseWriter, *http.Request))
	mux["/hello"] = sayhello
	mux["/bye"] = sayBye
	err := server.ListenAndServe()
	if err != nil {
		log.Fatal(err)
	}
}

type myHandler struct{}

func (*myHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	if h, ok := mux[r.URL.String()]; ok {
		h(w, r)
		return
	}
	io.WriteString(w, "hello this is default handler path = "+r.URL.Path)
}

func sayhello(w http.ResponseWriter, req *http.Request) {
	io.WriteString(w, "Hello this is sayHello ")
}

func sayBye(w http.ResponseWriter, req *http.Request) {
	io.WriteString(w, "Bye Bye!!!")
}

```