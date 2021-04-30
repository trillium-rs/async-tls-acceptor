# async-tls-acceptor


This crate provides a common interface for server-side tls acceptors,
abstracting over various implementations.

The only implementation provided by this crate is `()`, which is a
noop acceptor, and passes through the `Input` type.

Implementing this trait looks like:

```rust
use async_tls_acceptor::{async_trait, Acceptor, AsyncRead, AsyncWrite};

#[async_trait]
impl<Input> Acceptor<Input> for my_tls_impl::Acceptor
where
    Input: AsyncRead + AsyncWrite + Send + Sync + Unpin + 'static,
{
    type Output = my_tls_impl::TlsStream<Input>;
    type Error = my_tls_impl::Error;
    async fn accept(&self, input: Input) -> Result<Self::Output, Self::Error> {
        self.accept(input).await
    }
}
```

* [API Docs][docs] [![docs.rs docs][docs-badge]][docs]
* [Releases][releases] [![crates.io version][version-badge]][crate]
* [Contributing][contributing]
* [CI ![CI][ci-badge]][ci]
* [API docs for main][main-docs]

[ci]: https://github.com/trillium-rs/async-tls-acceptor/actions?query=workflow%3ACI
[ci-badge]: https://github.com/trillium-rs/async-tls-acceptor/workflows/CI/badge.svg
[releases]: https://github.com/trillium-rs/async-tls-acceptor/releases
[docs]: https://docs.rs/async-tls-acceptor
[contributing]: https://github.com/trillium-rs/async-tls-acceptor/blob/main/.github/CONTRIBUTING.md
[crate]: https://crates.io/crates/async-tls-acceptor
[docs-badge]: https://img.shields.io/badge/docs-latest-blue.svg?style=flat-square
[version-badge]: https://img.shields.io/crates/v/async-tls-acceptor.svg?style=flat-square
[main-docs]: https://trillium-rs.github.io/async-tls-acceptor/async-tls-acceptor/

## Safety
This crate uses `#![deny(unsafe_code)]`.

## License

<sup>
Licensed under either of <a href="LICENSE-APACHE">Apache License, Version
2.0</a> or <a href="LICENSE-MIT">MIT license</a> at your option.
</sup>

<br/>

<sub>
Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in this crate by you, as defined in the Apache-2.0 license, shall
be dual licensed as above, without any additional terms or conditions.
</sub>
