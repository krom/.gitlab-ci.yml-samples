# Docker Image for deployment

This image based at Ubuntu and contains:
* ssh-client
* rsync

## Setup

>You may to setup variables via [CI/CD variables]([https://gitlab.com/help/ci/variables/README#variables)
```shell
# SSH Private key 
$DEPLOY_KEY=dadaddasdas
# SSH Fingerprints
$SSH_KNOWN_HOSTS=github.com ssh-rsa AAAAB3NzaC1yc2EAAAAB...
```

## Example of .gitlab-ci.yml

```YAML
image: kromz/deploy-tools:latest

stages:
  - deploy


deploy:
  image: kromz/deploy-tools:latest
  stage: deploy
  only:
    - master
  environment:
    name: Dev
  script:
    - eval $(ssh-agent -s)
    - echo "$DEPLOY_KEY" | tr -d '\r' | ssh-add - > /dev/null
    - mkdir -p ~/.ssh
    - chmod 700 ~/.ssh
    - echo "$SSH_KNOWN_HOSTS" > ~/.ssh/known_hosts
    - chmod 644 ~/.ssh/known_hosts
    - ssh $USER@$HOST uname -a
    - rsync -a public $USER@$HOST:/var/www/public
```

## Commands description


### Start SSH Agent for authentication by SSH Keys
```bash
eval $(ssh-agent -s)
```

### Apply Private SSH Key
```bash
echo "$DEPLOY_KEY" | tr -d '\r' | ssh-add - > /dev/null
```

### Apply fingerprints for remote servers
```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
echo "$SSH_KNOWN_HOSTS" > ~/.ssh/known_hosts
chmod 644 ~/.ssh/known_hosts
```


### Generate fingerprints for $SSH_KNOWN_HOSTS
```bash
ssh-keyscan <remote SSH server>
```
## Files
* [.gitlab-ci.yml](.gitlab-ci.yml)

## Links
* [Repository at GitHub](https://github.com/krom/deploy-tools-docker)
* [Repository at Docker Hub](https://hub.docker.com/r/kromz/deploy-tools/)
