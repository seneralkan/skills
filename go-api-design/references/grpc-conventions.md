# gRPC Conventions

## Service design
- Use clear RPC naming: `Get`, `List`, `Create`, `Update`, `Delete`.
- Prefer separate request/response message types per RPC.

## Compatibility
- Never reuse field numbers.
- Reserve removed fields.
- Add fields as optional/default-safe.

## Status mapping
- Use canonical gRPC status codes consistently.
- Attach machine-readable error details for clients.
