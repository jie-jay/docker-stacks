# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.

# https://hub.docker.com/r/jupyter/base-notebook/tags
ARG OWNER=jupyter
ARG BASE_CONTAINER=$OWNER/base-notebook:33add21fab64
FROM $BASE_CONTAINER

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"
ENV TAG="33add21fab64"

WORKDIR "${HOME}"
COPY binder/README.ipynb .

# Fix permissions on README.ipynb as root
USER root

RUN apt-get update --yes && \
    apt-get install --yes --no-install-recommends \
    tini \
    wget \
    tmux \
    net-tools \
    ca-certificates \
    sudo \
    locales \
    fonts-liberation \
    run-one && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen

RUN fix-permissions README.ipynb

# Switch back to jovyan to avoid accidental container runs as root
USER ${NB_UID}

WORKDIR "${HOME}"
