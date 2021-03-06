This is the project that packages Rust in various formats. Currently
its job is to combine the outputs of the Rust build with that of the
Cargo build, both in [rust-installer] format, and produce installers
in a variety of formats.

[rust-installer]: https://github.com/rust-lang/rust-installer

# Usage

First you need to acquire the components that make up the Rust
installation, rustc, cargo, rust-docs, and - on Windows - rust-mingw,
containing portions of the mingw toolchain necessary to make Rust
work, as well as the corresponding source tarball (which is used to
fish out some version information, yech). *Note: neither the OS X nor
Windows builds actually produce source tarballs at the moment. It
would be much better for the binary tarballs to [include the
information](https://github.com/rust-lang/rust/pull/20388) the build
wants (but also would be good for those builds to produce source
tarballs).*

The easiest way to do this is just:

```
$ ./fetch-inputs.py --target=x86_64-unknown-linux-gnu --channel=nightly
```

Which will fetch the official binaries that correspond to the given
channel and put them in the `./in` directory.

To package from locally-built Rust and Cargo, just copy the tarballs
into `./in`.

Then to package, e.g.:

```
$ ./package-rust.py --target=x86_64-unknown-linux-gnu
$ ./package-rust.py --target=x86_64-apple-darwin --pkg
$ ./package-rust.py --target=x86_64-pc-windows-gnu --exe --msi
```

`--pkg`, `--exe`, and `--msi` are optional, producing
platform-specific installers *in addition* to the tarball
installer. These only work when run on OS X or Windows.

# License

This software is distributed under the terms of both the MIT license
and/or the Apache License (Version 2.0), at your option.

See [LICENSE-APACHE](LICENSE-APACHE), [LICENSE-MIT](LICENSE-MIT) for details.
