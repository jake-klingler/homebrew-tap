# Honor Homebrew Tap

Why is this not under `joinhonor/homebrew-tap`? Because:
1. Org policy prevents us from creating public repos.
2. Using private GitHub repos with custom brew taps is annoying.
3. A user may not have authenticated with GH by the time they need to install asdf.


## asdf@0.15.0

asdf introduced breaking changes in 0.16.0.

Brew has no easy way of installing specific versions of dependencies.

This is a temporary workaround for our local dev setups until we figure out a more permanent solution.


## scip@9.0.0

[SCIP](https://www.scipopt.org/) is an optimization library used by one of our ML services.
It needs to be installed on the host and is accessed via [pyomo](https://pyomo.readthedocs.io/) directly via the binary.

We need a custom tap to pin a specific version that matches the version installed in the Dockerfile.
This allows us to forego using a devcontainer for local development and develop (and run tests) on the host instead (like all of our other services).

### Optional: build bottle

To prevent all devs from having to build SCIP from source, we host a precompiled binary (homebrew bottle) on GitHub Releases.

To regenerate this bottle for a new version (this uses 9.0.0 as an example):
1. `brew install --build-bottle jake-klingler/tap/scip@9.0.0`.
2. `brew bottle jake-klingler/tap/scip@9.0.0`.
3. manually upload the resulting `.tar.gz` file to a GitHub release.
4. update the `bottle` block of your new formula with the output from step 2.

See the `scip@9.0.0.rb` formula as an example.
