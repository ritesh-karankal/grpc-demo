# Go gRPC Server and Client

A simple Go project demonstrating all four types of gRPC communication using Protocol Buffers.

This project is based on the official gRPC Go tutorials and is intended as a beginner-friendly reference for learning gRPC in Go.

## Features

- Unary RPC
- Server Streaming RPC
- Client Streaming RPC
- Bidirectional Streaming RPC

## Project Structure

```text
.
├── client/
│   ├── main.go
│   ├── unary.go
│   ├── server_stream.go
│   ├── client_stream.go
│   └── bidirectional_stream.go
├── server/
│   ├── main.go
│   ├── unary.go
│   ├── server_stream.go
│   ├── client_stream.go
│   └── bidirectional_stream.go
├── proto/
│   ├── greet.proto
│   ├── greet.pb.go
│   └── greet_grpc.pb.go
├── go.mod
├── go.sum
└── README.md
```

## Prerequisites

- Go 1.22 or later
- Protocol Buffers Compiler (`protoc`)
- Git

Verify the installations:

```bash
go version
protoc --version
```

---

# Getting Started

## 1. Clone the repository

```bash
git clone https://github.com/ritesh-karankal/grpc-demo.git

cd basic-go-grpc
```

## 2. Install the Go plugins

```bash
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest

go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
```

Add the Go binaries to your PATH if they are not already available.

Linux/macOS:

```bash
export PATH="$PATH:$(go env GOPATH)/bin"
```

Verify:

```bash
protoc-gen-go --version

protoc-gen-go-grpc --version
```

## 3. Install project dependencies

```bash
go mod tidy
```

---

# Generate Go Files

Create your `proto/greet.proto` file.

If your proto file contains:

```proto
option go_package = "./proto";
```

generate the files using:

```bash
protoc --go_out=. --go-grpc_out=. proto/greet.proto
```

If your proto file instead contains a Go module path such as:

```proto
option go_package = "github.com/your-username/basic-go-grpc/proto";
```

generate the files using:

```bash
protoc \
  --go_out=. \
  --go_opt=module=github.com/your-username/basic-go-grpc \
  --go-grpc_out=. \
  --go-grpc_opt=module=github.com/your-username/basic-go-grpc \
  proto/greet.proto
```

---

# Running the Application

## Start the server

```bash
go run server/*.go
```

The server should start on:

```
localhost:8080
```

## Run the client

```bash
go run client/*.go
```

---

# Available RPC Examples

## Unary RPC

Client sends one request and receives one response.

```
Client -------> Server
        Request

Client <------- Server
        Response
```

---

## Server Streaming RPC

Client sends one request and receives multiple responses.

```
Client -------> Server
        Request

Client <------- Server
        Response 1

Client <------- Server
        Response 2

Client <------- Server
        Response 3
```

---

## Client Streaming RPC

Client sends multiple requests and receives one response.

```
Client -------> Server
        Request 1

Client -------> Server
        Request 2

Client -------> Server
        Request 3

Client <------- Server
        Response
```

---

## Bidirectional Streaming RPC

Client and server both send messages simultaneously.

```
Client -------> Server
        Request 1

Client <------- Server
        Response 1

Client -------> Server
        Request 2

Client <------- Server
        Response 2
```

---

# Switching Between Examples

In `client/main.go`, uncomment the RPC you want to test.

```go
callSayHello(client)

// callSayHelloServerStream(client, names)

// callSayHelloClientStream(client, names)

// callSayHelloBidirectionalStream(client, names)
```

Run the client again after changing the function.

---

# Technologies Used

- Go
- gRPC
- Protocol Buffers (protobuf)

---

# Learning Resources

- https://grpc.io/docs/languages/go/
- https://grpc.io/docs/what-is-grpc/
- https://protobuf.dev/

---
