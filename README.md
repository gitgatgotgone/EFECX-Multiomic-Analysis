# EFECX Multiomic Analysis

EFECX (Exhaustive Feature Enrichment by Conservative eXcess) analyses paired
single-cell/nucleus ATAC and gene-expression measurements. It discovers
footprints, tests selected genes against a counter-gene universe, and publishes
authenticated outcome counts and prediction packages.

This source release includes targeted and observed-gene genome-wide initial
workflows, bounded shared-memory concurrent execution, supplied-gene follow-ups,
the serial signed-tally AVL backend, numerical tests and BAM input-preparation
tools. It contains no experimental datasets, lab images, private review records,
Git history, compiled executables or transferable host qualification.

## Source Integrity

Git clones and uploads that do not preserve executable bits are supported: invoke
the tools with their Ruby/Python interpreters. `.gitattributes` prevents newline
conversion of the manifested source. Other source edits require a newly generated
source manifest and fresh qualification; an old receipt does not authorize edits.
Root-level licensing files and Git metadata are outside the runtime manifest.
See the project's LICENSE and `THIRD_PARTY.md` for licensing information.

## Requirements

Use 64-bit Linux, Ruby 3.3.8/JSON 2.7.2 for the current qualified resource profile,
Python 3, GHC 9.10.3, Cabal, LLVM/Clang 15, GCC with ThreadSanitizer, GNU time,
gzip, zstd 1.5.7, sort and sha256sum. GMP, MPFR and OpenSSL development libraries
are required. A stable Linux machine ID and C.UTF-8 locale are used by host checks.
The current resource profile verifies exact supported interpreter/codec builds;
an incompatible installation is rejected rather than silently admitted.

The native setup uses FLINT 3.6.0 production, instrumented reentrant and serial
control prefixes. `source/tools/build_reentrant_flint.rb` builds/reuses the first
two from the upstream source tarball. Its usage is printed without arguments.
The expected tarball SHA-256 is
`b95e2c7792f5eea4a1c8d2d42c4098434756832e57a094b295eb5dfdc9b4c36b`.
That helper currently expects LLVM 15 in `$HOME/.local/opt/llvm-15/bin` and GCC
at `/usr/bin/gcc`. For the serial loader-control prefix, build the same FLINT
source separately with shared libraries and reentrancy disabled. It is only a
negative test, never the production library.

## Build and Qualify

Authenticate the archive checksum before extraction. Manifest checks detect
accidental changes; they are not a cryptographic signature from the publisher.
From the extracted directory or its Git clone:

```sh
ruby bootstrap.rb verify-source
ruby bootstrap.rb --cache "$EFECX_CACHE" --llvm-bin "$LLVM15_BIN" \
  --flint-prefix "$FLINT_PREFIX" \
  --instrumented-flint-prefix "$TSAN_FLINT_PREFIX" \
  --serial-flint-prefix "$SERIAL_FLINT_PREFIX" --jobs 4 prepare
```

All cache/build/output directories must be outside this source directory.
Compilers and missing external packages are installation prerequisites, not
bundled runtimes. Supply `--store "$MATCHING_CABAL_STORE"` to reuse an existing
compatible Haskell package store. Otherwise an external persistent store is
created. Repeated preparation reuses validated builds and local qualification.
No private repository access or Git executable is required by bootstrap.

Preparation runs numerical and application tests, native concurrency checks and
host qualification before printing an `INSTALLATION.json` path. Source integrity
alone does not grant permission to run an unqualified concurrent installation.

```sh
ruby bootstrap.rb --installation "$INSTALLATION" verify
```

See `INPUT_PREPARATION.md` for BAM-derived inputs and `CLI.md` for sample/settings
tables, targeted runs, genome-wide runs and follow-ups. The same source can be
used for a new machine, but the installation receipt cannot be transferred.

## Resource and Scientific Scope

Whole-run targets are input-sized; there is no 128-target split. Active workers,
resident footprints, source/context slots and plan-cache capacity are separate
settings. Input-derived application bounds and separately qualified runtime
allowances inform admission; they are not a proved process-RSS ceiling. Large
worker counts do not require a same-scale benchmark to compute the provision.

The local tests validate implementation behavior, not biological
calibration, causal enhancer assignments or universal performance guarantees.
