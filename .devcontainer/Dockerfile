ARG DOCKER_DEFAULT_PLATFORM=linux/amd64

FROM --platform=$DOCKER_DEFAULT_PLATFORM mcr.microsoft.com/devcontainers/typescript-node:1-20-bullseye
# FROM mcr.microsoft.com/devcontainers/typescript-node:1-20-bullseye

# Install SonarScanner CLI
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    unzip \
    && rm -rf /var/lib/apt/lists/* \
    && sudo curl https://cdn.shiftleft.io/download/sl >/usr/local/bin/sl && chmod a+rx /usr/local/bin/sl