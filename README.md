# BuildDynarePreprocessor_jll

This repository is for testing and tracking changes in the recipe needed to build DynarePreprocessor_jll

When a new version is ready, copy `build_tarballs.jl` to Yggdrasil.jl/D/DynarePreprocessor in your own fork of Yggdrasil and open a PR

The current version uses https://git.dynare.org/Dynare/preprocessor#julia-6.4.0 as the upstream source. This is a fork of the master branch still using autoconf tools before the switch to meson build. There is also some changes to the C++ syntax necessary to allow compilation with the version of LLVM/clang used by `BinaryBuilder.jl` when building for MacOS or FreeBSD.

There are a few small differences in the logic of the code. Among them:
- improvements in the writing of `modfile.json` when the preprocessor is called with option `language=julia`
- relaxing the requirement that all endogenous variables appear in `steady_state_model` block so as to permit to communicate only a partial solution for the steady state

## Running the `build_tarballs.jl` script

- Make sure that `BinaryBuilder.jl` is added to Julia default environment
- To (cross-)compile and build for a basic Linux installation on a x86_64 machine, run from the terminal command line
```
  julia --color=yes  build_tarballs.jl x86_64-linux-gnu --debug --verbose
```
- To cross-compile and build for a x86_64 MacOS installation, run from the terminal command line
```
  julia --color=yes  build_tarballs.jl x86_64-apple-darwin --debug --verbose
```
- To cross-compile and build for all plateforms supported by Julia, run from the terminal command line
```
  julia --color=yes  build_tarballs.jl --debug --verbose
```

## Testing the artifact locally

See the [BinaryBuilder documentation](https://docs.binarybuilder.org/stable/building/#Building-a-custom-JLL-package-locally)

## Cleaning up

The above procedure creates the `build` and `products` directories that you can remove after having verified them if necessary.

## Open issues:
- Finalize the transition to meson build. Solve the problem for MacOS. See branch `meson`.
- Rebase on current state of `master` branch
- See if some of the changes made for Julia should be ported to `master`.
