rebar3-app-test
=====

Test application with four members in `apps/`. All four are listed as
`applications` in `src/rebar3-app-test.app.src`.

The apps themselves do NOT use each other.

See `rebar3-related-app-test` for an app with related sub-apps.

In "rebar 3.0.0-beta.3+build.3079.ref2754214 in OTP r16b03, 17.5, and
18.1", with the applications listed in rebar3-app-test.app.src in the
order:

```
{application, 'rebar3-app-test',
 [...
  {applications,
   [kernel,
    stdlib,
    app21, app13, app42, app34
   ]},
  ...
 ]}.
```

here's the build output:

```
$ ./rebar3 compile
===> Verifying dependencies...
===> Compiling app42
===> Compiling app34
===> Compiling app21
===> Compiling app13
===> Compiling rebar3-app-test
```

Changing the order in `rebar-app-test.app.src` file doesn't
affect this.

Tristan said on #rebar that this is as expected.

Build
-----

    $ rebar3 compile
