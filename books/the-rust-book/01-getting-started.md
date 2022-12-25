## Installing Rust

Install `rustup`:
```bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

`rustup update`:
- update to latest version

`rustup self uninstall`:
- uninstall Rust and `rustup`

`rustup doc`:
- open local Rust documentation in the browser (Rust ships with its docs on install)

## Main function

- All Rust programs have a `main` function
- The `main` function is **always** the first code that runs in every executable Rust program

```rust
fn main() {
	println!("Hello, world!");
}
```

## Compiling & Running

`rustc <filename.rs>`:
- takes the source code file with `.rs` extension
- outputs the rust executable (`.exe` on windows, no extension on *nix)

`./<executable>`:
- runs the binary produced by compiler

## Cargo

- Rust's build system *and* package manager
	- builds our code
	- downloads dependencies
	- builds dependencies

`cargo new <project name>`:
- creates a new directory with given name, and generates a `Cargo.toml` config file and a `src/` directory with `main.rs` inside
- `cargo` expects source files to live in the `src/` directory
`cargo build`:
-  creates an executable file in `target/debug/<project name>`
`cargo run`:
- compiles and then runs the executable
- cargo will only rebuild the executable if it detects changes
`cargo check`:
- checks code to make sure it compiles, but doesn't yield an executable file
- usually runs much faster than `cargo build`
`cargo build --release`:
- compile an executable that is fully optimized in `target/release`
- optimizations make the executable run faster, but takes a longer time to compile
