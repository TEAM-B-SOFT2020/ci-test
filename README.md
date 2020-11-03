# Continous Integration Setup

![Node.js CI with yarn](https://github.com/TEAM-B-SOFT2020/ci-test/workflows/Node.js%20CI%20with%20yarn/badge.svg)

### Github Actions with Node.js

```yaml
name: Node.js CI with yarn

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ${{ matrix.os }}

    strategy:
      matrix:
        os: [macos-latest, windows-latest, ubuntu-latest]
        node-version: [10.x, 12.x, 14.x]

    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js version ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}
      - name: Install dependencies
        run: yarn
      - name: Run tests
        run: yarn test
```
