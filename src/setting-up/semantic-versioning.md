# Semantic Versioning

Semantic versioning enables interoperability within the rust ecosystem.

If you are using a private cargo workspace not published to crates.io you can eschew
considering semantic versions entirely and just never update your project versions.
However if you are publishing your crate it's good to be aware of when a semantic version
change is required.

Many crates break semver. You should still use cargo-semver-checks. I've been broken
by crates which intentionally published semver breaking changes over a minor release.

<!--
  Every time I see the github profile of that developer I'm like, fuck that guy!
  He's the one who always breaks my code.
-->

Doing this too often will annoy your users and hurt the ecosystem.

- aahash crate nightly sniffing versions
- rustls 22 -> 23 aws-lc on windows nasm
- sqlx nightly dependency bug


Accidental and intentionally semver breakages happen. You should avoid breaking people's code,
but if you do, at least do it with intention and a good reason.

To mitigate these breakages, you should consider committing your Cargo.lock file.

- <https://users.rust-lang.org/t/psa-please-specify-precise-dependency-versions-in-cargo-toml/71277>
- <https://github.com/obi1kenobi/cargo-semver-checks>
- <https://doc.rust-lang.org/cargo/reference/semver.html>
- <https://matklad.github.io/2024/11/23/semver-is-not-about-you.html>
