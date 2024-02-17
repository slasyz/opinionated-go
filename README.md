# Opinionated Go

This is my curated list of Go packages.

Unlike [awesome-go](https://github.com/avelino/awesome-go), which is a very comprehensive list of Go packages, this list is opinionated and contains only a subset of packages that I find good to start with. Inspired by [blessed.rs/crates](https://blessed.rs/crates).

The purpose of this list is to provide a selection of go-to options for basic needs when there are no specific requirements.

If you have any feedback, feel free to reach out to me directly.


## Contents

- [Basic](#basic)
    - [Console](#console)
    - [Data Serialization](#data-serialization)
    - [Dependency Injection](#dependency-injection)
    - [Errors Handling](#errors-handling)
    - [Logging](#logging)
    - [Testing](#testing)

- [Web](#web)
    - [APIs](#apis)
    - [Authentication and Authorization](#authentication-and-authorization)
    - [Databases](#databases)
    - [HTTP Client](#http-client)
    - [HTTP Server](#http-server)
    - [OpenAPI](#openapi)
    - [Websockets](#websockets)

- [Other](#other)
    - [AI](#ai)
    - [Archives](#archives)
    - [GUI](#gui)
    - [Templates](#templates)
    - [Tools](#tools)
    - [Utilities](#utilities)


## Packages

### Basic

#### Console

- [pflag](https://github.com/spf13/pflag) is a simple library for parsing CLI args, just like [flag](https://pkg.go.dev/flag) from standard library, but uses POSIX/GNU-style `--flags` instead of `-flags`.
- [cobra](https://github.com/spf13/cobra) is a powerful library for creating modern command-line interfaces like `kubectl` or `docker`.  It supports subcommands, cascading flags, suggestions, shell autocompletions, and many more.
- [viper](https://github.com/spf13/viper) to load configuration from many sources (CLI args, environment variables, JSON/TOML/etc files, remote stores like etcd/Consul)

TUI:

- [go-prompt](https://github.com/c-bata/go-prompt) is a library for building powerful interactive prompts
- [huh](https://github.com/charmbracelet/huh) is a simple yet powerful library for building interactive forms and prompts in the terminal
- [bubletea](https://github.com/charmbracelet/bubbletea) is a framework for building terminal UIs
- for more libraries and components for glamorous console interfaces, see [charm.sh](https://charm.sh/)


#### Data Serialization

- [encoding/json](https://pkg.go.dev/encoding/json) from standard library for JSON
- [easyjson](https://github.com/mailru/easyjson) for faster JSON, but it requires code generation
- [yaml](https://github.com/go-yaml/yaml) for YAML
- [go-toml](https://github.com/pelletier/go-toml) and [toml](https://github.com/BurntSushi/toml) for TOML


#### Dependency Injection

Do not use libraries for that.


#### Errors Handling

- [errors](https://pkg.go.dev/errors) from standard library


#### Logging

Structured logging:

- [zerolog](https://github.com/rs/zerolog) — fast, popular, user-friendly, flexible
- [zap](https://github.com/uber-go/zap) is a good option too, popular, very fast, but slower than zerolog
- [log/slog](https://pkg.go.dev/log/slog) from standard library (since Go 1.21).  Good choice if you don't want to introduce any third-party dependencies.


#### Testing

- [testify](https://github.com/stretchr/testify) provides a lot of well-designed syntactic sugar that the standard library lacks
- [moq](https://github.com/matryer/moq) for generating mock structures from interfaces


### Web

#### APIs

- [google-api-go-client](https://github.com/googleapis/google-api-go-client) for Google
- [go-github](https://github.com/google/go-github) for GitHub
- [facebook](https://github.com/huandu/facebook) for Facebook
- [twitter](https://github.com/dghubble/go-twitter) for Twitter
- [telegram-bot-api](https://github.com/go-telegram-bot-api/telegram-bot-api) for Telegram


#### Authentication and Authorization

- [jwt](https://github.com/golang-jwt/jwt) for JWT
- [x/oauth](https://pkg.go.dev/golang.org/x/oauth2) for OAuth 2.0 clients, supports popular providers
- [go-oidc](https://github.com/coreos/go-oidc) for OpenID Connect


#### Databases

Clients for SQL databases:

- [pgx](https://github.com/jackc/pgx) for PostgreSQL.  Use this driver directly instead of `database/sql` interface (because it is faster and supports more features) unless you do not have specific reasons to do so.
- [go-sqlite3](https://github.com/mattn/go-sqlite3) for SQLite. It requires `cgo`, it should not be a problem generally, but if you want to avoid it, there is [sqlite](https://gitlab.com/cznic/sqlite) package, but it's much less popular.
- [mysql](https://github.com/go-sql-driver/mysql) for MySQL
- more drivers for `database/sql` interface on the [official wiki](https://go.dev/wiki/SQLDrivers)

Clients for NoSQL databases:

- [mongo-go-driver](https://github.com/mongodb/mongo-go-driver) for Mongo
- [go-redis](https://github.com/redis/go-redis) for Redis

Clients for message brokers, queues, event systems:

- [kafka-go](https://github.com/segmentio/kafka-go) for Kafka
- [amqp091-go](github.com/rabbitmq/amqp091-go) for RabbitMQ (maintained by the RabbitMQ team)
- for ZeroMQ there are [pebbe/zmq4](https://github.com/pebbe/zmq4) (wrapper for `libzmq`, requires `cgo`, cannot be cross-compiled) and [go-zeromq/zmq4](https://github.com/go-zeromq/zmq4) (pure Go library, unclear development status).

SQL utilities:

- [sqlx](https://github.com/jmoiron/sqlx) to work conveniently with structs (uses `database/sql` interface)
- [squirrel](https://github.com/Masterminds/squirrel) to generate SQL queries (for example, when your app supports filtering and you need to build a `WHERE` clause dynamically)
- [goose](https://github.com/pressly/goose) for SQL migrations, supports both text-based SQL migrations and Go functions


#### HTTP Client

- [net/http](https://pkg.go.dev/net/http) from standard library
- [requests](https://github.com/earthboundkid/requests) for syntactic sugar


#### HTTP Server

No need for frameworks, use standard library.

For URL routing:

- [net/http.ServeMux](https://pkg.go.dev/net/http#ServeMux) from standard library is good enough
- [httprouter](https://github.com/julienschmidt/httprouter) is more powerful, very fast, supports parameters like `/post/:id` and many more. Not actively developed right now, but widely adopted.
- [chi](https://github.com/go-chi/chi) is powerful and lightweight too, has even more features


#### OpenAPI

- [oapi-codegen](https://github.com/deepmap/oapi-codegen) to generate Go boilerplate code from an OpenAPI 3.0 specification file
- [swag](https://github.com/swaggo/swag) to generate Swagger 2.0 specification from Go code annotations


#### Websockets

- [gorilla/websocket](https://github.com/gorilla/websocket) for both server and client


### Other

#### AI

- [langchaingo](https://github.com/tmc/langchaingo) to build LLM-powered apps


#### Archives and Compression

Archives:

- [archive/zip](https://pkg.go.dev/archive/zip) from standard library
- [archive/tar](https://pkg.go.dev/archive/tar) from standard library

Compression and decompression:

- [xz](https://github.com/ulikunitz/xz)
- [compress/bzip2](https://pkg.go.dev/compress/bzip2) from standard library for decompression, and [dsnet/compress/bzip2](https://github.com/dsnet/compress) if you need compression too
- [compress/gzip](https://pkg.go.dev/compress/gzip) from standard library


#### GUI

Besides obvious GTK and Qt bindings:

- [gio](https://gioui.org/) — lightweight immediate mode GUI library


#### Templates

- [text/template](https://pkg.go.dev/text/template) and [html/template](https://pkg.go.dev/html/template) from standard library


#### Tools

- [golangci-lint](https://github.com/golangci/golangci-lint) for linters
- [goimports](https://pkg.go.dev/golang.org/x/tools/cmd/goimports) for sorting imports and formatting code


#### Utilities

- [uuid](https://github.com/google/uuid) to work with UUIDs
- [date](https://github.com/rickb777/date) to work with dates
