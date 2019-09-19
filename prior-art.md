# Inspiration

We considered sevral systems. At the heart of them there's a method to declare a rule that takes
some set of inputs, runs a shell script or other executable and creates some output. Rules can
be composed together. An output from one rule can be used as the input to others



## Anaconda
You provide a `build.sh` and/or `build.bat`

```
mkdir -p $PREFIX/bin
cp $RECIPE_DIR/my_script_with_recipe.sh $PREFIX/bin/super-cool-script.sh
```

Anything you write to `$PREFIX` is in the conda package.

## Bazel
[https://docs.bazel.build/versions/master/be/general.html#genrule]

```python
genrule(
    name = "foo",
    srcs = [],
    outs = ["foo.h"],
    cmd = "./$(location create_foo.pl) > \"$@\"",
    tools = ["create_foo.pl"],
)
```


## Nix
[https://nixos.org/nixos/nix-pills/index.html]


A nix deriviation called simple that compile an c executable
```nix

with (import <nixpkgs> {});
derivation {
  name = "simple";
  builder = "${bash}/bin/bash";
  args = [ ./simple_builder.sh ];
  inherit gcc coreutils;
  src = ./simple.c;
  system = builtins.currentSystem;
}
```

A builder is anything that can be executed in this example note that it's just 
a bash script. Anything it puts in the `$out` directory is considered the results of the step

This direvation depends on `$gcc`, `$bash` those will be built before this deriviation is run. The paths
are  set  to where the results of the depedencies are in the store.


Note that the "builder" is just a shell script

```bash

export PATH="$coreutils/bin:$gcc/bin"
mkdir $out
gcc -o $out/simple $src
```

## GitHub Actions

Dosen't have the notion of composeability of build results, it's very imperative.  But you can use create an action
which is a gitrepo with some javascript, a yaml file  and possibly a Dockerfile. ONe action can refer to another
action by `org`/`repo`@`git-ref` name.

They also have a matrix strategy which runs the action for various platforms.

```
on: push
jobs:
  test:
    strategy:
      matrix:
        platform: [ubuntu-latest, macos-latest, windows-latest]
    runs-on: ${{ matrix.platform }}
    steps:
    - uses: actions/checkout@master
    - uses: actions/setup-node@master
      with:
        version: 12
    - run: npm install-ci-test
    - uses:
 ```




[Previous: Goals](prior-art.md) 
[Next: Press Release](press-release.md) 
