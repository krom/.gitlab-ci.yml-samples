# Various node versions

### .gitlab-ci.yml full version with linter and audit

```yaml
image: node:latest

# Setup stages
stages:
- lint
- test
- audit
- release


lint:
  stage: lint
  script:
  - npm install
  - npm run lint

test:node:10:
  stage: test
  image: node:10
  script:
  - npm install
  - npm run test

test:node:8:
  stage: test
  image: node:8
  script:
  - npm install
  - npm run test

test:node:6:
  stage: test
  image: node:6
  script:
  - npm install
  - npm run test

test:node:4:
  stage: test
  image: node:4
  script:
  - npm install
  - npm run test

audit:
  stage: audit
  script:
  - npm install
  - npm audit

```

## Links

* https://www.exclamationlabs.com/blog/continuous-deployment-to-npm-using-gitlab-ci/