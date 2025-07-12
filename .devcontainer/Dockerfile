FROM debian:bookworm

ARG USERNAME=devuser
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ARG LOCALE=ja_JP.UTF-8
ARG TIME_ZONE=Asia/Tokyo
ARG NODE_VERSION=22

ENV LANGUAGE=${LOCALE}
ENV LC_ALL=${LOCALE}
ENV TZ=${TIME_ZONE}
ENV DEBIAN_FRONTEND=noninteractive
ENV DEVCONTAINER=true

# Install development tools and utilities
RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends \
    build-essential \
    ca-certificates \
    chromium \
    curl \
    dnsutils \
    fonts-noto \
    git \
    gnupg \
    imagemagick \
    jq \
    less \
    libssl-dev \
    locales \
    mariadb-client \
    ncdu \
    openssh-client \
    postgresql-client \
    rsync \
    shellcheck \
    sqlite3 \
    sudo \
    tree \
    unzip \
    wget \
    vim \
    yq \
    zip \
    zsh \
    # Additional tools for development
    htop \
    tmux \
    ripgrep \
    fd-find \
    bat \
    exa \
    fzf \
    man-db \
    procps \
    gh \
    iptables \
    ipset \
    iproute2 \
    aggregate \
    # clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Install Node.js repository and Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash - \
    && apt-get install -y nodejs

# Install Claude
RUN npm install -g @anthropic-ai/claude-code

# Configure locale, create user, and set up workspace
RUN : \
    # locale
    && sed -i -E "s/# (${LOCALE})/\1/" /etc/locale.gen \
    && locale-gen ${LOCALE} \
    # user
    && groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd -s /bin/bash --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME} \
    # work directory
    && mkdir -p /workspace \
    && chown ${USERNAME}:${USERNAME} /workspace

# Install git-delta for better git diff
RUN ARCH=$(dpkg --print-architecture) && \
    wget "https://github.com/dandavison/delta/releases/download/0.18.2/git-delta_0.18.2_${ARCH}.deb" && \
    dpkg -i "git-delta_0.18.2_${ARCH}.deb" && \
    rm "git-delta_0.18.2_${ARCH}.deb"

# Set up command history persistence
RUN mkdir -p /commandhistory \
    && touch /commandhistory/.bash_history \
    && touch /commandhistory/.zsh_history \
    && chown -R ${USERNAME}:${USERNAME} /commandhistory

# Create .claude directory structure
RUN mkdir -p /home/${USERNAME}/.claude \
    && chown -R ${USERNAME}:${USERNAME} /home/${USERNAME}/.claude

# Switch to non-root user
USER ${USERNAME}

# Set up zsh with Oh My Zsh
RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v1.2.0/zsh-in-docker.sh)" -- \
    -p git \
    -p fzf \
    -a "source /usr/share/doc/fzf/examples/key-bindings.zsh" \
    -a "source /usr/share/doc/fzf/examples/completion.zsh" \
    -a "export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
    -a "export HISTFILE=/commandhistory/.zsh_history" \
    -a "export HISTSIZE=1000" \
    -a "export SAVEHIST=1000" \
    -x

# Set environment variables
ENV SHELL=/bin/zsh

# Set working directory
WORKDIR /workspace
