[![Travis](https://travis-ci.org/japaric/rust-everywhere.svg?branch=master)](https://travis-ci.org/japaric/rust-everywhere)
[![Appveyor](https://ci.appveyor.com/api/projects/status/d37xqtcx5ct9fyfr?svg=true)](https://ci.appveyor.com/project/japaric/rust-everywhere)

# `rust-everywhere`

> Use CI services to generate binary releases of your Rust program for Linux, Mac and Windows

This repository has configured [Travis CI] and [AppVeyor] to generate **[binary releases]** of a
Cargo project (in this example, a variation of hello world) for all the [tier 1] platforms and some
lower tier platforms whenever a new git tag is pushed.

[Travis CI]: https://travis-ci.org/
[AppVeyor]: https://www.appveyor.com/
[binary releases]: https://github.com/japaric/rust-everywhere/releases
[tier 1]: https://doc.rust-lang.org/book/getting-started.html#tier-1

## Supported targets

The current CI configuration builds, tests and generates binary releases for the following targets:

- `arm-unknown-linux-gnueabihf`. **WARNING** Experimental target. Tests are executed using qemu user
    emulation, but this approach may have problems when too many threads are spawned. Also, by the
    next Rust stable release, this target will be replaced by `armv7-unknown-linux-gnueabihf`.
- `i686-apple-darwin` (32-bit OSX)
- `i686-pc-windows-gnu` (32-bit Windows, MinGW)
- `i686-pc-windows-msvc` (32-bit Windows, MSVC)
- `i686-unknown-linux-gnu` (32-bit Linux)
- `x86_64-apple-darwin` (64-bit OSX)
- `x86_64-pc-windows-gnu` (64-bit Windows, MinGW)
- `x86_64-pc-windows-msvc` (64-bit Windows, MSVC)
- `x86_64-unknown-linux-gnu` (64-bit Linux)
- `x86_64-unknown-linux-musl`. (64-bit Linux, statically linked binaries)

## How to use

You can use this CI configuration as a starting point for your project by copying the `.travis.yml`
and `appveyor.yml` files and the `ci` directory in your project repository. And then customizing
the configuration for your needs by implementing all the `TODO`s contained in those files.

All these aspects can be configured:

- Test on any combinations of these channels: stable, beta and nightly.
- Deploy on one of these channels: stable, beta and nightly.
- The contents of the release tarball/zipfile
- CI phases like `install` and `script`

Once configured, simply push a new git tag to build a new binary release:

``` sh
git tag v1.2.3
git push --tags
```

You should see the release tarballs/zipfiles under your project's ['releases'] page.

['releases']: https://github.com/japaric/rust-everywhere/releases

## Using a binary release with Travis CI

If you want to use a binary release generated by rust-everywhere (to save time by not having to call
`cargo install`) on a Travis build job, you can use the `install.sh` script contained in this
repository and use it like this in your Travis configuration:

```
install:
  - curl -sf "https://raw.githubusercontent.com/japaric/rust-everywhere/master/install.sh" | bash -s -- --from azerupi/mdBook --tag 0.0.11-rc1
```

Check the script for more information about its usage, and it's not very robust on errors so use it
with care ;-).

## Known issues

- The Cargo project must be hosted on GitHub. I know GitLab also has a "releases" feature but I
    don't know if it can be integrated with Travis CI and/or AppVeyor. AFAICT Bitbucket has no
    "releases" equivalent. And IDK about other git hosting solutions.

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or
  http://www.apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the
work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any
additional terms or conditions.
