# How to Hack the Rust Standard Library Using Nightly + Cargo

This guide explains how to safely modify and run the Rust Standard Library (`std`) for experiments, using the nightly toolchain and `cargo -Zbuild-std`.

---

## 🛠️ Preparation

### Install Nightly Toolchain
```bash
rustup install nightly
```

### Set Nightly for Your Project
```bash
rustup override set nightly
```

### Install Rust Source Code
```bash
rustup component add rust-src --toolchain nightly
```

✅ This installs the standard library source code at:

```
~/.rustup/toolchains/nightly-x86_64-unknown-linux-gnu/lib/rustlib/src/rust/library/
```

---

## 🖋️ Modify the Standard Library

Navigate to the stdlib source:

```bash
cd ~/.rustup/toolchains/nightly-x86_64-unknown-linux-gnu/lib/rustlib/src/rust/library/std/src
```

Edit files like:
- `fs/mod.rs` (for file system functions)
- `io/mod.rs` (for I/O operations)

Add your custom `println!()` or any modifications.

✅ Save your changes.

---

## 📚 Create a Test Project

```bash
cargo new my-std-test
cd my-std-test
```

Edit `src/main.rs` to call functions that you modified, e.g., using `fs::read()`.

---

## ⚖️ Build and Run with Modified Standard Library

Run with:

```bash
cargo run -Zbuild-std
```

✅ Cargo will:
- Rebuild `core`, `alloc`, `std` from the modified sources.
- Compile your project linked against your modified `std`.

✅ Your custom `println!()` will appear during runtime!

---

## ⚠️ Important Commands to Remember

| Task | Command |
|:----|:--------|
| Remove nightly override | `rustup override unset` |
| Clean project before re-running | `cargo clean` |
| Rebuild after further edits | `cargo run -Zbuild-std` |

---

# 🏆 Summary Quick Commands

```bash
rustup install nightly
rustup override set nightly
rustup component add rust-src --toolchain nightly

# Modify files in:
# ~/.rustup/toolchains/nightly-x86_64-unknown-linux-gnu/lib/rustlib/src/rust/library/std/src

cargo new my-std-test
cd my-std-test

# Edit src/main.rs

cargo run -Zbuild-std
```

✅ You are now running Rust with **your own custom standard library** without rebuilding the full compiler.

---
