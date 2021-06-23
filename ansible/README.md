# Ansible lint, test and playbook

## Setup
>No setup required

## .gitlab-ci.yml

```yaml
image: kromz/ansible:latest

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

* [Repository at GitHub](https://github.com/krom/ansible-docker)
* [Repository at Docker Hub](https://hub.docker.com/r/kromz/ansible/)
