# Ansible lint, test and playbook

## Setup
>No setup required

## .gitlab-ci.yml

```yaml
image: kudlayry/ansible:latest

stages:
  - test
  - deploy

test:
  stage: test
  script:
    - ansible-lint playbook.yml
    - ansible-playbook --check playbook.yml

deploy:
  stage: deploy
  only:
    - master
  environment:
    name: Dev
  script:
    - ansible-playbook playbook.yml
```

## Files
* [.gitlab-ci.yml](.gitlab-ci.yml)

## Links

* https://github.com/krom/ansible-docker