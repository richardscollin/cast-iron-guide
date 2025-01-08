# Derive Conventions

## Alphabetically sort `#[derive]` attributes.

This isn't done by rustfmt because there could be code differences if you reorder derives, see: <https://github.com/rust-lang/rustfmt/issues/4112>.

First all attributes from the std library unprefixed, then traits from external crates
prefixed with the crate name.

## Use crate prefixed `#[derive]` attributes

Using the prefixing means the derives will be unambiguous. (Many crates reuse the name Serialize and Deserialize).
This means if you want to derive `serde::Serialize`.

<div style="display: flex; gap: 12px;">
<div style="width: 100%;">

```rust
// Instead of this,
use serde::Serialize;

#[derive(Serialize)]
struct Foo {
    x: i32,
    y: i32,
}
```
</div>

<div style="width: 100%;">

```rust
// use this.

#[derive(serde::Serialize)]
struct Foo {
    x: i32,
    y: i32,
}


```
</div>

</div>


## Comments should go before derives.

Comments can get large, it's possible to miss a derive if it's above the comments.

# See Also
- <https://github.com/maksym-arutyunyan/keepsorted>
- <https://crates.io/crates/cargo-sort-derives>
