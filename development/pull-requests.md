# Pull Requests

## Branch protection rules
A pull request against any of our Deploy branches should always be approved by at least two developers before merging.

### Deploy branches.
When merging into any of the below branches, a deploy will start.  
  
| branch  | Enviroments             |
| ------- | ----------------------- |
| dev     | develop                 |
| master  | stage, test, production |
| release | release                 |

## Pull request template
```
## Feature description
Clearly and concisely describe the feature.

## Solution description
Describe your code changes in a more technical detailed for reviewers.

## What areas is affected by these changes?.
What part of the code base is affected by these changes.

## Is there any excisting behavior change of other features due to this code change?
Mention Yes or No. If Yes, provide the appropriate explanation.

## Covered unit tests cases / E2E test cases?
Whether unit test cases or E2E test cases recorded for this feature?

## Are your code structured in a way so that reviewers can understand it?
Mention Yes or No. If No, provide a reason for the complexity.

## Was this feature tested in the following environments?
- [x] Your personal AWS environment.
- [x] Your local Serverless environment.

```


