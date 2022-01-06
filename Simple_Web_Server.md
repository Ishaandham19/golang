# Simple Web Server in Go

``` Go
import (
	"fmt"
	"io/ioutil"
	"log"
	"net/http"
)

func main() {
	http.HandleFunc("/", func(rw http.ResponseWriter, r *http.Request) {
		log.Println("Running Hello World Handler")

		// read the body of req
		b, err := ioutil.ReadAll(r.Body)
		if err != nil {
			log.Println("Error reading body", err)

			http.Error(rw, "Unable to read request body", http.StatusBadRequest)
			return
		}

		// write the response
		fmt.Fprintf(rw, "Hello %s", b)
	})

	// requests to the path /goodbye handled
	http.HandleFunc("/goodbye", func(http.ResponseWriter, *http.Request) {
		log.Println("Goodbye World")
	})

	// Create server and listen on all ip adresses with port 9090
	err := http.ListenAndServe(":9090", nil)
	log.Fatal(err)
}
```

## Description 

> TODO - Add a brief description about the above code. Add details about the http library in Go