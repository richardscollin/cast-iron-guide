# Construction

In one sense, there's only a single way create struct, using the struct initializer syntax.
One the other hand, there are several conventional ways we can create objects built on top of this layer.

- `new()`
- `default()`
- or `with_extra_args(a1, a2)`

<div style="display: flex; gap: 12px;">
<div style="width: 100%;">

```rust
// Write this
Self {
    mode: RRMode::default(),
}
```
Pros:
- Will break if mode type is changed

</div>

<div style="width: 100%;">

```rust
// not that
Self {
    mode: Default::default(),
}
```
Pros:
- Consistent across types
- Won't break if mode type is changed

</div>
</div>

`Default::default()` is ok when it's a type you don't care about, but you can make 

## Rationale

if you change the type in the parent struct definition you want other code to break so that you're forced to
verify that the effected code is still correct.


- gitlab code review ~sucks~ leaves much to be desired if your accustomed to an IDE, one optimizes for code readability even in those restricted viewing environments.

- abusing `From` trait
  -  forces the reader to do type inference in their head to go from which into to find the write implementation

- consider also using the destructuring pattern binding in the From method to force all
fields to be used when converting types


## From

implementing from:
when it makes sense use destructuring in your from implementations to catch bugs


```rust
struct Foo {
  x: i32,
  y: i32,
}

struct Bar {
  a: i32,
  b: i32,
}
```

<div style="display: flex; gap: 12px;">
<div style="width: 100%;">

```rust
// instead consider doing this
impl From<Foo> for Bar {
  fn from(Foo {x, y}: Foo) -> Self {
    Self {
      a: x,
      b: y,
    }
  }
}
```
- they'll be forced to look at the From implementation

</div>
<div style="width: 100%;">

```rust
// don't do this
impl From<Foo> for Bar {
  fn from(value: Foo) -> Self {
    Self {
      a: value.x,
      b: value.y,
    }
  }
}
```
- an additional field to Foo causes no compilation changes

</div>
</div>

Why?

What happens if later on a developer (not you, or future you) changes Foo.
when the compilation fails.

TODO: this differs from recommendations <https://github.com/canonical/rust-best-practices/blob/main/best-practices.md#pattern-matched-parameters>

>  Indeed, the fact that a particular parameter is to be pattern-matched inside of the function is not important to the user—it is an unwelcome implementation detail and should be hidden as such.


## Looking ahead

I'm hopeful for some of the ideas being explored in [RFC 3681](https://rust-lang.github.io/rfcs/3681-default-field-values.html).
