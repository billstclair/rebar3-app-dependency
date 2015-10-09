rebar3-related-app-test
=====

Test application with four members in `apps/`. None of them are listed as
`applications` in `src/rebar3-related-app-test.app.src`.

The apps themselves have dependencies as follows, where `a->b` means that `a` depends on `b` by listing `b` as an `application` in `a.app.src`.

```
app34 -> app13 -> app42 -> app21
```

See `rebar3-app-test` for an app with no dependecy between its sub-apps.

In "rebar 3.0.0-beta.3+build.3079.ref2754214 in OTP r16b03, 17.5, and 18.1, here's the build output:

```
$ ./rebar3 compile
===> Verifying dependencies...
===> Compiling app21
===> Compiling app42
===> Compiling rebar3-related-app-test
===> Compiling app13
===> Compiling app34
```

Note that the sub-apps are in the specified order, but `rebar3-related-app-test` is compiled in a pretty random place, due to its lack of dependency on any of the sub-apps (must be a hash table there somewhere).

Build
-----

    $ rebar3 compile
