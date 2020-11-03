# Continous Integration Setup

**Group members**  
Rasmus Helsgaun  
Jonas Valentin Björk Hein  
Jonatan Magnus Klarskov Bakke  
Stephan Djurhuus  
Thomas Stevns Nielsen Ebsen  
Alex Langhoff  
Adam Lass  
Andreas Due Jørgensen  
Pernille Lørup

![Node.js CI with yarn](https://github.com/TEAM-B-SOFT2020/ci-test/workflows/Node.js%20CI%20with%20yarn/badge.svg)

[See Github Actions here](https://github.com/TEAM-B-SOFT2020/ci-test/actions)

### Github Actions with Node.js

The yaml file below is used as a setup file for Github Actions.  
It supports the following operation systems: Mac OS, Windows, Ubuntu.  
As a reference we have used the following [link](https://docs.github.com/en/free-pro-team@latest/actions/guides/building-and-testing-nodejs)

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

As a test framework we are using Jest made by Facebook. Two examples of tests is written below. We have a passing test and a failing test, which is why our Github Actions Badge above is presented as failing.

**Passing test**

```typescript
test("two plus two is four", () => {
  expect(2 + 2).toBe(4);
});
```

**Failing test**

```typescript
test("name is egon", () => {
  expect("muhammed").toEqual("egon");
});
```
