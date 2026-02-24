# Contributing to the Nano Crate Family

Thanks for your interest in contributing! The nano crate family is a collection of minimal Rust crates for CLI applications, and we welcome contributions of all kinds.

## Reporting Issues

Each crate lives in its own repository. Please file issues on the appropriate crate's repo:

- **nanoargs** — [github.com/anthonysgro/nanoargs/issues](https://github.com/anthonysgro/nanoargs/issues)
- **nanocolor** — [github.com/anthonysgro/nanocolor/issues](https://github.com/anthonysgro/nanocolor/issues)
- **nanospinner** — [github.com/anthonysgro/nanospinner/issues](https://github.com/anthonysgro/nanospinner/issues)
- **nanoprogress** — [github.com/anthonysgro/nanoprogress/issues](https://github.com/anthonysgro/nanoprogress/issues)
- **nanologger** — [github.com/anthonysgro/nanologger/issues](https://github.com/anthonysgro/nanologger/issues)
- **nanotime** — [github.com/anthonysgro/nanotime/issues](https://github.com/anthonysgro/nanotime/issues)

For issues related to this landing page repository itself (broken links, typos, etc.), feel free to open an issue here.

## Suggesting New Crates

Have an idea for a new nano crate? Open an issue on this repository with:

- A short name following the `nano*` convention
- What problem it solves for CLI applications
- Why it belongs in the nano family (minimal, focused, zero-dependency where possible)

## Contributing to Existing Crates

To contribute code to an existing crate:

1. Fork the crate's repository (linked above)
2. Create a feature branch from `main`
3. Keep changes minimal and focused — that's the nano way
4. Make sure all existing tests pass
5. Open a pull request with a clear description of your changes

### Guiding Principles

- **Stay minimal.** Every crate should do one thing well in as few lines as possible.
- **Avoid dependencies.** Use only the Rust standard library unless absolutely necessary. If a dependency is needed, prefer other nano family crates.
- **Keep it readable.** Clear code over clever code.
