#Simple Database like Redis using Go,implementation of a Redis-like in-memory data store written in Go. 

#This project provides key-value storage functionality and includes features like server-client communication, peer-to-peer networking, and basic CRUD operations. 

#It mimics the behavior of Redis with basic components such as a key-value store, server processes, and network communication.


#Core Features Summary:
In-Memory Key-Value Store: The project implements a thread-safe in-memory store for key-value pairs.

Networked Server: The application listens for client commands over a TCP connection and processes requests concurrently using Go’s goroutines.

Protocol Support: Implements a simple protocol for client-server communication, likely mimicking Redis’s RESP.

Peer-to-Peer Communication: Includes support for distributing data across nodes or replicating it, potentially allowing for a multi-node setup.

Concurrency: The project leverages Go’s concurrency primitives (goroutines and mutexes) to ensure high performance and safe access to shared resources.

Testing: The project includes unit and integration tests to validate its functionality.
