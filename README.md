# Opinionated Go

This is my curated list of Go packages.

Unlike [awesome-go](https://github.com/avelino/awesome-go), which is a very comprehensive list of Go packages, this list is opinionated and contains only a subset of packages that I find good to start with.

The purpose of this list is to provide a selection of go-to options for basic needs when there are no specific requirements.

If you have any feedback, feel free to reach out to me directly.


## Contents

- [Basic](#basic)
    - [Console](#console)
    - [Data Serialization](#data-serialization)
    - [Dependency Injection](#dependency-injection)
    - [Error Handling](#error-handling)
    - [Logging](#logging)
    - [Testing](#testing)

- [Server Side](#server-side)
    - [Databases](#databases)
    - [HTTP Server](#http-server)
    - [OpenAPI](#openapi)

- [Web](#web)
    - [Authentication, Authorization](#authentication-authorization)
    - [APIs](#apis)
    - [HTTP Client](#http-client)
    - [Websockets](#websockets)

- [Other](#other)
    - [Archives](#archives)
    - [Templates](#templates)
    - [Tools](#tools)
    - [Other](#other)


## Packages

### Basic

#### Console

- [pflag](https://github.com/spf13/pflag) is a simple library for parsing CLI args, just like standard library, but POSIX/GNU-style.
- [cobra](https://github.com/spf13/cobra) is a powerful library for making modern CLI interfaces like `kubectl` or `docker`.  Supports subcommands, cascading flags, suggestions, shell autocompletions and many more.



#### Data Serialization

- [encoding/json](https://pkg.go.dev/encoding/json) from standard library for JSON
- [easyjson](https://github.com/mailru/easyjson) for faster JSON, but it requires code generation
- [yaml](https://github.com/go-yaml/yaml) for YAML
- [go-toml](https://github.com/pelletier/go-toml) and [toml](https://github.com/BurntSushi/toml) for TOML are good


#### Dependency Injection

Do not use libraries for that.


#### Error Handling

Use standard library.


#### Logging

Structured logging:

- [zerolog](https://github.com/rs/zerolog) — fast, popular, user-friendly, flexible.
- [zap](https://github.com/uber-go/zap) is popular too, very fast, but slower than zerolog.
- [log/slog](https://pkg.go.dev/log/slog) from standard library (since Go 1.21).  Good choice if you don't want to introduce any third-party dependencies.


#### Testing

- [testify](https://github.com/stretchr/testify) provices a lot of well-designed syntactic sugar that the standard library lacks.
- [moq](https://github.com/matryer/moq) for generating mock structures from interfaces.


### Server Side

#### Databases

SQL databases drivers:

- [pgx](https://github.com/jackc/pgx) is a driver and toolkit for PostgreSQL.  Do not use `database/sql` interface (it's slower and supports fewer features) if you do not have specific reasons to do so.
- [go-sqlite3](https://github.com/mattn/go-sqlite3) for SQLite. It requires CGO, it should not be a problem generally, but if you want to avoid it, there is [sqlite](https://gitlab.com/cznic/sqlite) package, but it's much less popular.
- [mysql](https://github.com/go-sql-driver/mysql)
- more drivers for `database/sql` interface on the [official wiki](https://go.dev/wiki/SQLDrivers)

NoSQL:

- [mongo-go-driver](https://github.com/mongodb/mongo-go-driver)
- [go-redis](https://github.com/redis/go-redis)

Message brokers, queues, events:

- [kafka-go](https://github.com/segmentio/kafka-go)
- [amqp091-go](github.com/rabbitmq/amqp091-go) for RabbitMQ (maintained by the RabbitMQ team)
- for ZeroMQ: [pebbe/zmq4](https://github.com/pebbe/zmq4) (wrapper for libzmq, requires cgo, cannot be cross-compiled), [go-zeromq/zmq4](https://github.com/go-zeromq/zmq4) (pure Go library, unclear development status)

Useful SQL utilities:

- [sqlx](https://github.com/jmoiron/sqlx) to work convenient with structs (uses `database/sql` interface)
- [squirrel](https://github.com/Masterminds/squirrel) to generate SQL queries (for example, when your app supports filtering and you need to build a `WHERE` clause dynamically)


#### HTTP Server

No need for frameworks, use standard library.

For URL routing:
- [net/http.ServeMux](https://pkg.go.dev/net/http#ServeMux) from standard library is good enough
- [httprouter](https://github.com/julienschmidt/httprouter) is more powerful, supports parameters like `/post/:id` and many more
- [chi](https://github.com/go-chi/chi) even more powerful, still lightweight


#### OpenAPI

- TODO

### Web

#### Authentication, Authorization

- [jwt](https://github.com/golang-jwt/jwt) for JWT
- [x/oauth](https://pkg.go.dev/golang.org/x/oauth2) for OAuth 2.0 clients, supports popular providers
- [go-oidc](https://github.com/coreos/go-oidc) for OpenID Connect


#### APIs

- [google-api-go-client](https://github.com/googleapis/google-api-go-client)
- [go-github](https://github.com/google/go-github)
- [facebook](https://github.com/huandu/facebook)
- [twitter](https://github.com/dghubble/go-twitter)
- [telegram-bot-api](https://github.com/go-telegram-bot-api/telegram-bot-api)


#### HTTP Client

- [net/http](https://pkg.go.dev/net/http) from standard library
- [requests](https://github.com/earthboundkid/requests) for syntactic sugar

#### Websockets

- [gorilla/websocket](https://github.com/gorilla/websocket)


### Other

#### Archives and Compression

Archives:

- [archive/zip](https://pkg.go.dev/archive/zip) from standard library
- [archive/tar](https://pkg.go.dev/archive/tar) from standard library

Compression and decompression:

- [xz](https://github.com/ulikunitz/xz)
- [compress/bzip2](https://pkg.go.dev/compress/bzip2) from standard library for decompression, and [dsnet/compress/bzip2](https://github.com/dsnet/compress) if you need compression too.
- [compress/gzip](https://pkg.go.dev/compress/gzip) from standard library


#### Templates

- [text/template](https://pkg.go.dev/text/template) and [html/template](https://pkg.go.dev/html/template) from standard library


#### Tools

- [golangci-lint](https://github.com/golangci/golangci-lint) for linters.
- [goimports](https://pkg.go.dev/golang.org/x/tools/cmd/goimports) for sorting imports.  It should already be integrated in your IDE.


#### Other

- [uuid](https://github.com/google/uuid)

- [viper](https://github.com/spf13/viper) — configuration management, to load configuration from many sources (CLI args, environment variables, JSON/TOML/etc files, remote stores like etcd/Consul)
