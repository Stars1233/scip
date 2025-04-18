# ChangeLog

## Unreleased

Rust SCIP bindings:

- Bumped MSRV to Rust 1.81.0 (https://github.com/sourcegraph/scip/pull/316, https://github.com/sourcegraph/scip/pull/313).
- Bumped the pinned version of the `protobuf` crate to
  the latest release v3.7.2.
  (https://github.com/sourcegraph/scip/pull/313)

Go bindings:

- BREAKING CHANGE: IndexVisitor now accepts a context object and returns an error.
  When an error is returned, the visitor short-circuits.

## v0.5.2

SCIP schema:

- Added kind `SymbolInformation.Kind.Concept` for C++ (https://github.com/sourcegraph/scip/pull/305)

## v0.5.1

CLI:

- Cleaned up the formatting for the `test` command.
  (https://github.com/sourcegraph/scip/pull/281)

Rust SCIP bindings:

- Bumped the pinned version of the `protobuf` crate to
  the latest release v3.7.1.
  (https://github.com/sourcegraph/scip/pull/287)

## v0.5.0

CLI:

- Added a `test` command for targeted testing of specific occurrences.
  See the [CLI](docs/CLI.md) and [test file syntax reference](docs/test_file_format.md) for details.
  (https://github.com/sourcegraph/scip/pull/236)
- Breaking changes:
  - Removed the `convert` subcommand for SCIP to LSIF conversion.
    (https://github.com/sourcegraph/scip/pull/275)

Schema:

- Added two new `SymbolKind` variants: `Extension` and `Mixin`.
  (https://github.com/sourcegraph/scip/pull/277)

Go SCIP bindings:

- Added clearer documentation around document canonicalization.
  (https://github.com/sourcegraph/scip/pull/273)
- Breaking changes:
  - Removed SCIP to LSIF conversion functionality.
    (https://github.com/sourcegraph/scip/pull/275)

## v0.4.0

SCIP schema:

- Added documentation that ranges must be half-open intervals.

Go SCIP bindings:

- Breaking changes:
  - The `NewRange` function does well-formedness checks and returns `(Range, error)` instead of `*Range`.
    When skipping checks, `NewRangeUnchecked` can be used instead.
  - The `SortRanges` function takes a `[]Range` instead of a `[]*Range`
    to avoid extra heap allocations.
- Features:
  - Added new methods for `Range` and `Position` types.

## v0.3.3

SCIP schema:

- Added new `PositionEncoding` field to specify how consumers
  should interpret the character offsets.
  (https://github.com/sourcegraph/scip/pull/224, https://github.com/sourcegraph/scip/pull/225)

scip CLI:

- `scip snapshot` output includes the `diagnostics` field.

## v0.3.2

SCIP schema:

- Added new `SymbolRole`: `ForwardDefinition`
  (https://github.com/sourcegraph/scip/pull/217)

scip CLI:

- `scip print` supports turning off colorful output using `--color=false` or
  by setting the environment variable `NO_COLOR=1`.
  (https://github.com/sourcegraph/scip/pull/214)

## v0.3.1

SCIP schema:

- Added new `Kind` enum constants to represent more detailed
  information about different pieces of syntax in different languages.
  (https://github.com/sourcegraph/scip/pull/195,
  https://github.com/sourcegraph/scip/pull/208,
  https://github.com/sourcegraph/scip/pull/209)
- Added new `Language` enum constants.
  (https://github.com/sourcegraph/scip/pull/195,
  https://github.com/sourcegraph/scip/pull/207)
- Minor documentation improvements.
  (https://github.com/sourcegraph/scip/pull/194,
  https://github.com/sourcegraph/scip/pull/206)

scip CLI:

- Added a new `--project-root` flag to `scip stats`.
  (https://github.com/sourcegraph/scip/pull/187)

Go bindings:

- Added missing validation for local symbols when
  parsing a symbol string.
  (https://github.com/sourcegraph/scip/pull/206)
- Fixed a bug related to escaping in symbol formatting.
  (https://github.com/sourcegraph/scip/pull/186)
  (https://github.com/sourcegraph/scip/pull/206)
- Fixed a bug in occurrence canonicalization.
  (https://github.com/sourcegraph/scip/pull/180)
- Fixed some bugs in the new streaming parsing APIs.
  (https://github.com/sourcegraph/scip/pull/176,
  https://github.com/sourcegraph/scip/pull/177)

Rust bindings:

- Added missing validation for local symbols when
  parsing a symbol string.
  (https://github.com/sourcegraph/scip/pull/206)

## v0.3.0

SCIP schema:

- Several new fields were added:
  [`SymbolInformation.signature_documentation`](https://github.com/sourcegraph/scip/pull/159),
  [`SymbolInformation.display_name`](https://github.com/sourcegraph/scip/pull/158),
  [`SymbolInformation.kind`](https://github.com/sourcegraph/scip/pull/156)
  [`Occurrence.enclosing_range`](https://github.com/sourcegraph/scip/pull/150)

scip CLI:

- The `print` subcommand supports a new `--json` flag to emit JSON output
  instead of colored textual output. (https://github.com/sourcegraph/scip/pull/147)
- The `snapshot` subcommand supports a new `--comment-syntax` flag
  to customize the prefix used for inline comments in snapshot output.
  (https://github.com/sourcegraph/scip/pull/139)
- `snapshot` output now include override_documentation for occurrences.
  (https://github.com/sourcegraph/scip/pull/116)

Go bindings:

- Added new APIs to parse SCIP indexes in a streaming
  fashion at Document granularity. This allows consumers
  to process SCIP indexes with better control over memory usage.
  (https://github.com/sourcegraph/scip/pull/172)
- Fixed a panic when descriptors are incomplete
  (https://github.com/sourcegraph/scip/pull/171)

Rust bindings:

- Fixes a bug when emitting symbols which require escaping
  (https://github.com/sourcegraph/scip/pull/169)
- Fixes a bug in handling for macro symbols
  (https://github.com/sourcegraph/scip/pull/145)

## v0.2.3

### Fixes

- Fixed a bug in SCIP to LSIF conversion of indexes using the new `Relationship.is_definition` field. Without this fix, the generated LSIF index would fail to process in Sourcegraph with a "unknown reference to $ID (expected a range)" error. (https://github.com/sourcegraph/scip/pull/108)

## v0.2.2

### Additions

- The new `scip print` subcommand can be used to view a SCIP index without access to protoc. (https://github.com/sourcegraph/scip/pull/91)
- The new `scip lint` subcommand can be used to identify correctness and redundancy issues with a SCIP index. (https://github.com/sourcegraph/scip/pull/92)

### Fixes

- `scip --version` now works as expected instead of reporting 0.1.0. (https://github.com/sourcegraph/scip/pull/97)
