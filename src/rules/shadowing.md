# Shadowing

I have mixed feelings on shadowing. Initially when I learned of the feature I didn't like it.
It seems many others have the same [feeling](https://stackoverflow.com/questions/59860476/what-is-the-rationale-behind-allowing-variable-shadowing-in-rust). I felt that shadowing contradicts a coding principle from [Code Complete, 2nd Edition.](https://learning.oreilly.com/library/view/code-complete-2nd/0735619670/) Section 10.8: Using Each Variable for Exactly One Purpose.
Reusing a variable name for a new binding seems clunky.

However, after seeing shadowing used effectively and meaningfully in [Mara Bos Book](https://marabos.nl/atomics/basics.html#naming-clones) I've changed my mind on wanting to restrict shadowing completely.

There are still some kinds of shadowing I feel are bad:

- unrelated shadowing
- shadowing in large scopes / functions where it's easy to lose context

in short scopes it's okay, but it can lead to accidental unused variables
or getting confused about the value that being bound. In large functions
shadowing means you have to trace all previous usages.

proponents might say you can make use of shadowing to prevent accidental reuse.

In fact, the one allowable exception I've seen for shadowing is:

```rust
let a = Arc::new([1, 2, 3]);

let b = a.clone();

thread::spawn(move || {
    dbg!(b);
});

dbg!(a);

// -----------
let a = Arc::new([1, 2, 3]);

thread::spawn({
    let a = a.clone();
    move || {
        dbg!(a);
    }
});

dbg!(a);
```

I think this pattern is very useful because having a bunch of variables called:

a_clone, just so you can move them is quite ugly.


## Other uses

When first learning rust, I frequently got the error message: "temporary value dropped while borrowed".
This is another case where it may make sense to make use of shadowing. See [super-let](https://blog.m-ou.se/super-let/).
TODO: flesh out the details here more.

