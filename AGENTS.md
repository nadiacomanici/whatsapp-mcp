# Repo Guide

This repository contains a WhatsApp Model Context Protocol implementation. The code is split into two
main directories:

- **whatsapp-bridge** – Go application built with the whatsmeow library. It connects to WhatsApp Web,
  stores messages in a SQLite database and exposes a small HTTP API used by the MCP server.
- **whatsapp-mcp-server** – Python implementation of a FastMCP server which exposes tools for Claude or
  Cursor. It queries the bridge HTTP API and the database to perform actions like searching messages or
  sending content.

## Running
1. Run the Go bridge in `whatsapp-bridge/` with `go run main.go`. The first run will ask you to scan a QR
   code. The bridge also starts an HTTP server on port `8080` for the MCP server.
2. Run the MCP server in `whatsapp-mcp-server/` using `uv run main.py` or `python main.py`.

## Development Notes
- The MCP tools live in `whatsapp-mcp-server/main.py`. Each tool calls helper functions in
  `whatsapp-mcp-server/whatsapp.py`.
- The Go bridge exposes its functionality over HTTP from `startRESTServer` in `whatsapp-bridge/main.go`.
- Group management endpoints are implemented under paths like `/api/create_group` and are wrapped by
  Python helper functions (`create_group`, `join_group_with_link`, ...).

Feel free to extend the project with additional WhatsApp features following the existing pattern.

