# ShipperD Operator
###### *ShipperD is currently in early proof-of-concept development.

### Objective
ShipperD provides a kubernetes native, simple human interface to upload and update arbitrary image collections via self contained offline carry friendly packages. This operator's primary function is to serve as a purpose built point of entry for disconnected container image uploading and publishing. The Koffer + ShipperD model was created to fill the restricted, disconnected, and airgap cluster use cases currently missing from the OCI Distribution Spec.

[OCI distribution-spec](https://github.com/opencontainers/distribution-spec) disconnected bundle prototype reference builds are currently built by [Koffer](https://github.com/CloudCtl/Koffer) and driven by it's [various plugin examples](https://github.com/CodeSparta).

### Where does Koffer + ShipperD make sense?    
Active Field use cases and artifact types where this model is being practiced include:
  - Local artifact mirror caching in connected cluster deployments (WAN bandwidth bottleneck remediation)
  - Day Zero/One offline artifact image mirror for Restricted/Airgaped platform deployment.
  - Day Two offline artifact image mirror augmentation, update, and upgrade
  - For oci container images including Platfom Infra, Operator, and arbitrary application images

### Issue Proposition:
Some painpoints ShipperD attempts to address include pre-platform & pre-infrastructure blockers:
  - need for unique image distribution approaches and inventiveness
    - self serving images over nginx/registry service is a barrier to clean automation
    - pre-priming (via skopeo or podman/docker pull/push cmds) does not scale
  - fragmented approaches and patterns induce a wide range of outcomes and
    failure/troubleshooting vectors which significantly lengthen runway to
    success from environment to environment and version to version

### MVP Operator Criteria
##### Image Bundle
  - Universal Gather format (ee - oo - Gee) aka Prototype Proposal OCI Distribution Spec Disconnected RFE POC
  - Enablement support for all image types including:
    - [x] [Red Hat OpenShift Platform Container Images](https://mirror.openshift.com/pub/openshift-v4/clients/ocp/latest/release.txt) (by name@sha:digest)
    - [x] [RedHat Operators Catalog Container Images](https://github.com/CodeSparta/collector-operators) (by name@sha:digest)
    - [x] [Arbitrary Container Image Lists](https://github.com/CodeSparta/collector-apps) (by name@sha:digest and/or name:tag)
  - Serving via UGF bundle Supportible via RH OCP IPI Bootstrap capability
  - Deploy Time & Post Deploy Cluster/Operator/Application serve / update / upgrade via UGF 

##### Operator
  - Automated squashfs bundle unpack & upload
  - UGF Bundle upload via http(s) enabled
  - UGF Bundle upload via `oc rsync` enabled
  - OCP Cluster Internal Registry as first MVP
  - Path to support cluster external & on cluster alternate registries (harbor/quay/etc)
  - Path to support action on bundle metadata from upload/unpack/push event (webhook, etc)
