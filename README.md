# JMAllen.net

Personal home page for JMA, driven by [Hugo CMS](https://gohugo.io)

Published at https://jmallen.net, via AWS S3 static hosting behind an AWS Cloudfront distribution.

## Install

```shell
brew install hugo
```

## Deployment

1. Build the static pages

Run from the root of the repo:

```shell
hugo --minify --loglLevel info --destination public/
```

2. Upload site to AWS S3

`env_file` contains the 1Password "secret link" to the AWS Private Access Key and AWS Secret Access Key vault items. We can inject those values into the environment for deployment:

First, validate the actions to be taken, using the `--dryRun` flag:

```shell
op run --env-file env_file -- hugo deploy --confirm --dryRun --target production
```

Then, **actually** deploy:

```shell
op run --env-file env_file -- hugo deploy --confirm --target production
```

By default, the deployment will invalidate the Cloudfront distro cache. Add the flag `--invalidateCDN=false` to the deploy command above to avoid that, if required.

