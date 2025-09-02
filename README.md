# run-gap-tests

This GitHub action runs the GAP test-suite after loading the GAP package located in the current directory. Based on [gap-actions/run-pkg-tests](https://github.com/gap-actions/run-pkg-tests).


## Usage

The action `run-gap-tests` has to be called by the workflow of a GAP package.
By default it runs the file `tst/testinstall.g`.

Its behaviour can be customized via the inputs below.

### Inputs
  - `complete`:
    * Use the more complete (but slower) `teststandard.g` instead of `testinstall.g`
    * default: `false`
    * required: `false`
- `mode`:
  - Value that determines which packages are loaded before the package is tested. The possible values
    are `'default'`, `'onlyneeded'` or `'loadall'`. The option `'default'` loads GAP with default
    set of package; `'onlyneeded'` loads only the needed dependencies of the package being tested;
    `'loadall'` executes `LoadAllPackages()` before the package being tested.
  - default: `'default'`
- `pre-gap`:
  - Prefix for the `GAP` shell variable used by this action to launch GAP (e.g.
    setting this to `valgrind --trace-children=yes --leak-check=full` will run
    GAP through valgrind)'
  - default: `''`
- `warnings-as-errors`:
  - Boolean that determines whether any warnings produced whilst loading the package will be treated as errors.
  - default: `'true'`

### Example

```yaml
name: CI

on:
  - push
  - pull_request
  - workflow_dispatch

jobs:
  build:
    name: "Build the GAP package"
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5
      - uses: gap-actions/setup-gap@v2
      - uses: gap-actions/build-pkg@v1
      - uses: stertooy/run-gap-tests@v1
```

## Contact

Please submit bug reports, suggestions for improvements and patches via
the [issue tracker](https://github.com/stertooy/run-gap-tests/issues).

## License

The action `run-gap-tests` is free software; you can redistribute
and/or modify it under the terms of the GNU General Public License as published
by the Free Software Foundation; either version 2 of the License, or (at your
opinion) any later version. For details, see the file `LICENSE` distributed
with this action or the FSF's own site.
