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
snap install rockcraft --classic
```

Build the ROCK,

```bash
rockcraft pack
```

Convert it to a Docker image,

```bash
sudo /snap/rockcraft/current/bin/skopeo --insecure-policy copy \
oci-archive:foxglove-studio_*_amd64.rock docker-daemon:foxglove-studio:rock
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

## Shareable links

Build and share deep links with your teammates to open Foxglove
with specific layouts and data sources.

To open Foxglove using a specific layout or data source,
construct a "deep link" URL using the format:

```
https://127.0.0.1:8080/?param1=value2&param2=value2
```

The complete documentation can be found on
[Foxglove shareable links doc](https://docs.foxglove.dev/docs/visualization/shareable-links)

Starting at version 1.87.0, this rock includes [a patch](./1.87.0/local/0001-studio-base-workspace-add-layout-data-from-url.patch) allowing custom dynamic layout through the following parameter:

| parameter | type | required | description |
| ----------|------|----------|------------ |
| layoutURL | string | ✓ | URL to layout json file |
