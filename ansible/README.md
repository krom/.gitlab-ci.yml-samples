# Ansible lint and playbook

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

## Links

* https://github.com/krom/ansible-docker