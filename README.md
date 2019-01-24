# Arch on GitHub

[![Build Status](https://travis-ci.com/ajaybhatia/arch-on-github.svg?branch=master)](https://travis-ci.com/ajaybhatia/arch-on-github)

An experiment to create an Arch custom repository, building packages from the
AUR and hosting them via [GitHub Releases](https://help.github.com/articles/about-releases/).

It uses [Travis Cron Jobs](https://docs.travis-ci.com/user/cron-jobs/) to
re-build these packages every day.

## Usage

To use this "repository", include the following in your `/etc/pacman.conf`:

```conf
[github]
SigLevel = Optional TrustAll
Server = https://github.com/ajaybhatia/arch-on-github/releases/download/latest
```

## Building packages

To build the base Docker image used to build our packages and interact with
GitHub's REST endpoints:

```
make build-image
```

To then build our repository, storing the contents in `./repo`:

```
make repo
```

To add or delete packages, simply modify [`packages.txt`](./packages.txt).

In our [`.travis.yml`](./.travis.yml) file, we then delete both the `latest`
release and remote tag and then re-deploy.
