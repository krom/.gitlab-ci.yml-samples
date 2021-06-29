# Publish at AWS S3

## Setup

1. **AWS_ACCESS_KEY_ID** TBD
1. **AWS_SECRET_ACCESS_KEY** TBD

## .gitlab-ci.yml

```yaml
deploy:
  image: python:latest
  stage: deploy
  before_script:
  - pip install awscli
  script:
    - aws s3 cp ./build s3://${BUCKET_NAME} --recursive --acl public-read
  ##  -  Invalidate cache if you use CloudFront
  #  - aws cloudfront create-invalidation --distribution-id $DISTRIBUTION_ID --paths "/*"
  environment:
    name: ${CI_COMMIT_REF_SLUG}
    url: http://${BUCKET_NAME}.s3-website.${AWS_DEFAULT_REGION}.amazonaws.com
  only:
  - development
```
## Files
* [.gitlab-ci.yml](.gitlab-ci.yml)

## Links
