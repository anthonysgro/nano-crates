# 📦 Nano Crate Suite

> Minimal, (mostly) zero-dependency Rust crates for focused applications.

A collection of tiny, focused Rust crates built on the standard library alone. Each one does one thing well and keeps its dependency count at zero. The one exception is **nanologger**, whose only dependencies are two other nano crates — [nanocolor](https://crates.io/crates/nanocolor) and [nanotime](https://crates.io/crates/nanotime) — keeping the family entirely self-contained. **nanoargs** also optionally depends on nanocolor for colored help output via a cargo feature.

## Crates

| Crate | Description | Version | GitHub | Coverage |
|-------|-------------|---------|--------|----------|
| 📎 [nanoargs](#-nanoargs) | Argument parser | [![crates.io](https://img.shields.io/crates/v/nanoargs.svg)](https://crates.io/crates/nanoargs) | [Repo](https://github.com/anthonysgro/nanoargs) | [![Coverage](https://coveralls.io/repos/github/anthonysgro/nanoargs/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanoargs?branch=main) |
| 🪵 [nanologger](#-nanologger) | Colored, leveled logger | [![crates.io](https://img.shields.io/crates/v/nanologger.svg)](https://crates.io/crates/nanologger) | [Repo](https://github.com/anthonysgro/nanologger) | [![Coverage](https://coveralls.io/repos/github/anthonysgro/nanologger/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanologger?branch=main) |
| 🎨 [nanocolor](#-nanocolor) | Terminal colors and styles | [![crates.io](https://img.shields.io/crates/v/nanocolor.svg)](https://crates.io/crates/nanocolor) | [Repo](https://github.com/anthonysgro/nanocolor) | [![Coverage](https://coveralls.io/repos/github/anthonysgro/nanocolor/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanocolor?branch=main) |
| ░ [nanoprogress](#-nanoprogress) | Progress bars | [![crates.io](https://img.shields.io/crates/v/nanoprogress.svg)](https://crates.io/crates/nanoprogress) | [Repo](https://github.com/anthonysgro/nanoprogress) | [![Coverage](https://coveralls.io/repos/github/anthonysgro/nanoprogress/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanoprogress?branch=main) |
| ⠋ [nanospinner](#-nanospinner) | Terminal spinners | [![crates.io](https://img.shields.io/crates/v/nanospinner.svg)](https://crates.io/crates/nanospinner) | [Repo](https://github.com/anthonysgro/nanospinner) | [![Coverage](https://coveralls.io/repos/github/anthonysgro/nanospinner/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanospinner?branch=main) |
| ⏱ [nanotime](#-nanotime) | Time utilities | [![crates.io](https://img.shields.io/crates/v/nanotime.svg)](https://crates.io/crates/nanotime) | [Repo](https://github.com/anthonysgro/nanotime) | [![Coverage](https://coveralls.io/repos/github/anthonysgro/nanotime/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanotime?branch=main) |

---

### 📎 nanoargs

[![Build Status](https://github.com/anthonysgro/nanoargs/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/anthonysgro/nanoargs/actions)
[![Crates.io](https://img.shields.io/crates/v/nanoargs)](https://crates.io/crates/nanoargs)
[![Docs.rs](https://docs.rs/nanoargs/badge.svg)](https://docs.rs/nanoargs/latest/nanoargs/)
[![Coverage Status](https://coveralls.io/repos/github/anthonysgro/nanoargs/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanoargs?branch=main)
[![License](https://img.shields.io/crates/l/nanoargs)](https://crates.io/crates/nanoargs)

> A lightweight, zero-dependency argument parser for Rust

[GitHub](https://github.com/anthonysgro/nanoargs) · [crates.io](https://crates.io/crates/nanoargs) · [docs.rs](https://docs.rs/nanoargs)

Flags, options, subcommands, help generation, env fallback, and typed parsing — everything you'd reach for `clap` for in a typical CLI, with zero dependencies.

**Install:**

```sh
cargo add nanoargs
```

**Dependencies:** 0 (only std; optional `color` feature adds [nanocolor](https://crates.io/crates/nanocolor))

```rust
use nanoargs::{ArgBuilder, Flag, Opt, Pos, ParseError};

fn main() {
    let parser = ArgBuilder::new()
        .name("myapp")
        .description("A sample CLI tool")
        .flag(Flag::new("verbose").desc("Enable verbose output").short('v'))
        .option(Opt::new("output").placeholder("FILE").desc("Output file path"))
        .positional(Pos::new("input").desc("Input file").required())
        .build()
        .unwrap();

    let args: Vec<String> = std::env::args().skip(1).collect();

    match parser.parse(args) {
        Ok(result) => {
            println!("verbose: {}", result.get_flag("verbose"));
            println!("output:  {:?}", result.get_option("output"));
            println!("input:   {:?}", result.get_positionals());
        }
        Err(ParseError::HelpRequested(text)) => print!("{}", text),
        Err(ParseError::VersionRequested(text)) => println!("{}", text),
        Err(e) => eprintln!("error: {}", e),
    }
}
```

---

### 🪵 nanologger

[![Build Status](https://github.com/anthonysgro/nanologger/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/anthonysgro/nanologger/actions)
[![Crates.io](https://img.shields.io/crates/v/nanologger)](https://crates.io/crates/nanologger)
[![Docs.rs](https://docs.rs/nanologger/badge.svg)](https://docs.rs/nanologger/latest/nanologger/)
[![Coverage Status](https://coveralls.io/repos/github/anthonysgro/nanologger/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanologger?branch=main)
[![License](https://img.shields.io/crates/l/nanologger)](https://crates.io/crates/nanologger)

> A minimal logger for Rust.

[GitHub](https://github.com/anthonysgro/nanologger) · [crates.io](https://crates.io/crates/nanologger) · [docs.rs](https://docs.rs/nanologger)

Colored, leveled logging to stderr with format!-style macros, optional timestamps, source locations, thread info, module filtering, file logging, and log facade integration.

**Install:**

```sh
cargo add nanologger
```

**Dependencies:** 2 — [nanocolor](https://crates.io/crates/nanocolor) and [nanotime](https://crates.io/crates/nanotime) (both nano family crates)

> ⚠️ nanologger is the only crate in the family that is **not** zero-dependency.
> Its only dependencies are two other nano crates, keeping the family self-contained.

```rust
use nanologger::{LoggerBuilder, LogLevel};

fn main() {
    LoggerBuilder::new()
        .level(LogLevel::Trace)
        .timestamps(true)
        .init()
        .unwrap();

    nanologger::error!("something went wrong: {}", "disk full");
    nanologger::warn!("retries remaining: {}", 3);
    nanologger::info!("server started on port {}", 8080);
}
```

---

### 🎨 nanocolor

[![Build Status](https://github.com/anthonysgro/nanocolor/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/anthonysgro/nanocolor/actions)
[![Crates.io](https://img.shields.io/crates/v/nanocolor)](https://crates.io/crates/nanocolor)
[![Docs.rs](https://docs.rs/nanocolor/badge.svg)](https://docs.rs/nanocolor/latest/nanocolor/)
[![Coverage Status](https://coveralls.io/repos/github/anthonysgro/nanocolor/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanocolor?branch=main)
[![License](https://img.shields.io/crates/l/nanocolor)](https://crates.io/crates/nanocolor)

> A minimal, zero-dependency terminal color and text styling crate for Rust

[GitHub](https://github.com/anthonysgro/nanocolor) · [crates.io](https://crates.io/crates/nanocolor) · [docs.rs](https://docs.rs/nanocolor)

ANSI 16-color support and common text styles through a chainable trait-based API — under 300 lines of code.

**Install:**

```sh
cargo add nanocolor
```

**Dependencies:** 0 (only std)

```rust
use nanocolor::Colorize;

fn main() {
    println!("{}", "error".red().bold());
    println!("{}", "warning".yellow());
    println!("{}", "success".green().on_black().underline());
}
```

---

### ██░░ nanoprogress

[![Build Status](https://github.com/anthonysgro/nanoprogress/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/anthonysgro/nanoprogress/actions)
[![Crates.io](https://img.shields.io/crates/v/nanoprogress)](https://crates.io/crates/nanoprogress)
[![Docs.rs](https://docs.rs/nanoprogress/badge.svg)](https://docs.rs/nanoprogress/latest/nanoprogress/)
[![Coverage Status](https://coveralls.io/repos/github/anthonysgro/nanoprogress/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanoprogress?branch=main)
[![License](https://img.shields.io/crates/l/nanoprogress)](https://crates.io/crates/nanoprogress)

> A minimal, zero-dependency terminal progress bar for Rust applications

[GitHub](https://github.com/anthonysgro/nanoprogress) · [crates.io](https://crates.io/crates/nanoprogress) · [docs.rs](https://docs.rs/nanoprogress)

Lightweight determinate progress bar — under 300 lines of code. Thread-safe, customizable width/fill/empty chars.

**Install:**

```sh
cargo add nanoprogress
```

**Dependencies:** 0 (only std)

```rust
use nanoprogress::ProgressBar;
use std::thread;
use std::time::Duration;

fn main() {
    let bar = ProgressBar::new(100)
        .message("Downloading...")
        .start();

    for _ in 0..100 {
        thread::sleep(Duration::from_millis(30));
        bar.tick(1);
    }
    bar.success("Download complete");
}
```

---

### ⠋ nanospinner

[![Build Status](https://github.com/anthonysgro/nanospinner/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/anthonysgro/nanospinner/actions)
[![Crates.io](https://img.shields.io/crates/v/nanospinner)](https://crates.io/crates/nanospinner)
[![Docs.rs](https://docs.rs/nanospinner/badge.svg)](https://docs.rs/nanospinner/latest/nanospinner/)
[![Coverage Status](https://coveralls.io/repos/github/anthonysgro/nanospinner/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanospinner?branch=main)
[![License](https://img.shields.io/crates/l/nanospinner)](https://crates.io/crates/nanospinner)

> A minimal, zero-dependency terminal spinner for Rust applications

[GitHub](https://github.com/anthonysgro/nanospinner) · [crates.io](https://crates.io/crates/nanospinner) · [docs.rs](https://docs.rs/nanospinner)

Lightweight animated spinner using only the Rust standard library — under 200 lines of code.

**Install:**

```sh
cargo add nanospinner
```

**Dependencies:** 0 (only std)

```rust
use nanospinner::Spinner;
use std::thread;
use std::time::Duration;

fn main() {
    let handle = Spinner::new("Loading...").start();
    thread::sleep(Duration::from_secs(2));
    handle.success();
}
```

---

### ⏱ nanotime

[![Build Status](https://github.com/anthonysgro/nanotime/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/anthonysgro/nanotime/actions)
[![Crates.io](https://img.shields.io/crates/v/nanotime)](https://crates.io/crates/nanotime)
[![Docs.rs](https://docs.rs/nanotime/badge.svg)](https://docs.rs/nanotime/latest/nanotime/)
[![Coverage Status](https://coveralls.io/repos/github/anthonysgro/nanotime/badge.svg?branch=main)](https://coveralls.io/github/anthonysgro/nanotime?branch=main)
[![License](https://img.shields.io/crates/l/nanotime)](https://crates.io/crates/nanotime)

> A minimal, zero-dependency time utility crate for Rust applications

[GitHub](https://github.com/anthonysgro/nanotime) · [crates.io](https://crates.io/crates/nanotime) · [docs.rs](https://docs.rs/nanotime)

Local and UTC time retrieval, nanosecond-precision timestamps, human-readable formatting, relative time strings, and lightweight elapsed duration measurement.

**Install:**

```sh
cargo add nanotime
```

**Dependencies:** 0 (only std + raw FFI)

```rust
use nanotime::{NanoTime, Elapsed};

fn main() {
    let now = NanoTime::now();
    println!("Local time: {}", now);
    println!("UTC: {}", NanoTime::now_utc().datetime());

    let timer = Elapsed::start();
    // ... do some work ...
    println!("Took {}", timer);
}
```

---

## Using Multiple Nano Crates

```toml
[dependencies]
nanoargs = "0.1"
nanologger = "0.1"
nanocolor = "0.1"
nanoprogress = "0.1"
nanospinner = "0.1"
nanotime = "0.1"
```

## Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on reporting issues, suggesting new crates, and contributing to existing ones.

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
