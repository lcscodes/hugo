---
title: "Go"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Go

## Command Line

### Init Modul

Init modul adalah command pertama kali yang harus dijalankan setelah membuat folder project.

        go mod [nama project]

### Run Server

        go run main.go

## Code

### Router main.go

        package main

        import (
            "fmt"
            "net/http"
        )

        func main() {
        	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
            	fmt.Fprintln(w, "halo!")
            })

            fmt.Println("starting web server at http://localhost:10001/")
            http.ListenAndServe(":10001", nil)
        }
