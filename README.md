# {{ .Name }}

{{ .Name }} is a simple example of a production ready RPC service in Go. Instead of attempting to abstract away the details of bootstrapping a new service like `kit`, this is meant to be used as a blueprint of how to piece together various libraries.

# Libraries

- [conf](https://github.com/segmentio/conf): Loading program configuration from multiple sources.
- [events](https://github.com/segmentio/events): Handles routing, formatting and publishing logs.
- [stats](https://github.com/segmentio/stats): Handles routing, formatting and publishing stats.
- [rpc](https://github.com/segmentio/rpc): jsonrpc v2 server (and client) that integrates with `events` and `stats`.
- [alice](https://github.com/justinas/alice): HTTP middleware chaining used for HTTP stats and logs.
- [assert](https://github.com/stretchr/testify#assert-package): Assertion helper methods for testing.

# Tools

- [Trebuchet](https://github.com/segmentio/trebuchet): For deploying our service.
- [Docker](https://www.docker.com/): To package and ship our application.

# Get started

```
# Ensure your GOPATH is configured correctly.
# https://github.com/golang/go/wiki/SettingGOPATH
go get github.com/segmentio/{{ .Name }}
cd $GOPATH/src/github.com/{{ .Org }}/{{ .Name }}
make test
```

# Running {{ .Name }}

After completing the [Get Started](#get-started) section follow these steps for running the `{{ .Name }}` rpc server

To execute rpc for `HelloWorld.HelloWorld`

```shell
# In console window 1
make run
```

To execute rpc for `HelloWorld.Hello`

```shell
# In console window 2
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{"jsonrpc": "2.0", "method": "HelloWorld.Hello", "params": "prateek", "id": "foo"}' \
http://localhost:3000/rpc
```

# Layout

The general layout of this repository is as follows:

```
.
├── .run # trebuchet configuration
├── .buildkite # buildkite configuration
├── cmd # binaries produced by the repo
│   └── service
└── internal # internal packages only meant for use in this repository. public packages should live in the root directory.
    └── hellow
```

# Generation Note

This repo was automatically generated from the [go service template](https://github.com/segmentio/go-service-template). If you would like to create your own repo, you can use:

```
robo init-repo
```
