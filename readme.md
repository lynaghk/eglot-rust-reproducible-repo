## Problem

When using a path dependency in Cargo, flymake doesn't update with changes to that dependency.

To reproduce using this repo:

1. Use Emacs with Eglot mode to open `consumer/src/main.rs` and `dep/src/lib.rs`.
2. In lib.rs, remove field `b` from struct `Foo`.
3. Notice that flymake does *not* highlight an error in `main.rs`.
4. In `main.rs`, run emacs commands `eglot-shutdown` followed by `eglot`.
5. Notice that flymake now highlights the expected error, "struct `dep::Foo` has no field named `b`"


## Visual Studio Code

I suspect the problem is somewhere on the Emacs side rather than the language server (RLS) side, because Visual Studio Code uses the same language server but doesn't suffer from this problem.
Specifically, one can add `consumer` to their VSCode workspace, jump to definition of `Foo`, remove field `b`, and then immediately see the error highlighted in `consumer/src/main.rs`.


## Version info

```
rustc 1.40.0 (73528e339 2019-12-16)
rls 1.40.0 (5db91c7 2019-10-30)
Emacs 26.2
MacOS 10.14.6
eglot 20191230.913
flymake 1.0.8
```
