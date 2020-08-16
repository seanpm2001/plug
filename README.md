# Gleam Plug! 🔌

A Gleam HTTP service adapter for the Plug web application interface.

## Usage

Define a Gleam HTTP service

```rust
import gleam/http
import gleam/bit_builder.{BitBuilder}

pub fn service(req: http.Request(BitBuilder)) {
  http.response(200)
  |> http.prepend_resp_header("made-with", "Gleam")
  |> http.set_resp_body(req.body)
}
```

And then call it from an Elixir Plug application

```elixir
defmodule MyPlug do
  def init(options) do
    options
  end

  def call(conn, params) do
    conn
    |> GleamPlug.conn_to_request(params)
    |> :my_gleam_module.service(req)
    |> GleamPlug.send(conn)
  end
end
```

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `gleam_plug` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:gleam_plug, "~> 0.1.0"}
  ]
end
```

Documentation can be generated with [ExDoc](https://github.com/elixir-lang/ex_doc)
and published on [HexDocs](https://hexdocs.pm). Once published, the docs can
be found at [https://hexdocs.pm/gleam_plug](https://hexdocs.pm/gleam_plug).
