# foxglove-studio-rock

[ROCKs](https://canonical-rockcraft.readthedocs-hosted.com/en/latest/) for [Foxglove Studio](https://foxglove.dev/studio).
This repository holds all the necessary files to build ROCKs for the upstream versions we support. The Foxglove Studio ROCK is used by the [foxglove-studio-operator](https://github.com/ubuntu-robotics/foxglove-k8s-operator) charm.

The ROCKs on this repository are built with [OCI Factory](https://github.com/canonical/oci-factory/), which also takes care of periodically rebuilding the images.

Automation takes care of:

* validating PRs, by simply trying to build the ROCK
* pulling upstream releases, creating a PR with the necessary files to be manually reviewed
<!-- * releasing to GHCR at [ghcr.io/canonical/foxglove-studio:dev](https://ghcr.io/canonical/foxglove-studio:dev), when merging to main, for development purposes. -->

## Quick start

Install rockcraft,

```bash
snap install rockcraft
```

Build the ROCK,

```bash
rockcraft pack
```

Convert it to a Docker image,

```bash
sudo /snap/rockcraft/current/bin/skopeo --insecure-policy copy
oci-archive:foxglove-studio_1.0_amd64.rock docker-daemon:foxglove-studio:rock
```

Verify that the image is now available,

```bash
docker image list
```

Launch a foxglove-studio instance,

```bash
docker run --rm --name studio -p 127.0.0.1:8080:8080 foxglove-studio:rock
```

And open your web browser at `http://localhost:8080`.

<!-- @todo -->
<!-- http://localhost:8080/?ds=remote-file&ds.url= -->