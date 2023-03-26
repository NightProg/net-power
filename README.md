# Net Power

## What is it?

Net Power is a simple tool written in Rust that allows you to make complex calculations in servers configured to reduce
the use of your computer's ram

## How to use it?

### Installation

To install Net Power, you must have Rust installed on your computer. If you don't have it, you can install it by
following the instructions on the [Rust website](https://www.rust-lang.org/tools/install).

Once you have Rust installed, you can install Net Power by running the following command:

```bash
cargo install net-power
```

## The server

To use Net Power, you must have a server running.

### With your computer

To start the server, you can run the following command:

```bash
net-power new-server localhost:8080
```

if you want to use a different port, you can change the port number in the command.

### With a remote server

The server can be run on a remote server. To do this, you must have a server with a public IP address, a port open and a
key. Once you have the server, you can run the following command:

```bash
net-power configure-server <ip address>:<port> -k <key>
```

The key must be the same as the one used to start the server.

DON'T SHARE YOUR KEY WITH ANYONE

## The client

### With a terminal

To use Net Power with a terminal, you can run the following command:

```bash
net-power new-client localhost:8080
```

if you want to use a different port, you can change the port number in the command.

### With JSON

To use Net Power with JSON, you can run the following command:

```bash
net-power new-client localhost:8080 -j <json>
```

change `<json>` for the json you want to use.

#### JSON format

the json must have the following format:

```json
{
  "name": "<name>",
  variables: {
    "<variable name>": "<variable value>"
  },
  calculations: [
    {
      "name": "<calculation name>",
      "expression": "<calculation expression>"
    }
  ]
}
```

change `<name>` for the name of the calculation.

change `<variable name>` for the name of the variable.

change `<variable value>` for the value of the variable.

change `<calculation name>` for the name of the calculation.

change `<calculation expression>` for the expression of the calculation.

#### Example

```json
{
  "name": "example",
  variables: {
    "a": "2",
    "b": "2"
  },
  calculations: [
    {
      "name": "sum",
      "expression": "a+b"
    }
  ]
}
```

the result will be:

```json
{
  "sum": "4"
}
```

### If you want to use it in your code

To use Net Power in your code, you can add the following line to your Cargo.toml file:

```toml
net-power = "0.1.0"
```

Once you have added the line, you can use Net Power in your code by adding the following line:

```rust
use net_power::client::Client;
```

#### The Client API

The Client API is very simple. To use it, you must create a new client with the following line:

```rust
use net_power::client::Client;
let client = Client::new("localhost:8080");
```

to send a request to the server, you can use the following line:

```rust
use net_power::client::Client;
let client = Client::new("localhost:8080");
let result = client.send_request("2+2");
```

The result will be a `Result<String, Error>` type. If the request was successful, the result will be `Ok(String)`, and
if it was not, the result will be `Err(Error)`.

you can also use the `send_request_with_key` function to send a request with a key. This function has the following
signature:

```rust
use net_power::client::Client;
let client = Client::new("<ip-address>:<host>");
let result = client.send_request_with_key("<key>", "2+2");
```

change `<key>` for the key you want to use.

change `<ip-address>` for the ip address of the server.

change `<host>` for the port of the server.

## The server API

The server API is very simple. To use it, you must create a new server with the following line:

```rust
use net_power::server::Server;
let server = Server::new("localhost:8080");
```

if you want to use a different port, you can change the port number in the command.
if you want to use a key, you can use the following line:

```rust
use net_power::server::Server;

let server = Server::new_with_key("localhost:8080", "my-key");
```

change `my-key` for the key you want to use.

to start the server, you can use the following line:

```rust
use net_power::server::Server;
let server = Server::new("localhost:8080");
server.start();
```

if you want to configure the server to use less ram, you can use the following line:

```rust
use net_power::server::Server;
let server = Server::new("localhost:8080");
server.start_with_less_ram();
```

if you want to configure a server existing in a remote server, you can use the following line:

```rust
use net_power::server::Server;
use net_power::server::RemoteServer;
let server = RemoteServer::new("yoursite.com").unwrap();
server.setup();
server.start();
```

change `yoursite.com` for the ip address of the server.











