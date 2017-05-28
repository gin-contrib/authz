Gin-authz [![GoDoc](https://godoc.org/github.com/casbin/gin-authz?status.svg)](https://godoc.org/github.com/casbin/gin-authz)
======

Gin-authz is an authorization middleware for [Gin](https://github.com/gin-gonic/gin), it's based on [https://github.com/casbin/casbin](https://github.com/casbin/casbin).

## Installation

    go get github.com/casbin/gin-authz

## Simple Example

```Go
package main

import (
	"net/http"

	"github.com/casbin/casbin"
	"github.com/casbin/gin-authz"
	"github.com/gin-gonic/gin"
)

func main() {
	// load the casbin model and policy from files, database is also supported.
	e := casbin.NewEnforcer("authz_model.conf", "authz_policy.csv")

	// define your router, and use the Casbin authz middleware.
	// the access that is denied by authz will return HTTP 403 error.
    router := gin.New()
    router.Use(authz.NewAuthorizer(e))
}
```

## Getting Help

- [casbin](https://github.com/casbin/casbin)

## License

This project is under MIT License. See the [LICENSE](LICENSE) file for the full license text.
