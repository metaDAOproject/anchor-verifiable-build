# Anchor Verifiable Build

![License MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

An action for generating verifiable [Anchor](https://www.anchor-lang.com/) builds.

## Usage

### Example workflow

Here's an example workflow:

```yaml
name: update-verifiable-build
on: [push]
jobs:
  run-anchor-test:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v3
      - uses: metadaoproject/anchor-verifiable-build@v0.2
        with:
          program: 'autocrat_v0'
          anchor-version: '0.29.0'
          solana-cli-version: '1.17.16'
      - run: cp target/deploy/autocrat_v0.so ./verifiable-builds
      - name: Commit verifiable build if it's different from what exists
        uses: EndBug/add-and-commit@v9.1.4
        with:
          default_author: github_actions
          message: 'Update verifiable build'
```

This workflow generates verifiable builds for 'autocrat_v0' and stores them in the verifiable-builds folder.

## Credits

This is a modification of Helium's [build verified action](https://github.com/helium/helium-program-library/blob/68da8e38e769a22bca0492156695b9677978d139/.github/actions/build-verified/action.yaml#L1verified) that they use internally.
