#ARG VARIANT="hirsute"
#FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

FROM rockylinux:8

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# RUN dnf -y update && dnf -y dist-sync
RUN dnf -y update 
RUN dnf -y group install "Minimal Install" --allowerasing

RUN adduser tec && echo "Passw0rd" | passwd --stdin tec \
    && echo "Passw0rd" | passwd root --stdin

