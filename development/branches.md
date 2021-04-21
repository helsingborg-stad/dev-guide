<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Branches](#branches)
  - [Strategy](#strategy)
    - [Gitflow articles](#gitflow-articles)
  - [Naming convention](#naming-convention)
  - [Release branch naming convention](#release-branch-naming-convention)
  - [Master branch version tagging.](#master-branch-version-tagging)
  - [Deployment](#deployment)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Branches


## Strategy
We are using gitflow as our branching strategy with a temporary stable `release` branch used before merge between `dev` and `master` as dev is considered semi stable with continous updates.
![Gitflow example](images/git-model@2x.png "Gitflow")

### Gitflow articles
[A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)  
[Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

## Naming convention
Our main branch for production code should be called `master`.  
For all other purposes the allowed branch names starts with a prefix, a slash(/) and then you feature name with words seperated by a dash(-).  
ex.
```
feat/example-feature
```
  
List of allowed prefixes:  
| prefix  | Description                                                                                             |
| ------- | --------------------------------------------------------------------------------------------------------|
| feat    | (Feature) A new feature.                                                                                |
| fix     | (Bug fix) A bug Fix.                                                                                    |
| hotfix  | (Hot fix) A fix to patch production code.                                                               |
| docs    | (Documentation) Documentation only changes.                                                             |
| perf    | (Code Refactoring) Code changes that improves performance.                                              |
| wip     | (Work In Progress) A code change that won't be finished soon.                                           |
| test    | (TESTS) Adding missing tests or correcting existing tests.                                              |
| ci      | (Continuous Integrations) Changes to our CI configuration files and scripts (example scope: CircleCi).  |
| build   | (Builds) Changes that affect the build system or external dependencies (example scope: npm).            |
| release | (Release) Preparation of a new production release.                                                      |

## Release branch naming convention
The `release` branches purpose is to be a stable branch to be merged merged with the `master` branch.
release branches is only allowed to have a semantic version as "feature name".  
ex.
```
release/1.0.0
```

## Master branch version tagging.
Whenever any branch whether it´s a `hotfix` or a `release` is merged into master a [SemVer](./versioning.md) formed tag should be added to mark the merge.  

## Deployment
When a pull request is accepted and merged into any of the below branches a deploy pipeline will trigger pushing the accepted PR to different environments.  

| branch  | Environments            |
| ------- | ------------------------|
| dev     | develop                 |
| master  | stage, test, production |
| release | release                 |