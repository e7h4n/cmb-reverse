FROM mcr.microsoft.com/playwright:v1.53.0-noble

# Replace apt sources with Aliyun mirrors using https
# For Ubuntu 24.04 (Noble), the sources are in /etc/apt/sources.list.d/ubuntu.sources
RUN if [ -f /etc/apt/sources.list ]; then \
        sed -i 's|http://archive.ubuntu.com|https://mirrors.aliyun.com|g' /etc/apt/sources.list && \
        sed -i 's|http://security.ubuntu.com|https://mirrors.aliyun.com|g' /etc/apt/sources.list && \
        sed -i 's|http://ports.ubuntu.com|https://mirrors.aliyun.com|g' /etc/apt/sources.list; \
    fi && \
    if [ -f /etc/apt/sources.list.d/ubuntu.sources ]; then \
        sed -i 's|http://archive.ubuntu.com|https://mirrors.aliyun.com|g' /etc/apt/sources.list.d/ubuntu.sources && \
        sed -i 's|http://security.ubuntu.com|https://mirrors.aliyun.com|g' /etc/apt/sources.list.d/ubuntu.sources && \
        sed -i 's|http://ports.ubuntu.com|https://mirrors.aliyun.com|g' /etc/apt/sources.list.d/ubuntu.sources; \
    fi

# Install zsh, sudo, and common utilities
RUN apt-get update && \
    apt-get install -y \
        zsh \
        sudo \
        software-properties-common \
        vim \
        git \
        curl \
        wget \
        ca-certificates \
        gnupg \
        lsb-release && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Configure passwordless sudo for pwuser
RUN echo "pwuser ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Set zsh as default shell for the user
RUN chsh -s /bin/zsh pwuser

# Optional: Install Oh My Zsh for better zsh experience
USER pwuser
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" || true

USER root