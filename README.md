# JMAllen.net

Personal home page for JMA, driven by [Hugo CMS](https://gohugo.io)

Published at https://jmallen.net, via GitHub pages

[![Deploy Hugo site to GitHub Pages](https://github.com/ubahmapk/jmallen/actions/workflows/hugo.yaml/badge.svg?branch=main&event=push)](https://github.com/ubahmapk/jmallen/actions/workflows/hugo.yaml)

## Install

```shell
brew install hugo
```

## Development

1. Build the static pages

Run from the root of the repo:

```shell
hugo --minify --loglLevel info --destination public/
```

2. Validate the site works / displays as expected

## Deployment

1. Tag a commit on the main branch

2. Check [Github Actions](https://github.com/ubahmapk/jmallen/actions) page for results

3. Fix whatever broke and try again 🤷‍♂️️

## Previous deployment instructions for hosting at AWS S3+CloudFront

1. Build the static pages

Run from the root of the repo:

```shell
hugo --minify --loglLevel info --destination public/
```

2. Validate Actions

`env_file` contains the 1Password "secret link" to the AWS Private Access Key and AWS Secret Access Key vault items. We can inject those values into the environment for deployment:

First, validate the actions to be taken, using the `--dryRun` flag:

```shell
op run --env-file env_file -- hugo deploy --confirm --dryRun --target production
```

3. Deploy

```shell
op run --env-file env_file -- hugo deploy --confirm --target production
```

By default, the deployment will invalidate the Cloudfront distro cache. Add the flag `--invalidateCDN=false` to the deploy command above to avoid that, if required.
