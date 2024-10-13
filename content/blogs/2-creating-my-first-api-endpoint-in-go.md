+++
title = '2 Creating my first API endpoint in Go'
date = 2024-06-20T22:37:09+05:30
draft = true
+++

As stated in the first post of the series, I am going to develop a simple API based tic-tac-toe application in Go. Since this is my first ever GO project ever, I wanted to start simple, by creating an endpoint for creating a Game.

```ln:false
	POST /games 
```

Go has a powerful package call `net/http` which can be used to create API applications. This package is part of Go's standard library. All it takes are few lines to setup the server, configure the endpoint and start handling requests

```go lineNos:true
package main

import (
	"encoding/json"
	"log"
	"net/http"
)

func main() {
	// registering the /games URL to be handled by gamesHandler function
	http.HandleFunc("/games", gamesHandler)

	// Starting the service at PORT 9099
	log.Fatal(
		http.ListenAndServe(":9099", nil),
	)
}

// defining gamesHandler function
func gamesHandler(w http.ResponseWriter, r *http.Request) {
	// Parses the json in request body and assigns it to var i
	var i any
	err := json.NewDecoder(r.Body).Decode(&i)
	if err != nil {
		http.Error(w, "Error while reading input", http.StatusUnprocessableEntity
		return
	}

	// Responds with the json body from request
	w.Header().Set("Content-Type", "application/json")
	json.NewEncoder(w).Encode(i)
	if err != nil {
		http.Error(w, "Error while producing output", http.StatusInternalServerError)
		return
	}
}
```

The above program exposes the endpoint `/games`. It reads the request body as JSON and responds with the same JSON.

Here in line 22 I've declared a special variable `i` of type `any`(alias for `interface{}` - [empty interface](https://go.dev/tour/methods/14)). This allows the variable to be assigned with values of any type. The next line converts the request Body(`r.Body`) to `map[string]interface{}` and assigns it to the variable `i`. 

There is another way to parse JSON using `json.Unmarshal`. Also for converting object to JSON it supplies `json.Marshal` method. But here there are lots of error handling to be done and the entire JSON needs to be set in memory as `[]byte` value before writing it to the response. So I will continue to use `Encode` and `Decode` methods.

```go
func gamesHandler(w http.ResponseWriter, r *http.Request) {
	// Parses the json in request body and assigns it to var i
	var i any
	reqData, err := ioutil.ReadAll(r.Body)
	if err != nil {
		http.Error(w, "Error while reading input", http.StatusUnprocessableEntity)
		return
	}
	err = json.Unmarshal(reqData, &i)
	if err != nil {
		http.Error(w, "Error while reading input", http.StatusUnprocessableEntity)
		return
	}

	// Responds with the json body from request
	w.Header().Set("Content-Type", "application/json")
	resData, err := json.Marshal(i)
	if err != nil {
		http.Error(w, "Error while producing output", http.StatusInternalServerError)
		return
	}
	_, err = w.Write(resData)
	if err != nil {
		http.Error(w, "Error while producing output", http.StatusInternalServerError)
		return
	}
}
```

As of now this endpoint accepts all HTTP methods (GET, PUT, PATCH, POST, ..). But it should ideally respond to POST alone. Lets modify the gamesHander to respond with error if the request method is not POST

```go
func gamesHandler(w http.ResponseWriter, r *http.Request) {
	// Allow only POST method
	if r.Method != http.MethodPost {
		http.Error(w, "HTTP method not allowed", http.StatusMethodNotAllowed)
		return
	}

	// Parses the json in request body and assigns it to var i
	var i any
	err := json.NewDecoder(r.Body).Decode(&i)
	if err != nil {
		http.Error(w, "Error while reading input", http.StatusUnprocessableEntity)
		return
	}

	// Responds with the json body from request
	w.Header().Set("Content-Type", "application/json")
	json.NewEncoder(w).Encode(i)
	if err != nil {
		http.Error(w, "Error while producing output", http.StatusInternalServerError)
		return
	}
}

```

Now the `/games` endpoint is up and responds only to POST request. If there are any other request Methods used or if the JSON provided is not valid json, the endpoint is returning error, but in plain text - not in JSON format. I will attempt this in the next post along with creating the Game resource.

Code can be found here: https://github.com/shivakumaarmgs/tic_tac_toe_api/tree/0.0.1ui
