# ShipperD Operator
ShipperD is currently in early proof-of-concept development.

ShipperD is built to fill a gap in the OCI Distribution Spec where needs of
disconnected/restricted kubernetes platforms and workloads are not addressed by
current industry adopted standards.

Primary painpoints observed in this space include pre-platform & pre-infrastructure blockers such as:
  - need for invented image distribution approach
  - self serving images over nginx/registry service is a barrier to clean automation
  - pre-priming (via skopeo or podman/docker pull/push cmds) does not scale

### MVP Criteria
