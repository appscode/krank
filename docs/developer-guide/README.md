## Development Guide
This document is intended to be the canonical source of truth for things like supported toolchain versions for building Krank.
If you find a requirement that this doc does not capture, please submit an issue on github.

This document is intended to be relative to the branch in which it is found. It is guaranteed that requirements will change over time
for the development branch, but release branches of Krank should not change.

### Build Krank
Some of the Krank development helper scripts rely on a fairly up-to-date GNU tools environment, so most recent Linux distros should
work just fine out-of-the-box.

#### Setup GO
Krank is written in Google's GO programming language. Currently, Krank is developed and tested on **go 1.8.3**. If you haven't set up a GO
development environment, please follow [these instructions](https://golang.org/doc/code.html) to install GO.

#### Download Source

```console
$ go get github.com/appscode/krank
$ cd $(go env GOPATH)/src/github.com/appscode/krank
```

#### Install Dev tools
To install various dev tools for Krank, run the following command:

```console
# setting up dependencies for compiling krank...
$ ./hack/builddeps.sh
```

#### Build Binary
```
$ ./hack/make.py
$ krank version
```

#### Dependency management
Krank uses [Glide](https://github.com/Masterminds/glide) to manage dependencies. Dependencies are already checked in the `vendor` folder.
If you want to update/add dependencies, run:
```console
$ glide slow
```

#### Build Docker images
To build and push your custom Docker image, follow the steps below. To release a new version of Krank, please follow the [release guide](/docs/developer-guide/release.md).

```console
# Build Docker image
$ ./hack/docker/krank/setup.sh; ./hack/docker/krank/setup.sh push

# Add docker tag for your repository
$ docker tag appscode/krank:<tag> <image>:<tag>

# Push Image
$ docker push <image>:<tag>
```

#### Generate CLI Reference Docs
```console
$ ./hack/gendocs/make.sh
```