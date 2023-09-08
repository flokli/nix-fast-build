# nix-ci-build

Combine the power of `nix-eval-jobs` with `nix-output-monitor` to supercharge your ci evaluation and building process.

## Why `nix-ci-build`?

**Problem**: Evaluating and building big flakes i.e. with numerous NixOS machines can be painfully slow.

**Our Solution**: `nix-ci-build` offers a seamless experience by evaluating and building your nix packages concurrently, drastically reducing the overall time.

## How Does It Work?

Under the hood:
1. It leverages the output from `nix-eval-jobs` to evaluate flake attributes in parallel.
2. For each flake attribute, a separate `nix-build` process is spawned.
3. Lastly, `nix-output-monitor` to show the build progress nicely.

## Usage

To get started, simply run:

```console
$ nix-ci-build
```

This command will concurrently evaluate and build the attributes `.#checks.$currentSystem`.

---

Enjoy faster and more efficient NixOS builds with `nix-ci-build`!

## Reference

```console
$ nix-ci-build --help
usage: nix-ci-build [-h] [-f FLAKE] [-j MAX_JOBS] [--option OPTION]
                    [--systems SYSTEMS] [--retries RETRIES] [--skip-cached]
                    [--verbose] [--eval-max-memory-size EVAL_MAX_MEMORY_SIZE]
                    [--eval-workers EVAL_WORKERS]

options:
  -h, --help            show this help message and exit
  -f FLAKE, --flake FLAKE
                        Flake url to evaluate/build (default: .#checks
  -j MAX_JOBS, --max-jobs MAX_JOBS
                        Maximum number of build jobs to run in parallel (0 for
                        unlimited)
  --option OPTION       Nix option to set
  --systems SYSTEMS     Comma-separated list of systems to build for (default:
                        current system)
  --retries RETRIES     Number of times to retry failed builds
  --skip-cached         Skip builds that are already present in the binary
                        cache (default: false)
  --verbose             Print verbose output
  --eval-max-memory-size EVAL_MAX_MEMORY_SIZE
                        Maximum memory size for nix-eval-jobs (in MiB) per
                        worker. After the limit is reached, the worker is
                        restarted.
  --eval-workers EVAL_WORKERS
                        Number of evaluation threads spawned
```
