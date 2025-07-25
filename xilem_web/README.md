<div align="center" class="rustdoc-hidden">

# Xilem Web

</div>

<div align="center">

**Experimental implementation of the Xilem architecture for the Web**

[![Latest published version.](https://img.shields.io/crates/v/xilem_web.svg)](https://crates.io/crates/xilem_web)
[![Documentation build status.](https://img.shields.io/docsrs/xilem_web.svg)](https://docs.rs/xilem_web)
[![Apache 2.0 license.](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](#license)
\
[![Linebender Zulip chat.](https://img.shields.io/badge/Linebender-%23xilem-blue?logo=Zulip)](https://xi.zulipchat.com/#narrow/stream/354396-xilem)
[![GitHub Actions CI status.](https://img.shields.io/github/actions/workflow/status/linebender/xilem/ci.yml?logo=github&label=CI)](https://github.com/linebender/xilem/actions)
[![Dependency staleness status.](https://deps.rs/crate/xilem_web/latest/status.svg)](https://deps.rs/crate/xilem_web)

</div>

This is a prototype implementation of the Xilem architecture (through [Xilem Core][]) using DOM elements as Xilem elements (unfortunately the two concepts have the same name).

## Quickstart

The easiest way to start, is to use [Trunk] within some of the examples (see the `web_examples/` directory).
Run `trunk serve`, then navigate the browser to the link provided (usually <http://localhost:8080>).

### Example

A minimal example to run an application with `xilem_web`:

```rust,no_run
use xilem_web::{
    document_body,
    elements::html::{button, div, p},
    interfaces::{Element as _, HtmlDivElement},
    App,
};

fn app_logic(clicks: &mut u32) -> impl HtmlDivElement<u32> + use<> {
    div((
        button(format!("clicked {clicks} times")).on_click(|clicks: &mut u32, _event| *clicks += 1),
        (*clicks >= 5).then_some(p("Huzzah, clicked at least 5 times")),
    ))
}

pub fn main() {
    let clicks = 0;
    App::new(document_body(), clicks, app_logic).run();
}
```

## Minimum supported Rust Version (MSRV)

This version of Xilem Web has been verified to compile with **Rust 1.88** and later.

Future versions of Xilem Web might increase the Rust version requirement.
It will not be treated as a breaking change and as such can even happen with small patch releases.

<details>
<summary>Click here if compiling fails.</summary>

As time has passed, some of Xilem Web's dependencies could have released versions with a higher Rust requirement.
If you encounter a compilation issue due to a dependency and don't want to upgrade your Rust toolchain, then you could downgrade the dependency.

```sh
# Use the problematic dependency's name and version
cargo update -p package_name --precise 0.1.1
```
</details>

<!-- We hide these elements when viewing in Rustdoc, because they're not expected to be present in crate level docs -->
<div class="rustdoc-hidden">

## Community

Discussion of Xilem Web development happens in the [Linebender Zulip](https://xi.zulipchat.com/), specifically the [#xilem channel](https://xi.zulipchat.com/#narrow/stream/354396-xilem).
All public content can be read without logging in.

Contributions are welcome by pull request.
The [Rust code of conduct] applies.

## License

Licensed under the Apache License, Version 2.0 ([LICENSE] or <http://www.apache.org/licenses/LICENSE-2.0>)

</div>

[Rust code of conduct]: https://www.rust-lang.org/policies/code-of-conduct
[Trunk]: https://trunkrs.dev/
[Xilem Core]: https://crates.io/crates/xilem_core

<!-- Needs to be defined here for rustdoc's benefit -->
[LICENSE]: LICENSE
