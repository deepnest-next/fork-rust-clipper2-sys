# Building clipper2-sys

`build.rs` compiles Clipper2 (C++) and the `clipper2c` C wrapper with the `cc` crate. The
Rust bindings are pre-generated in `generated/`, so the default build does **not** need
libclang.

## External dependencies

| Needed for | What | Debian/Ubuntu | Fedora | Alpine | macOS | Windows |
|---|---|---|---|---|---|---|
| Sources | git submodules (`clipper2c`, inside it `vendor/Clipper2`) | `git submodule update --init --recursive` | | | | |
| Every build | Rust toolchain + C++17 compiler | `build-essential` | `gcc-c++` | `build-base` (build.rs adds the musl C++ include paths) | Xcode Command Line Tools | MSVC Build Tools |
| `--features generate-bindings` / `update-bindings` (regenerate `generated/`) | clang + libclang (bindgen) | `clang libclang-dev` | `clang clang-devel` | `clang-dev` | Xcode Command Line Tools | LLVM (`winget install LLVM.LLVM`), set `LIBCLANG_PATH` |

## Build

```bash
git submodule update --init --recursive
cargo build
cargo test
cargo build --features update-bindings   # only after updating Clipper2 or bindgen
```
