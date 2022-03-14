---
title: "JS/TS - ESLint"
date: 2021-05-27
draft: false
layout: default
grand_parent: Development
parent: Linters
---

# JavaScript

[ESLint](https://eslint.org/) is used as a static analyzing tool for JavaScript/TypeScript projects.

## Configuration

Latest reference ESLint config for React-Native project is available [here](https://github.com/helsingborg-stad/app-mitt-helsingborg/blob/develop/.eslintrc.js).

The base of the ESLint config uses the [Airbnb](https://www.npmjs.com/package/eslint-config-airbnb) config, with additional rules on top for [Jest](https://www.npmjs.com/package/eslint-plugin-jest), [React](https://www.npmjs.com/package/eslint-plugin-react) and [TypeScript](https://github.com/typescript-eslint/typescript-eslint) when needed.

[Prettier](https://github.com/prettier/eslint-config-prettier) rules are applied last as Prettier is used for formatting the code. This turns off certain ESLint rules and ensures that no stylistic errors are reported by ESLint, enabling the developer to focus on more impactful errors.

## Code editor Extensions

In order to enforce linting of code automatically for developers it is recommended to install the ESLint extensions for your IDE if available.

### Visual Studio Code

[Link to ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

It is recommended to set `source.fixAll: true` as a save-action so that VSCode automatically fixes fixable linting errors on save.

It is also recommended to also install the [Prettier extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) and set code to format on save.

[Link to sample settings.json for VSCode](https://github.com/helsingborg-stad/app-mitt-helsingborg/blob/develop/.vscode/settings.json)
