# foxglove-studio-rock

[ROCKs](https://canonical-rockcraft.readthedocs-hosted.com/en/latest/) for [Foxglove Studio](https://foxglove.dev/studio).
This repository holds all the necessary files to build ROCKs for the upstream versions we support. The Foxglove Studio ROCK is used by the [foxglove-studio-operator](https://github.com/ubuntu-robotics/foxglove-k8s-operator) charm.

The ROCKs on this repository are built with [OCI Factory](https://github.com/canonical/oci-factory/), which also takes care of periodically rebuilding the images.

Automation takes care of:

* validating PRs, by simply trying to build the ROCK
* pulling upstream releases, creating a PR with the necessary files to be manually reviewed
<!-- * releasing to GHCR at [ghcr.io/canonical/foxglove-studio:dev](https://ghcr.io/canonical/foxglove-studio:dev), when merging to main, for development purposes. -->
