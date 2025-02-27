FROM mcr.microsoft.com/devcontainers/python:1-3.12-bullseye

ARG USER
ARG WORKDIR
ARG HOME="/home/${USER}"

ENV PATH="${HOME}/.local/bin:${PATH}"

RUN DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y build-essential --no-install-recommends make \
        ca-certificates \
        git \
        libssl-dev \
        zlib1g-dev \
        libbz2-dev \
        libreadline-dev \
        libsqlite3-dev \
        curl \
        llvm \
        libncurses5-dev \
        xz-utils \
        tk-dev \
        libxml2-dev \
        libxmlsec1-dev \
        libffi-dev \
        liblzma-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR ${WORKDIR}
USER ${USER}

RUN curl -sSL https://install.python-poetry.org | python3 - \
    && poetry config virtualenvs.in-project true \
    && curl -sfL https://direnv.net/install.sh | bash \
    && echo 'eval "$(direnv hook bash)"' >> ${HOME}/.bashrc \
    && mkdir -p ${HOME}/.config/direnv \
    && echo "[whitelist]\nprefix = [ \"${WORKDIR}\" ]\n" > ${HOME}/.config/direnv/direnv.toml
