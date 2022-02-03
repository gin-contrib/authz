# Authz

[![CodeQL](https://github.com/gin-contrib/authz/actions/workflows/codeql.yml/badge.svg)](https://github.com/gin-contrib/authz/actions/workflows/codeql.yml)
[![Run Tests](https://github.com/gin-contrib/authz/actions/workflows/go.yml/badge.svg?branch=master)](https://github.com/gin-contrib/authz/actions/workflows/go.yml)
[![codecov](https://codecov.io/gh/gin-contrib/authz/branch/master/graph/badge.svg)](https://codecov.io/gh/gin-contrib/authz)
[![Go Report Card](https://goreportcard.com/badge/github.com/gin-contrib/authz)](https://goreportcard.com/report/github.com/gin-contrib/authz)
[![GoDoc](https://godoc.org/github.com/gin-contrib/authz?status.svg)](https://godoc.org/github.com/gin-contrib/authz)
[![Join the chat at https://gitter.im/gin-gonic/gin](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/gin-gonic/gin)

Authz is an authorization middleware for [Gin](https://github.com/gin-gonic/gin), it's based on [https://github.com/casbin/casbin](https://github.com/casbin/casbin).

## Installation

```bash
go get github.com/gin-contrib/authz
```

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
