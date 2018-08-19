# IOS builds

## Setup

> See links below

## .gitlab-ci.yml

```yaml
stages:
  - lint
  - test
  - develop

variables:
  LANG: "en_US.UTF-8"
  LC_ALL: "en_US.UTF-8"

before_script:
  - sudo gem install bundler && bundle update

lint:
  tags:
    - ios
  stage: lint
  script:
    - bundle exec fastlane lint
  only:
    - branches
  except:
    - tags
  artifacts:
    paths:
      - fastlane/swiftlint.html
  allow_failure: false

test:
  tags:
    - ios
  stage: test
  script:
    - bundle exec fastlane test
  only:
    - branches
  except:
    - tags
  artifacts:
    paths:
      - fastlane/tests/
  allow_failure: false

develop:
  tags:
    - ios
  stage: develop
  script:
    - bundle exec fastlane develop
  only:
    - /^develop-.*/
    - develop
  environment:
    name: develop
```

## Files
* [.gitlab-ci.yml](.gitlab-ci.yml)

## Links
* https://medium.com/flawless-app-stories/how-to-set-up-gitlab-continuous-integration-for-ios-projects-without-a-hustle-53c2b642c90f