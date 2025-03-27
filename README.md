# GoRedis

## Overview

GoRedis is a lightweight, high-performance in-memory data store written in Go, inspired by Redis. This project implements a thread-safe key-value storage system with network communication capabilities, supporting both client-server and peer-to-peer architectures.

## Features

- **In-Memory Key-Value Store**: Fast, thread-safe storage for any type of data
- **Networked Server**: TCP-based server that handles concurrent client connections
- **Simple Protocol**: Implementation of a Redis-like protocol for client-server communication
- **Peer-to-Peer Networking**: Support for data distribution and replication across multiple nodes
- **Concurrency**: Efficient handling of simultaneous operations using Go's goroutines and mutexes
- **Data Persistence**: Optional periodic snapshots to disk for data durability
- **Comprehensive Testing**: Thorough unit and integration tests ensuring reliability

## Installation

### Prerequisites

- Go 1.16 or higher
- Git

### Steps

```bash
# Clone the repository
git clone https://github.com/yourusername/goredis.git

# Navigate to the project directory
cd goredis

# Build the project
go build -o goredis cmd/server/main.go

# Run the server
./goredis
```

## Usage

### Starting the Server

```bash
# Start with default configuration (port 6379)
./goredis

# Start with custom port
./goredis -port 7000

# Start with persistence enabled
./goredis -persist -dbfile data.db
```

### Client Connection Examples

#### Using the CLI Client

```bash
# Connect to the server
go run cmd/client/main.go -addr localhost:6379

# Inside the client
> SET user:1 "John Doe"
OK
> GET user:1
"John Doe"
> DEL user:1
(integer) 1
```

#### Programmatic Usage

```go
package main

import (
	"fmt"
	"goredis/client"
)

func main() {
	// Create a client
	c, err := client.New("localhost:6379")
	if err != nil {
		panic(err)
	}
	defer c.Close()

	// Set a key
	err = c.Set("counter", "1")
	if err != nil {
		panic(err)
	}

	// Get a key
	value, err := c.Get("counter")
	if err != nil {
		panic(err)
	}
	fmt.Println("Counter value:", value)

	// Increment a counter
	newValue, err := c.Incr("counter")
	if err != nil {
		panic(err)
	}
	fmt.Println("New counter value:", newValue)
}
```

### Supported Commands

| Command | Description | Example |
|---------|-------------|---------|
| SET | Set key to value | `SET key value` |
| GET | Get value by key | `GET key` |
| DEL | Delete a key | `DEL key` |
| EXISTS | Check if key exists | `EXISTS key` |
| INCR | Increment value | `INCR counter` |
| DECR | Decrement value | `DECR counter` |
| EXPIRE | Set key expiration | `EXPIRE key seconds` |
| TTL | Get key time-to-live | `TTL key` |
| PING | Test connection | `PING` |
| INFO | Server information | `INFO` |

## Architecture

GoRedis follows a modular architecture with the following key components:

1. **Storage Engine**: Thread-safe in-memory store with support for different data types
2. **Network Layer**: TCP server handling client connections and protocol parsing
3. **Command Processor**: Processes commands and interacts with the storage engine
4. **Peer Communication**: Handles node-to-node communication for distributed setups
5. **Persistence Manager**: Provides snapshotting capability for data durability

### Concurrency Model

The system uses Go's concurrency primitives to ensure thread safety:
- Read-write mutexes protect the key-value store
- Each client connection is handled in a separate goroutine
- Channel-based communication coordinates system-wide operations

## Performance

GoRedis is designed for high performance:
- Low memory footprint
- Efficient data structures for different use cases
- Optimized for high throughput and low latency
