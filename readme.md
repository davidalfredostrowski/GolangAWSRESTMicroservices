
sudo apt-get update
sudo apt install golang-go


package main

import (
        "fmt"
        "net/http"
)

func main() {
        http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
                fmt.Fprintf(w, "Path: %s!", r.URL.Path[1:])
        })

        http.ListenAndServe(":8080", nil)
}




curl -X GET http://ec2-35-164-152-184.us-west-2.compute.amazonaws.com:8080



##### example two 

3
sudo apt install golang-github-gorilla-mux-dev


go mod init   gorilla/mux
go mod tidy
go get github.com/gorilla/mux


usage: go mod tidy [-v] Tidy makes sure go. 
mod matches the source code in the module. 
It adds any missing modules necessary to build 
the current module's packages and dependencies,
 and it removes unused modules that don't provide 
any relevant packages. It also adds 
any missing entries to go.

package main


import (
        "fmt"
        "log"
        "net/http"
        "time"

        "github.com/gorilla/mux"
)

func main() {
        router := mux.NewRouter()
        router.HandleFunc("/resources", func(w http.ResponseWriter, r *http.Request) {
                fmt.Fprintf(w, "/resources")
        })
        router.HandleFunc("/resources/{id:[0-9]+}", func(w http.ResponseWriter, r *http.Request) {
                fmt.Fprintf(w, "/resources/{id:[0-9]+}: %s!", mux.Vars(r)["id"])
        })
        router.HandleFunc("/resources/{id:[0-9]+}/values", func(w http.ResponseWriter, r *http.Request) {
                fmt.Fprintf(w, "/resources/{id:[0-9]+}/values: %s", mux.Vars(r)["id"])
        })

        srv := &http.Server{
                Handler:      router,
                Addr:         ":8080",
                WriteTimeout: 15 * time.Second,
                ReadTimeout:  15 * time.Second,
        }

        log.Fatal(srv.ListenAndServe())
}


curl http://ec2-35-164-152-184.us-west-2.compute.amazonaws.com:8080/resources/123
curl http://ec2-35-164-152-184.us-west-2.compute.amazonaws.com:8080/resources/456/values


curl http://ec2-34-222-53-60.us-west-2.compute.amazonaws.com:8080/resources/123
curl http://ec2-34-222-53-60.us-west-2.compute.amazonaws.com:8080/resources/456/values
