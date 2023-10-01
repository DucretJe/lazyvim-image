FROM alpine:edge@sha256:f2d1645cd73c7e54584dc225da0b5229d19223412d719669ebda764f41396853

ARG USER=nvim

# Mention Lazyvim version in order for the build to be triggered when bumped
ENV LAZYVIM_VER v8.0.0

# Repology
# renovate: datasource=repology depName=alpine_edge/alpine-sdk versioning=loose
ENV ALPINESDK_VER 1.0-r1
# renovate: datasource=repology depName=alpine_edge/lazygit versioning=loose
ENV LAZYGIT_VER 0.40.2-r1
# renovate: datasource=repology depName=alpine_edge/git versioning=loose
ENV GIT_VER 2.42.0-r0
# renovate: datasource=repology depName=alpine_edge/neovim versioning=loose
ENV NEOVIM_VER 0.9.2-r0
# renovate: datasource=repology depName=alpine_edge/ripgrep versioning=loose
ENV RIPGREP_VER 13.0.0-r6
# renovate: datasource=repology depName=alpine_edge/sudo versioning=loose
ENV SUDO_VER 1.9.14_p3-r0

RUN adduser -D -h /home/${USER} -s /bin/ash ${USER}
RUN apk update && apk add --no-cache \
    git=${GIT_VER} \
    lazygit=${LAZYGIT_VER} \
    neovim=${NEOVIM_VER} \
    ripgrep=${RIPGREP_VER} \
    alpine-sdk=${ALPINESDK_VER} \
    sudo=${SUDO_VER}
SHELL ["/bin/ash", "-o", "pipefail", "-c"]
RUN echo "${USER} ALL=(ALL) NOPASSWD:/usr/bin/nvim" | tee /etc/sudoers.d/${USER} && \
    git clone https://github.com/LazyVim/starter /root/.config/nvim && \
    nvim +q

USER ${USER}

HEALTHCHECK NONE

ENTRYPOINT ["/usr/bin/sudo", "/usr/bin/nvim"]
