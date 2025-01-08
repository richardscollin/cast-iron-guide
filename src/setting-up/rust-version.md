# Picking a Rust Channel

When you start your project you'll need to choose a channel for your toolchain. There are 3 options stable, beta, or nightly.

Use **stable**.

At some point while developing, you'll see a function you want to use that's only available on nightly.
Avoid the temptation to switch to the nightly compiler and enabling unstable feature flags.

The allure of new features and brand new API's may be exciting at first, but it's not worth the long term effort.
Keeping up with new nightly features is exhausting.

## You NEED nightly you say

You couldn't possibly write code without using let-chains or the ! (never) type.
**Tough**, syntactic sugar is not a good enough reason.

If there's a legitimate reason you're using nightly, then here's some advice.

📌 Use a pinned version of the compiler and update when it suites you.
Even better, only upgrade to the nightly version released right before a beta release a couple weeks after the fact.
If you don't, [you might encounter failures in external crates compiling on nightly when things break](https://github.com/tkaitchuck/aHash/issues/200).
Also, know if you follow this technique you may be missing important patches which were merged into the stable branch,
but you'll never receive on your pinned version.

🚩 Be conservative with which `#[feature(flags)]` you enable.
Don't enable things simply because they are are "nice to have".
Reducing your unstable surface decreases the likelihood of hitting an unstable breakage.

You'll find that the more unstable feature flags you enable the more edge cases you'll hit.
For example, you'll discover that nice syntactic sugar you couldn't live without isn't supported by the most popular macro crates.

🦀 🧊 🐛 I've encountered trait solver bugs, [ ICE (internal compiler errors)](https://github.com/rust-lang/glacier), and more.

If you haven't changed your mind yet.
You'll want to keep up with unstable language updates to know how to make use of these features.
The compiler bug tracker is there too. You never know.

- [The Unstable Book](https://doc.rust-lang.org/unstable-book/)
- [Unstable Cargo Features](https://doc.rust-lang.org/cargo/reference/unstable.html)
- [Rust issues](https://github.com/rust-lang/rust/issues)

Working on your project shouldn't require you track compiler bugs. In short, use stable.

(Yes, for trying out new features on your own, it's fine to try out nightly.)

## Which stable?

Use the latest stable version of rust at the time you start your project.
During development you should track the new stable releases and update when it's convenient for you.
I recommend staying within the last 3 stable versions of rust.
If you get too far out of date new versions of some crates may not support your older compiler.
If you want to be able to always upgrade all your dependencies to the latest versions you'll still need to be on a recent compiler.


create a rust-toolchain.toml and specify the full path in private repo
