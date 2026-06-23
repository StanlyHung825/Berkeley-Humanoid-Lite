ARG ISAACSIM_BASE_IMAGE=nvcr.io/nvidia/isaac-sim:5.1.0
ARG UV_VERSION=0.8.15

FROM ghcr.io/astral-sh/uv:${UV_VERSION} AS uv
FROM ${ISAACSIM_BASE_IMAGE}

USER root

COPY --from=uv /uv /uvx /usr/local/bin/

RUN apt-get update \
    && apt-get install -y --no-install-recommends git python3-pip sudo \
    && rm -rf /var/lib/apt/lists/* \
    && groupadd --gid 992 render \
    && printf 'ubuntu ALL=(ALL) NOPASSWD:ALL\n' > /etc/sudoers.d/ubuntu \
    && chmod 0440 /etc/sudoers.d/ubuntu \
    && printf '\nforce_color_prompt=yes\nPS1="\\[\\033[01;32m\\]\\u@\\h\\[\\033[00m\\]:\\[\\033[01;34m\\]\\w\\[\\033[00m\\]\\$ "\n' >> /home/ubuntu/.bashrc \
    && mkdir -p /home/ubuntu/.cache /home/ubuntu/.venv \
    && chown -R ubuntu:ubuntu /home/ubuntu

ENV HOME=/home/ubuntu \
    TERM=xterm-256color \
    COLORTERM=truecolor \
    FORCE_COLOR=1 \
    UV_LINK_MODE=copy

USER ubuntu
WORKDIR /workspace

ENTRYPOINT []
CMD ["bash", "-l"]
