# GitHub Actions Runner Images

See the [official GitHub Actions Runner repository](https://github.com/actions/runner) for additional information.

See the [Actions Runner Controller release documentation](https://github.com/actions/actions-runner-controller/blob/master/docs/adrs/2022-10-17-runner-image.md) for more information regarding the Dockerfile and how it may be used to produce self-hosted Actions runners. These runners may be used in conjuction with ARC and Kubernetes.

## Dockerfile

The `Dockerfile` in this repository was copied from the official GitHub `actions/runner` repository. That Dockerfile may be found here:

https://github.com/actions/runner/blob/main/images/Dockerfile

### Arguments

The Dockerfile requires the following arguments to build an image. Some arguments have defaults specified within the Dockerfile.

Arguments for a Linux image:

```
TARGETOS=linux
TARGETARCH=amd64
RUNNER_VERSION=2.308.0
RUNNER_CONTAINER_HOOKS_VERSION=0.3.2
DOCKER_VERSION=23.0.6
```

## Build Image

Run the following command from the project base directory to build a Linux action runner.

```
docker build \
  --build-arg TARGETOS=linux \
  --build-arg TARGETARCH=amd64 \
  --build-arg RUNNER_VERSION=2.308.0 \
 --tag mwarman/gh-actions-runner-linux:latest \
 .
```
