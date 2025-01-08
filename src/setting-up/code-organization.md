# Project Organization

## Workspace vs Single Crate

If your project will consist of many different crates you should make use of a [cargo workspace](https://doc.rust-lang.org/cargo/reference/workspaces.html).

### Workspace Organization

location of workspace members

- src
- crates
- / (root)

```
.
├── Cargo.lock
├── Cargo.toml
├── clippy.toml
├── crates
│   └── single
│       ├── Cargo.toml
│       └── src
│           ├── lib.rs
│           ├── logging.rs
│           └── main.rs
├── README.md
├── rustfmt.toml
├── rust-toolchain.toml
├── taplo.toml
├── tools
│   └── lint
└── typos.toml
```

### Single Crate Organization

## Cargo Generate

[`cargo-generate`](https://crates.io/crates/cargo-generate) is a tool to generate a repo using an existing git repo as a template.
Using it isn't strictly necessary, you could just clone the repo and change the package name.

```
cargo install cargo-generate
```

```
cargo generate https://github.com/richardscollin/rust-template-workspace
```

# Recommended Tools

## Taplo

Rust projects use a lot of toml configuration files. It's nice to be able to format it.

## Typos

Check code for typos.A


## Clippy config

```toml
[lints.rust] # https://doc.rust-lang.org/rustc/lints/groups.html
unknown_lints                   = "allow" # non_exhaustive_omitted_patterns, unqualified_local_imports

exported_private_dependencies   = "warn"
let_underscore_drop             = "warn"
non_exhaustive_omitted_patterns = "deny"
unqualified_local_imports       = "deny" # https://github.com/rust-lang/rust/pull/125645
unused_imports                  = "allow"

[lints.clippy] # https://rust-lang.github.io/rust-clippy/master/index.html
shadow_reuse                  = "warn"
shadow_same                   = "warn"
shadow_unrelated              = "warn"
unwrap_used                   = "warn"
significant_drop_in_scrutinee = "warn"
# print_stdout                 = "warn"
```


# References

- <https://matklad.github.io/2021/08/22/large-rust-workspaces.html>
- <https://doc.rust-lang.org/cargo/reference/workspaces.html>
- <https://doc.rust-lang.org/cargo/guide/project-layout.html>



# mod.rs convention vs. module.rs and module/ folder

Yet another arbitrary decision that doesn't really matter.
The main thing that matters in being consistent within a project.
Choose one that you prefer and try to stick to that.


There's not a clear benefit to using one style over the other.
If you're working on a project which already makes use of one
of these styles, you're best continuing to use that.

- `#[warn(clippy::mod_module_files)]`
- `#[warn(clippy::self_named_module_files)]`

<div style="display: flex; gap: 12px;">
<div style="width: 100%;">

## mod.rs
pros:
- all files in a modules are at the same hierarchy level
- supported on older (pre-2018) rust compilers

</div>
<div style="width: 100%;">

## module.rs and module/
pros:
- no need to rename if converting code to a module
- less filename duplication in editor tabs (though many editors handle this well already)

</div>
</div>

- <https://doc.rust-lang.org/stable/book/ch07-02-defining-modules-to-control-scope-and-privacy.html>
- <https://doc.rust-lang.org/book/ch07-05-separating-modules-into-different-files.html>
- <https://doc.rust-lang.org/reference/items/modules.html#module-source-filenames>
- <https://internals.rust-lang.org/t/the-module-scheme-module-rs-file-module-folder-instead-of-just-module-mod-rs-introduced-by-the-2018-edition-maybe-a-little-bit-more-confusing/21977>
- <https://users.rust-lang.org/t/module-mod-rs-or-module-rs/122653>

## improve file tree editor support

ideally editors would know to not order files in the file tree alphabetically, but to follow module convention such that module.rs files are grouped with their corresponding module/ directory and mod.rs is put at the root.

neo-tree custom ordering

- [VSCode Custom Sorting Issue](https://github.com/microsoft/vscode/issues/27286)



# Organization

- extern crates
- mod
- use std
- use external crates
- use workspace
- use crate::

The first lines in your rust code will likely be some `use` declarations. How should you group your use declarations?

Consistent import style is useful because it can help reduce merge conflicts.

When I started my first job programming rust, our team had a discussion over a good convention to follow
for formatting use statements (imports). Most of use being familiar with python, we settled on the convention similar
to PEP8 import convention.

The first import group belongs to std. The second group: external crates. The third: our own code.

The problem with this choice is it's not the default rust formatting option. It requires manual effort to maintain compared to just using a single import
group. The imports quickly deteriorated into ... whatever, no convention.

After unsuccessfully trying to follow this style, I recommend projects with multiple team members adhere to the One import group style.

When StdExternalCrate is properly* supported by stable rustfmt, then it may make sense to reconsider this decision. Until then:
just group your imports into a single sorted group and let rust-analyzer manage them.

It's difficult to enforce a style for other developers to use if `rustfmt` doesn't support it.
Currently the style I use is the StdExternalWorkspaceCrate, but it's a annoying to maintain
when other co-workers use rustfmt and rust-analyzer to handle imports and this isn't a real mode.

[group_imports](https://rust-lang.github.io/rustfmt/?version=v1.6.0&search=#group_imports)
<https://github.com/rust-lang/rustfmt/issues/5083>

Rust-analyzer doesn't follow this.
rustfmt will sort groups if they are grouped

programmers will use their ide to auto import if things aren't setup the same way then it

mod before use
<!-- imports layout 
I also personally prefer imports_layout = vertical, but I think that might be too opinionated

others thoughts
https://github.com/rust-lang/compiler-team/issues/750
-->


## Impl ordering

how to structure impl. still unsure, instead I'll discuss trade-offs.

Want important code first

- struct def
- trait impls
- inherent impl

there are alternatives:

- struct def
- trait impls
- inherent impl

Or:

- all structs
- traits and impls

