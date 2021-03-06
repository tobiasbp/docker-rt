[![Travis CI](https://img.shields.io/travis/cloos/docker-rt/master.svg)](https://travis-ci.org/cloos/docker-rt/branches)
# Supported tags and respective `Dockerfile` links

-	[`4.0` (4.0/*Dockerfile*)](https://github.com/cloos/docker-rt/blob/master/4.0/Dockerfile)
-	[`4.2` (4.2/*Dockerfile*)](https://github.com/cloos/docker-rt/blob/master/4.2/Dockerfile)
-	[`4.4`, `latest` (4.4/*Dockerfile*)](https://github.com/cloos/docker-rt/blob/master/4.4/Dockerfile)

# What is Request Tracker?

Request Tracker (RT) is an open source issue tracking system.

> https://www.bestpractical.com/rt/

# How to use this image

**This image is intended for development or testing, not for production use.**

```console
$ docker run -it --rm --name rt -p 8080:80 netsandbox/request-tracker
```

Then, access it via `http://localhost:8080` or `http://host-ip:8080` in a browser.

If you want to test your RT Extension with this Docker image with
[Travis CI](https://travis-ci.org/), than add a `.travis.yml` file to your
project with this content:

```yml
language: bash
services: docker

env:
  - RT_VERSION=4.0
  - RT_VERSION=4.2
  - RT_VERSION=4.4

before_install:
  - env | sort
  - image="netsandbox/request-tracker:$RT_VERSION"

install:
    - docker pull $image
    - docker run -d -v $TRAVIS_BUILD_DIR:/rtx --name rt $image
    - docker ps -a

script:
    - docker exec -it rt bash -c "cd /rtx && RELEASE_TESTING=1 perl Makefile.PL && make && make test"
```
