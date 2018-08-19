# Publish new NPM version for package

## Setup
Copy the authorization token from the _.npmrc_ file and add it in GitLab as a [CI/CD variable](https://docs.gitlab.com/ce/ci/variables/README.html#variables) named **NPM_TOKEN**.

## .gitlab-ci-yml
```yaml
image: node:latest

stages:
- release

publish:
  stage: release
  only:
  - tags
  - triggers
  script:
  - npm run build
  - echo '//registry.npmjs.org/:_authToken=${NPM_TOKEN}'>.npmrc
  - npm publish
```

## Files
* [.gitlab-ci.yml](.gitlab-ci.yml)

## Links
* https://www.exclamationlabs.com/blog/continuous-deployment-to-npm-using-gitlab-ci/