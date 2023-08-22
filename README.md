# GitHub Actions Runner Images

See the [official GitHub Actions Runner repository][actions-runner] for additional information.

See the [Actions Runner Controller release documentation][arc-image] for more information regarding the Dockerfile and how it may be used to produce self-hosted Actions runners. These runners may be used in conjuction with ARC and Kubernetes.

## Dockerfile

The `Dockerfile` in this repository was copied from the official GitHub `actions/runner` repository. That Dockerfile may be found here:

https://github.com/actions/runner/blob/main/images/Dockerfile

### Arguments

The Dockerfile requires the following arguments to build an image. Some arguments have defaults specified within the Dockerfile.

Arguments for a Linux image:

```bash
TARGETOS=linux
TARGETARCH=amd64
RUNNER_VERSION=2.308.0
RUNNER_CONTAINER_HOOKS_VERSION=0.3.2
DOCKER_VERSION=23.0.6
```

## Build Image

Run the following command from the project base directory to build a Linux action runner.

```bash
docker build \
  --build-arg TARGETOS=linux \
  --build-arg TARGETARCH=amd64 \
  --build-arg RUNNER_VERSION=2.308.0 \
 --tag mwarman/gh-actions-runner-linux:latest \
 .
```

## Pod Spec

This is an example of a pod spec with the init container copying assets to the runner directory.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: <name>
spec:
  containers:
    - name: runner
      image: <image>
      command: ['/runner/run.sh']
      volumeMounts:
        - name: runner
          mountPath: /runner
  initContainers:
    - name: setup
      image: <image>
      command: ['sh', '-c', 'cp -r /actions-runner/* /runner/']
      volumeMounts:
        - name: runner
          mountPath: /runner
  volumes:
    - name: runner
      emptyDir: {}
```

## Related Information

[GitHub Actions Runner][actions-runner]  
[Action Runner Controller][arc]  
[Producing Runner Images][arc-image]  
[GitHub Actions Runner Dockerfile][actions-runner-dockerfile]

[actions-runner]: https://github.com/actions/runner
[actions-runner-dockerfile]: https://github.com/actions/runner/blob/main/images/Dockerfile
[arc]: https://github.com/actions/actions-runner-controller
[arc-image]: https://github.com/actions/actions-runner-controller/blob/master/docs/adrs/2022-10-17-runner-image.md
