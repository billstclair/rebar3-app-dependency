rebar3-app-dependency
=====

This directory has two sub-directories, each of which is an Erlang
application with four sub-applications. I made it to illustrate how
the order of compilation for [rebar3](https://github.com/rebar/rebar3)
depends on dependencies in the .app.src files, but _not_ on their

`rebar3-app-test` has the following `.app.src` file:

```
{application, 'rebar3-app-test',
 [...
   {applications,
   [kernel,
    stdlib,
    app13, app21, app34, app42
   ]},
 ]}.
```

The four sub-apps each include only `kernel` and `stdlib` in their
`applications` list. The build looks like this:

```
$ cd .../rebar3-app-test
$ ./rebar3 compile
===> Verifying dependencies...
===> Compiling app42
===> Compiling app34
===> Compiling app21
===> Compiling app13
===> Compiling rebar3-app-test
```

Note that the compile order does _not_ match the order in the
`.app.src` file.

`rebar-related-app-test` has the following `.app.src` file:

```
{application, 'rebar3-related-app-test',
 [...
  {applications,
   [kernel,
    stdlib
   ]},
 ]}.
```

Its four sub-applications depend on each other in a chain, where
`a->b` means that `a` has `b` in the `applications` list in its
`.app.src` file:

```
app34 -> app13 -> app42 -> app21
```

The build looks like this

```
$ cd .../rebar3-related-app-test
$ ./rebar3 compile
===> Verifying dependencies...
===> Compiling app21
===> Compiling app42
===> Compiling rebar3-related-app-test
===> Compiling app13
===> Compiling app34
```

Note that the dependencies changed the order of compilation of the
sub-applications, but since the rebar3-related-app-test application
depends on none of the sub-applications, it is compiled in a random
place relative to them.

`tristan` said on `#rebar` that this is as designed.
