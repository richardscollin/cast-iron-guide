# How should I learn Rust?

Different people learn differently and have different experience. Firstly, I wouldn't
recommend Rust as a first programming language. For most people, I'd recommend either
python or javascript as those are typically easier to learn, and get you to a place
where you can build cool things quickly.

If you already have programming experience I'll group your prior language experience into one of four rough categories:

- **Web**: javascript, typescript
- **Scripting**: python, ruby
- **Typed**: java, C#, go
- **Bare-Metal**: C, C++

If you've got experience from the Web and Scripting categories I'd probably recommend [the book](https://doc.rust-lang.org/stable/book/).
If you're coming from the Typed or Bare-Metal groups, [the book](https://doc.rust-lang.org/stable/book/) is still good,
but I might also recommend concurrently reading [Programming Rust](https://www.oreilly.com/library/view/programming-rust-2nd/9781492052586/)
and sticking with whichever you prefer. If you already have a lot of programming background,
such as a Computer Science degree,
I'd recommend going with [Programming Rust](https://www.oreilly.com/library/view/programming-rust-2nd/9781492052586/)
and switching back to the book if you find it too difficult.

# How long does it take to learn rust?

Before actively learning Rust, I estimated it would take me 2 months to learn the language.
I had binged a Ruby book and picked up that language in that amount of time for a previous job.
That was a gross underestimation. Rust is ... different.

I estimate an experienced programmer will take 6 - 12 months of daily effort before they are fluent in Rust.
That's about how long it took me. Yes, you'll be committing and contributing effectively well before then,
but having a strong grasp of the language will take time. Furthermore, don't be fooled thinking that once
you finish reading The Book, you'll have enough knowledge to be self sufficient. Notably the Rust language
isn't batteries included. You'll also have to spend some time wading through the crate ecosystem before
being competent.

# I want to start a project in Rust, but I haven’t found any good ideas yet. Does anyone have suggestions?

To me this is a bit of an odd question because I'm often teeming with ideas.
In fact, I keep a notes pages on my phone dedicated to different project ideas.
Here's a couple off the top:

1. `dashmap` no send sync drop-in replacement [Implemented](https://github.com/richardscollin/dashmap-no-send)
2. A crate to verify if two crates are drop in replacements (Could use rustdoc json api, cargo-semver-checks or similar)
3. Json Diffing Tool
4. Write my own Async Executor (for learning)
5. Gitlab cargo registry tools. [Basically this](https://gitlab.com/gitlab-org/gitlab/-/issues/33060)
6. cargo doc rust source include line coverage info from tests
7. rustdoc view source include asm view (like godbolt, but included in rustdoc)
8. Crab-themed terminal tower defense game

The list goes on, but most likely none of those ideas are very interesting to you. **Good**, you've proven my point[^1].
Side project are usually quite personal things. It depends a lot on your background and interests and what you
hope to get out of the project.

I think maybe this question comes up because there are projects which don't require Rust and are much simpler to use another tool,
but they still want to learn Rust because it seems like there's a bunch of hype around the language.

If this is you I'd recommend thinking hard is your primary objective to work on a project or learn rust?

## Walk-through

- [Write an OS in Rust](https://os.phil-opp.com/)

- Web (frontend)

Some things are better suited for other languages. For example building a website (frontend). Yes, you can do it in Rust. Wasm is a thing.
But I still wouldn't wish it on my worst enemy. Why? Lots of reasons. The biggest being the development experience is not good enough yet.
Imagine it taking 2 minutes to re-compile your site for very minor front end changes. That's just not acceptable for me to recommend.

If you've built web apps before using other modern tools, using rust will feel like going back to the stone age.

If you're so in love with rust, that the though of writing javascript makes you want to login to reddit and start calling people names,
then yes, some rust web frameworks exist for you, and you might be happy using them. For the rest of us who want to get work done,
use another tool.

[^1]: As a side note, if any are interesting to you please just go ahead and implement them. Less work for me :)

# How do I find a Rust job?

Good question!

Rust has yet to achieve widespread insdustry adoption. Though more companies are hiring.

Often times a company doesn't just want a "Rust programmer".

Instead they'll want an embedded engineer, backend web engineer, a distributed system engineer, or a crypto(currency) engineer who either
knows or is willing to learn rust.

It's probably wise to gain competency in another area which complements rust, because programming language skill isn't actually that
useful by itself without other expertise.

Sometimes the jobs aren't even advertised as Rust jobs.
The job I eventually landed I thought was looking for C/C++ people.
Only to find out they decided to switch to rust.

- [r/rust monthly job posting](https://www.reddit.com/r/rust/comments/1h2zwpx/official_rrust_whos_hiring_thread_for_jobseekers/)
- [Filtra Monthly Rust Jobs Report](https://filtra.io/rust/jobs-report/nov-24)
