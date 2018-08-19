# Publish at Firebase hosting

## Setup

1. **FIREBASE_TOKEN** TBD

## .gitlab-ci.yml

```yaml
image: node:latest

cache:
  paths:
  - node_modules/

deploy:production:
  stage: deploy
  environment:
    name: Production
    url: https://your-app.firebaseapp.com/
  only:
  - master
  script:
  - npm install -g firebase-tools
  - npm install
  - npm run build
  - firebase use --token $FIREBASE_TOKEN production
  - firebase deploy --only hosting -m "Pipeline $CI_PIPELINE_ID, build $CI_BUILD_ID" --non-interactive --token $FIREBASE_TOKEN

```

## Links

* https://gist.github.com/rambabusaravanan/4907ea46d814bc69002c6f011ae6dd48
* https://medium.com/@rambabusaravanan/firebase-hosting-deployment-automation-with-gitlab-ci-f3fad9130d62