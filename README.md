Authz [![Build Status](https://travis-ci.org/gin-contrib/authz.svg?branch=master)](https://travis-ci.org/gin-contrib/authz) [![Coverage Status](https://coveralls.io/repos/github/gin-contrib/authz/badge.svg?branch=master)](https://coveralls.io/github/gin-contrib/authz?branch=master) [![GoDoc](https://godoc.org/github.com/gin-contrib/authz?status.svg)](https://godoc.org/github.com/gin-contrib/authz)
======

Authz is an authorization middleware for [Gin](https://github.com/gin-gonic/gin), it's based on [https://github.com/casbin/casbin](https://github.com/casbin/casbin).

## Installation

    go get github.com/gin-contrib/authz

## Simple Example

```Go
package main

import (
	"net/http"

	"github.com/casbin/casbin"
	"github.com/gin-contrib/authz"
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

## Documentation

The authorization determines a request based on ``{subject, object, action}``, which means what ``subject`` can perform what ``action`` on what ``object``. In this plugin, the meanings are:

1. ``subject``: the logged-on user name
2. ``object``: the URL path for the web resource like "dataset1/item1"
3. ``action``: HTTP method like GET, POST, PUT, DELETE, or the high-level actions you defined like "read-file", "write-blog"


For how to write authorization policy and other details, please refer to [the Casbin's documentation](https://github.com/casbin/casbin).

## Getting Help

- [Casbin](https://github.com/casbin/casbin)

## License

This project is under MIT License. See the [LICENSE](LICENSE) file for the full license text.
