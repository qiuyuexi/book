# net/http初步学习.md

先上代码

```text
package main

import (
	"fmt"
	"net/http"
)

func handle(r http.ResponseWriter, w *http.Request) {
	fmt.Println("hello")
}

type mux struct {

}

func (mux *mux) ServeHTTP(w http.ResponseWriter,r *http.Request){
	fmt.Println(r)
	return
}


func main() {
	http.HandleFunc("/hello",handle)
	//http.ListenAndServe(":9090",nil);
	http.ListenAndServe(":9090",&mux{});
}
```

大致调用流程

```text
#####  1

``` go
 http.ListenAndServe(":9090",&mux{});


```


``` go 
func ListenAndServe(addr string, handler Handler) error {
	server := &Server{Addr: addr, Handler: handler}
	return server.ListenAndServe()
}
```

#####  2

``` go
func (srv *Server) ListenAndServe() error {
	...
	return srv.Serve(tcpKeepAliveListener{ln.(*net.TCPListener)})
}

```


#####  3 

``` go
func (srv *Server) Serve(l net.Listener) error {
	...
	for {
		...
		c := srv.newConn(rw)
		c.setState(c.rwc, StateNew) // before Serve can return
		go c.serve(ctx)
	}
}

// Create new connection from rwc.
func (srv *Server) newConn(rwc net.Conn) *conn {
	c := &conn{
		server: srv,
		rwc:    rwc,
	}
	if debugServerConnections {
		c.rwc = newLoggingConn("server", c.rwc)
	}
	return c
}

```


#####  4

``` go
func (c *conn) serve(ctx context.Context) {
	...
	

	for {
		w, err := c.readRequest(ctx)
		...
		
		serverHandler{c.server}.ServeHTTP(w, w.req)
		...
	}
}


// serverHandler delegates to either the server's Handler or
// DefaultServeMux and also handles "OPTIONS *" requests.
type serverHandler struct {
	srv *Server
}

func (sh serverHandler) ServeHTTP(rw ResponseWriter, req *Request) {
	handler := sh.srv.Handler
	if handler == nil {
		handler = DefaultServeMux
	}
	if req.RequestURI == "*" && req.Method == "OPTIONS" {
		handler = globalOptionsHandler{}
	}
	handler.ServeHTTP(rw, req)
}
``` 
```

