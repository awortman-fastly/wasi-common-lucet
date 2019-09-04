# WASI-common wrappers for Lucet

A crate to use the [reference WASI implementation](https://github.com/CraneStation/wasi-common/) in WebAssembly modules run with [Lucet](https://github.com/fastly/lucet).

- Call `wasi_common_lucet::export_wasi_funcs()` once in order to have the symbols exported
- Create a new isntance with `WasiCtx::new()`. Note that the function signature slightly differs from the `lucet-wasi` one.
- Register it into Lucet instances using `insert_embed_ctx()`.

```rust
use wasi_common_lucet::WasiCtx;

fn doit() -> Result <(), Error> {
    wasi_common_lucet::export_wasi_funcs();
    // ...
    let mut lucet_instance_handle = lucet_dylib.instantiate(region)?;
    let wasi_ctx: WasiCtx = WasiCtx::new(["app"].iter())?;
    lucet_instance_handle.insert_embed_ctx(wasi_ctx);
    // ...
}
```
