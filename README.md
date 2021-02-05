# ShipperD Operator
ShipperD is currently in early proof-of-concept development.

### Objective
ShipperD provides a kubernetes native, simple human interface, to upload and update arbitrary image collections via self contained, standardized bundle packages. This operator's primary function is to serve as a single point of entry for disconnected container image upload and publishing, and is built to fill the disconnected/airgap cluster use case missing from the OCI Distribution Spec.

[OCI distribution-spec](https://github.com/opencontainers/distribution-spec) disconnected bundle prototypes are currently created by [Koffer](https://github.com/CloudCtl/Koffer) and driven by it's [various plugins](https://github.com/CodeSparta).

### Painpoints include pre-platform & pre-infrastructure blockers:
  - need for invented image distribution approach
    - self serving images over nginx/registry service is a barrier to clean automation
    - pre-priming (via skopeo or podman/docker pull/push cmds) does not scale
  - fragmented approaches and patterns induce a wide range of outcomes and
    failure/troubleshooting vectors which significantly lengthen runway to
    success from environment to environment and version to version

### MVP Operator Criteria
##### Image Bundle
  - Universal Gather & Carry Format (UGCF) aka Prototype Proposal OCI Distribution Spec Disconnected RFE POC
  - Enablement support for all image types including:
    - [x] [Red Hat OpenShift Platform Container Images](https://mirror.openshift.com/pub/openshift-v4/clients/ocp/latest/release.txt) (by name@sha:digest)
    - [x] [RedHat Operators Catalog Container Images](https://github.com/CodeSparta/collector-operators) (by name@sha:digest)
    - [x] [Arbitrary Container Image Lists](https://github.com/CodeSparta/collector-apps) (by name@sha:digest and/or name:tag)
  - Serving via UGCF bundle Supportible via RH OCP IPI Bootstrap capability
  - Deploy Time & Post Deploy Cluster/Operator/Application serve / update / upgrade via UGCF 

##### Operator
  - Automated squashfs bundle unpack & upload
  - UGCF Bundle upload via http(s) enabled
  - UGCF Bundle upload via `oc rsync` enabled
  - OCP Cluster Internal Registry as first MVP
  - Path to support cluster external & on cluster alternate registries (harbor/quay/etc)
  - Path to support action on bundle metadata from upload/unpack/push event (webhook, etc)
