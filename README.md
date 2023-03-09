# gda-test-gap

This GitHub action tests GAP with the GAP package located in the current directory.


## Usage

This action can optionally be called in the workflow of a GAP package to run the GAP tests.

### Inputs
  - `COMPLETE`:
    * Use the more complete (but slower) teststandard.g instead of testinstall.g
    * default: `false`
    * required: `false`
  - `ONLY_NEEDEDE`:
    * Only load necessary packages, not suggested ones, prior to testing
    * default: `false`
    * required: `false`
  - `ALL_PACKAGES`:
    * Load all packages prior to testing
    * default: `false`
    * required: `false`

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

    container:
      image: ghcr.io/stertooy/gda-image:master-slim

    steps:
      - uses: actions/checkout@v3
      - uses: stertooy/gda-build-pkg@v1
      - uses: stertooy/gda-test-gap@v1
```
