## On tuples and readability

Tuples are an incredibly useful language construct. They can make prototyping and modify existing quick and easy.

That said, I recommend to avoid using them wherever possible. They can harm long term readability of code.

For example, code which starts out like this:
```rust
fn get_my_data() -> Data { }
```

can easily become this:
```rust
fn get_my_data() -> (Data, chrono::DateTime) { }
```

This isn't that bad. But what's the new interface return? The code doesn't document itself. A better interface would define a struct which gives the new field as name.
```rust
struct DataAndCreatedAt {
  data: Data,
  created_at: chrono::DateTime,
}
```

It's also better to do this early on before the return type becomes something like:
```rust
fn get_my_data() -> (Data, chrono::DateTime, chrono::DateTime, chrono::DateTime, u32) { }
```

Another reason to avoid defining tuples in your code is it the field accessors end up being hard to read because of the lack of names.

Better to avoid these problem at it's bud a define custom structs.
One allow exception to this rule is newtype structs with a single field, these can be defined using tuple struct syntax if so desired.
(but a curly brace struct works as well).

Exceptions:

One notable exception is when interacting with well known interface which require their usage such as:

- iterating over a key value map such as `HashMap::into_iter` or `BTreeMap::into_iter`
- creating a channel
