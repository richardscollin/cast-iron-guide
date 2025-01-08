# Introduction

I bought my first cast iron skillet in college with my two roommates.
We spent so much time in the store debating which one to buy that a passerby gave us a recommendation just so we'd stop arguing.

I hope I can be like that passerby for you. Someone that says: Do **this** and not *that*.
I'll discuss the trade-offs of different styles and then share my personal preference.
The explanation is the important part, because you aren't meant to blindly follow rules.

There are other resources doing similar things.
I recently discovered a [rust style guide published by Canonical](https://github.com/canonical/rust-best-practices) and shared in this [talk](https://www.youtube.com/watch?v=39utxTvS6hE&list=PL2b0df3jKKiTWZeF7cip6ZUsaVXxWioRi&index=31). I list some more style resources [here](/resources.html#style-guides).
If I knew of these the time I started this guide, maybe I wouldn't have created it.
Interestingly, some of the style recommendations from other sources differ from my own.
That's okay. For me, it shows that many of the decisions are somewhat arbitrary.
It made me focus more on the discussion of the differences and less on the decision itself.

The main motivating factor for me writing all of this down is the belief that:

- Having a consistent style improves readability and maintainability
- Having less arbitrary choices reduces "decision fatigue" and lead to better code
- Moving pedantic style discussions out of code reviews reduces team frustration

For many projects, it doesn't matter which style guide is used.
In this guide, I'll try to enumerate the trade-offs of some the arbitrary decisions
such that there's no need to debate the decisions.

Some Coding Style guides for other languages say things like: Don't sweat the small stuff.
One one hand, I agree. Enforcing arbitrary standards is meaningless.
However, codifying a coding style is an interesting exercise. Rust already has so many
tools that enforce consistency (rustfmt, clippy). When the existing tools and guides provide
no guidance, it's sometimes hard to decide which way to do something, especially as a new rust developer.

`clippy`, `rustfmt` and the [rust-style-guide](https://doc.rust-lang.org/stable/style-guide/index.html) also lay out some conventions,
but, as being part of the standard toolchain, the defaults are rightly unopinionated.
You have to turn a few knobs to get them to my desired configuration.

Guiding principles
==================

- Use the compiler to ensure correctness at compile time
- I want to implement most rules in the form of an automated tool, such as clippy or something else.
- Be opinionated. (Better to have an opinionated resource you disagree with over one that doesn't commit)

These rules should be automated. If you're wasting your brain cells enforcing them manually in code review
or through other means, you're fighting a losing battle. An urgent change wins over abstract notions of clean code, but good linting tooling will get most stubborn developers to just make the change.


Disclaimer
==========

This should go without saying, but if it's clear a rule is wrong in a certain circumstance, don't follow it.

Also, a lot of learners get too focused a lot on writing "idiomatic" Rust. I know I did. [Don't worry about that too much.](https://users.rust-lang.org/t/idioms-regarding-main-rs/122181/2) Instead, focus on accomplishing the task at hand.

I've never heard of people so concerned about idiomatic code in other languages, sure people talk about writing
pythonic python, but

