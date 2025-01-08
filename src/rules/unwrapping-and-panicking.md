> DON'T PANIC!
> 
> \- cover of "The Hitchhiker's Guide to ~the Galaxy~ Rust Programming"

# unwrapping

- Don't unwrap, expect instead
- When you have a helper function which unwraps annotate it with `#[track_caller]`

Don't unwrap doesn't mean don't write unwraps. Instead it means you better be sure
that that unwrap won't trigger in production.

Every unwrap should be carefully code reviewed an analyzed to verify it won't cause
an issue. Better yet is to document your assumptions using expect instead of unwrap.
This can lead to a bit of unnecessary code noise, but it's worth it.

## References

- <https://blog.burntsushi.net/unwrap/>
- <https://zkrising.com/writing/three-unwraps/>


The zkrising blog post is quite interesting. I tried implementing my own polyfill for the unwrap variants he mentions: `unwrap_panic`, `unwrap_todo`, and `unwrap_unreachable`. It ends up being not that useful. Just calling expect, covers both the unwrap kind of, this should never happen (and document my thoughts why) and if this happens it should be a fatal error.
