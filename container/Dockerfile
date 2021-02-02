#################################################################################
# Builder Image
FROM quay.io/cloudctl/registry           as registry
FROM registry.access.redhat.com/ubi8/ubi as builder
ARG BUILD_PATH='/rootfs'

#################################################################################
# DNF Package Install List
ARG DNF_LIST="\
  skopeo \
  openssl \
  coreutils-single \
  glibc-minimal-langpack \
"

#################################################################################
# DNF Package Install Flags
ARG DNF_FLAGS="\
  -y \
  --releasever 8 \
  --installroot /rootfs \
"
ARG DNF_FLAGS_EXTRA="\
  --nodocs \
  --setopt=install_weak_deps=false \
  ${DNF_FLAGS} \
"

#################################################################################
# Build Rootfs
RUN set -ex \
     && mkdir -p ${BUILD_PATH} \
     && dnf -y install 'dnf-command(copr)' \
     && dnf -y copr enable rhcontainerbot/container-selinux \
     && curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable.repo https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/CentOS_8/devel:kubic:libcontainers:stable.repo \
     && dnf update ${DNF_FLAGS_EXTRA} \
     && dnf install ${DNF_FLAGS_EXTRA} ${DNF_LIST} \
     && dnf clean all ${DNF_FLAGS} \
     && cp -f /etc/yum.repos.d/ubi.repo ${BUILD_PATH}/etc/yum.repos.d/ubi.repo \
     && rm -rf \
           ${BUILD_PATH}/var/cache/* \
     && mkdir -p /docker \
    && echo

#################################################################################
# Load Entrypoint from Cradle

#################################################################################
# Build Image from Rootfs
FROM scratch
COPY --from=builder /rootfs /
ADD ./rootfs /
COPY --from=registry   /bin/registry /usr/bin/registry
CMD /usr/bin/bash

#################################################################################
# Finalize Image
MAINTAINER ContainerCraft.io
LABEL \
  license=GPLv3                                                                 \
  name="shipperd"                                                               \
  distribution-scope="public"                                                   \
  io.openshift.tags="suipperd"                                                  \
  io.k8s.display-name="shipperd"                                                \
  summary="ShipperD Base Image | Micro Red Hat UBI Supportable Image"           \
  description="ShipperD Base Image | Micro Red Hat UBI Supportable Image"       \
  io.k8s.description="ShipperD Base Image | Micro Red Hat UBI Supportable Image"
