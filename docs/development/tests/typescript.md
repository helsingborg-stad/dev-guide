---
title: "Javascript unit tests"
date: 2021-09-23
draft: false
layout: default
parent: Tests
grand_parent: Development
---

# Javascript unit tests

## Tools and commands

### Jest
We use [Jest](https://jestjs.io/) for our javascript unit tests.

#### Install
Install Jest with yarn.
``` bash
yarn add --dev jest
```

In `package.json` add the test execute command to scripts section.

``` json
{
  "name": "test-project",
  "version": "0.0.1",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "node node_modules/.bin/jest"
  },
  "keywords": [],
  "author": "Helsingborg Stad",
  "license": "MIT",
  "dependencies": {}
}
```
Configuration to set code coverage thresholds.  
`jest.config.js`
``` javascript
module.exports = {
  transform: {
    '^.+\\.[t|j]sx?$': 'babel-jest',
  },
};
```

### Folder structure and file name convention
Example folder structure for test and test subjects.
File names for test should be subject.test.php and follow the source folder structure.  
ex.  
```
project
│   package.json   
│   jest.config.js
│
└───test
│   │
│   └───lambdas
│   │   │   main.test.js
│   │   │   ...
│   │
│   └───helpers
│       │   calculate.test.js
│       │   ...
│
└───lambdas
│   │ main.js
│   │ ...
│ 
└───helpers
    │ calculate.js
    │ ...
```


## Pull Request testing
To indicate test have failed on a Github Pull Request.  

![GitHub Unit Test check](images/github-check-unit-test.png "github-check-unit-test.png")  

Add a Github Action to run the test command on Pull Requests tergeting dev branch.  
`.github/workflow/pre-merge-tests.yaml`
```yaml 
name: pull-request
on:
  pull_request:
    branches: [ dev ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
      - uses: actions/checkout@v2

      - name: Set up node 
        uses: actions/setup-node@v1

      - name: Install dependencies
        run: yarn

      - name: Run tests 
        run: yarn run test
```

## Test coverage
