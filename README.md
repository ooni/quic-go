# A QUIC implementation in pure Go

**Note**: this repository is a temporary fork of
[lucas-clemente/quic-go](https://github.com/lucas-clemente/quic-go) to experiment
with and figure out our needs in terms of mapping an http3 request with the five tuple
used by the underlying http3 connection. We described this experiment in the
[ooni/probe#2220](https://github.com/ooni/probe/issues/2220) issue. The general
plan here is to understand what we exactly need and then see whether it's possible
to upstream the changes.

We started this fork at lucas-clemente/quic-go@v0.27.0. We're not going to publish
all the upstream tags for simplicity. When merging from upstream, we'll clarify which
tags we're merging.

(You should not depend on this repository! As mentioned, this is an experiment and
we may archive this repository anytime soon!)

- - -

<img src="docs/quic.png" width=303 height=124>

[![PkgGoDev](https://pkg.go.dev/badge/github.com/lucas-clemente/quic-go)](https://pkg.go.dev/github.com/lucas-clemente/quic-go)
[![Code Coverage](https://img.shields.io/codecov/c/github/lucas-clemente/quic-go/master.svg?style=flat-square)](https://codecov.io/gh/lucas-clemente/quic-go/)

quic-go is an implementation of the [QUIC protocol, RFC 9000](https://datatracker.ietf.org/doc/html/rfc9000) protocol in Go.
In addition to RFC 9000, it currently implements the [IETF QUIC draft-29](https://tools.ietf.org/html/draft-ietf-quic-transport-29). Support for draft-29 will eventually be dropped, as it is phased out of the ecosystem.

## Guides

*We currently support Go 1.16.x, Go 1.17.x, and Go 1.18.x.*

Running tests:

    go test ./...

### QUIC without HTTP/3

Take a look at [this echo example](example/echo/echo.go).

## Usage

### As a server

See the [example server](example/main.go). Starting a QUIC server is very similar to the standard lib http in go:

```go
http.Handle("/", http.FileServer(http.Dir(wwwDir)))
http3.ListenAndServeQUIC("localhost:4242", "/path/to/cert/chain.pem", "/path/to/privkey.pem", nil)
```

### As a client

See the [example client](example/client/main.go). Use a `http3.RoundTripper` as a `Transport` in a `http.Client`.

```go
http.Client{
  Transport: &http3.RoundTripper{},
}
```

## Projects using quic-go

| Project                                              | Description                                                                                            | Stars |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|-------|
| [algernon](https://github.com/xyproto/algernon)      | Small self-contained pure-Go web server with Lua, Markdown, HTTP/2, QUIC, Redis and PostgreSQL support | ![GitHub Repo stars](https://img.shields.io/github/stars/xyproto/algernon?style=flat-square) |
| [caddy](https://github.com/caddyserver/caddy/)       | Fast, multi-platform web server with automatic HTTPS                                                   | ![GitHub Repo stars](https://img.shields.io/github/stars/caddyserver/caddy?style=flat-square) |
| [go-ipfs](https://github.com/ipfs/go-ipfs)           | IPFS implementation in go                                                                              | ![GitHub Repo stars](https://img.shields.io/github/stars/ipfs/go-ipfs?style=flat-square) |
| [syncthing](https://github.com/syncthing/syncthing/) | Open Source Continuous File Synchronization                                                            | ![GitHub Repo stars](https://img.shields.io/github/stars/syncthing/syncthing?style=flat-square) |
| [traefik](https://github.com/traefik/traefik)        | The Cloud Native Application Proxy                                                                     | ![GitHub Repo stars](https://img.shields.io/github/stars/traefik/traefik?style=flat-square) |
| [v2ray-core](https://github.com/v2fly/v2ray-core)    | A platform for building proxies to bypass network restrictions                                         | ![GitHub Repo stars](https://img.shields.io/github/stars/v2fly/v2ray-core?style=flat-square) |
| [cloudflared](https://github.com/cloudflare/cloudflared)    | A tunneling daemon that proxies traffic from the Cloudflare network to your origins             | ![GitHub Repo stars](https://img.shields.io/github/stars/cloudflare/cloudflared?style=flat-square) |
| [OONI Probe](https://github.com/ooni/probe-cli)            | The Open Observatory of Network Interference (OONI) aims to empower decentralized efforts in documenting Internet censorship around the world.   | ![GitHub Repo stars](https://img.shields.io/github/stars/ooni/probe-cli?style=flat-square) |


## Contributing

We are always happy to welcome new contributors! We have a number of self-contained issues that are suitable for first-time contributors, they are tagged with [help wanted](https://github.com/lucas-clemente/quic-go/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22). If you have any questions, please feel free to reach out by opening an issue or leaving a comment.
