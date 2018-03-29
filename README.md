⚠ NOT YET IMPLEMENTED ⚠

# `wbgvm`

The `wasm-bindgen` virtual machine.

Consumes WebIDL and TypeScript definition files and emits `wasm-bindgen` `extern
type` and `extern fn` declarations.

## Architecture

### Frontends

There are two frontends:

1. TypeScript
2. WebIDL

Despite parsing and munging different input languages, both frontends translate
the input into the same IR.

#### TypeScript Frontend

Written in TypeScript and uses the TypeScript compiler API to parse `.d.ts`
definition files and emit the IR as JSON. This TypeScript frontend is run as a
subprocess.

https://github.com/Microsoft/TypeScript/wiki/Using-the-Compiler-API

#### WebIDL Frontend

This is pure Rust. We use the `webidl` crate to parse WebIDL interface
definitions and translate them into our IR.

### Intermediate Representation (IR)

The IR has a well-defined JSON encoding. It can describe any `wasm-bindgen`
extern declaration.

### Code Generation

The code generation serves as the shared backend for `wbgvm`. It takes the IR
and translates it into Rust source text defining `#[wasm_bindgen]` declarations.
