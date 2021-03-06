# Node Project Manually Patch Demo

![Node CI](https://github.com/Soontao/node-patch-demo/workflows/Node%20CI/badge.svg)

This is a nodejs patch fix demo project, with the [patch-package](https://github.com/ds300/patch-package) tool.

This project is directly dependent with the `lodash@4.17.14`, but its dependencies are dependent with the `lodash@4.17.15`, so developers must patch the lodash package in deep `node_modules`.

## Demo Patch

> this project how to apply patches

1. clone & install this project
1. run `npm install`, this project will install dependencies, then apply patches automatically
1. run `npm test`, all test cases will be passed

## Re-produce vulnerability

> there is a `prototype pollution` vulnerability in `lodash`

1. run `npm run reverse`, reverse all patches
1. run `npm test`, test will be failed, because the original libraries are broken

## How to patch

1. list all `broken` dependencies (direct/in-direct) by `npm ls {name}`
1. manually update source code in `node_modules` one by one
1. run `npx patch-package {module path}` to generate patch files in `patches` directory
1. setup tools for the broken project, ref the [document](https://github.com/ds300/patch-package#set-up)

## Comments

* this solution will not apply any changes on `package.json` or `package-lock.json` or `shrinkwrap.json`, as a result, your dependency check tools (like `whitesource`) still will report alerts
* for the recent prototype pollution issue, developers need to fix both the `_baseSet.js` & `lodash.js (pre-built bundle)` files.

## Project `Lodash` Dependencies
```
$ npm ls lodash
patch-demo@0.0.1 /Users/i337313/repos/node-patch-demo
├─┬ @commitlint/config-conventional@8.3.4
│ └─┬ conventional-changelog-conventionalcommits@4.2.1
│   └── lodash@4.17.14  deduped
├─┬ @typescript-eslint/eslint-plugin@2.34.0
│ └─┬ @typescript-eslint/experimental-utils@2.34.0
│   └─┬ @typescript-eslint/typescript-estree@2.34.0
│     └── lodash@4.17.15 
├─┬ @typescript-eslint/parser@2.34.0
│ └─┬ @typescript-eslint/typescript-estree@2.34.0
│   └── lodash@4.17.15 
├─┬ commitlint@8.3.5
│ └─┬ @commitlint/cli@8.3.5
│   ├─┬ @commitlint/lint@8.3.5
│   │ ├─┬ @commitlint/parse@8.3.4
│   │ │ └── lodash@4.17.14  deduped
│   │ ├─┬ @commitlint/rules@8.3.4
│   │ │ └─┬ @commitlint/ensure@8.3.4
│   │ │   └── lodash@4.17.15 
│   │ └── lodash@4.17.15 
│   ├─┬ @commitlint/load@8.3.5
│   │ ├─┬ @commitlint/resolve-extends@8.3.5
│   │ │ └── lodash@4.17.15 
│   │ └── lodash@4.17.15 
│   └── lodash@4.17.15 
├─┬ eslint@6.8.0
│ ├─┬ inquirer@7.1.0
│ │ └── lodash@4.17.15 
│ ├── lodash@4.17.14  deduped
│ └─┬ table@5.4.6
│   └── lodash@4.17.14  deduped
├─┬ jest@26.0.1
│ └─┬ @jest/core@26.0.1
│   ├─┬ @jest/transform@26.0.1
│   │ └─┬ @babel/core@7.10.2
│   │   ├─┬ @babel/generator@7.10.2
│   │   │ └── lodash@4.17.14  deduped
│   │   ├─┬ @babel/helper-module-transforms@7.10.1
│   │   │ └── lodash@4.17.14  deduped
│   │   ├─┬ @babel/traverse@7.10.1
│   │   │ └── lodash@4.17.14  deduped
│   │   └── lodash@4.17.14  deduped
│   ├─┬ jest-config@26.0.1
│   │ └─┬ jest-environment-jsdom@26.0.1
│   │   └─┬ jsdom@16.2.2
│   │     └─┬ request-promise-native@1.0.8
│   │       └─┬ request-promise-core@1.1.3
│   │         └── lodash@4.17.15 
│   └─┬ jest-snapshot@26.0.1
│     └─┬ @babel/types@7.10.2
│       └── lodash@4.17.14  deduped
├── lodash@4.17.14 
└─┬ standard-version@8.0.0
  ├─┬ conventional-changelog@3.1.18
  │ ├─┬ conventional-changelog-conventionalcommits@4.3.0
  │ │ └── lodash@4.17.15 
  │ └─┬ conventional-changelog-core@4.1.7
  │   ├─┬ conventional-changelog-writer@4.0.16
  │   │ └── lodash@4.17.15 
  │   └── lodash@4.17.15 
  ├─┬ conventional-changelog-conventionalcommits@4.2.3
  │ └── lodash@4.17.15 
  └─┬ conventional-recommended-bump@6.0.5
    └─┬ conventional-commits-parser@3.1.0
      └── lodash@4.17.15 
```
