FROM alpine:edge

# Mention Lazyvim version in order for the build to be triggered when bumped
LAZYVIM_VER v6.1.0

RUN apk add git lazygit neovim ripgrep alpine-sdk --update && \
    git clone https://github.com/LazyVim/starter ~/.config/nvim
    cd ~/.config/nvim
    nvim +q

HEALTHCHECK NONE

ENTRYPOINT ["nvim"]

