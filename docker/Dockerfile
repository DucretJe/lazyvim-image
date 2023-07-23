FROM alpine:edge@sha256:2d01a16bab53a8405876cec4c27235d47455a7b72b75334c614f2fb0968b3f90

ARG USER=nvim

# Mention Lazyvim version in order for the build to be triggered when bumped
ENV LAZYVIM_VER v6.1.0

# Repology
# renovate: datasource=repology depName=alpine_edge/alpine-sdk versioning=loose
ENV ALPINESDK_VER 1.0
# renovate: datasource=repology depName=alpine_edge/lazygit versioning=loose
ENV LAZYGIT_VER 0.39.2-r0
# renovate: datasource=repology depName=alpine_edge/git versioning=loose
ENV GIT_VER 2.41.0
# renovate: datasource=repology depName=alpine_edge/neovim versioning=loose
ENV NEOVIM_VER 0.9.1
# renovate: datasource=repology depName=alpine_edge/ripgrep versioning=loose
ENV RIPGREP_VER 13.0.0
# renovate: datasource=repology depName=alpine_edge/sudo versioning=loose
ENV SUDO_VER 1.9.14

RUN adduser -D -h /home/${USER} -s /bin/ash ${USER}

# False KICS positive in the following command triggering `Unpinned Package Version in Apk Add`
# We use >= as a workarround for revision but the packages are pinned and maintained by renovate
# False positive in HADOLINT, the version is pinned and redirectionned output
# hadolint ignore=DL3018
# kics-scan ignore-line
# hadolint disable=SC2261
RUN apk update && apk add --no-cache \
    git>=${GIT_VER} \
    lazygit>=${LAZYGIT_VER} \
    neovim>=${NEOVIM_VER} \
    ripgrep>=${RIPGREP_VER} \
    alpine-sdk>=${ALPINESDK_VER} \
    sudo>=${SUDO_VER}

RUN echo "${USER} ALL=(ALL) NOPASSWD:/usr/bin/nvim" | tee /etc/sudoers.d/${USER} && \
    git clone https://github.com/LazyVim/starter /root/.config/nvim && \
    nvim +q

USER ${USER}

HEALTHCHECK NONE

ENTRYPOINT ["/usr/bin/sudo", "/usr/bin/nvim"]
