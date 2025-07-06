FROM mcr.microsoft.com/playwright:v1.53.0-noble

# Replace apt sources with Aliyun mirrors using https
RUN sed -i 's|http://archive.ubuntu.com|https://mirrors.aliyun.com|g' /etc/apt/sources.list && \
    sed -i 's|http://security.ubuntu.com|https://mirrors.aliyun.com|g' /etc/apt/sources.list && \
    sed -i 's|http://ports.ubuntu.com|https://mirrors.aliyun.com|g' /etc/apt/sources.list

# Install zsh
RUN apt-get update && \
    apt-get install -y zsh && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set zsh as default shell for the user
RUN chsh -s /bin/zsh pwuser

# Optional: Install Oh My Zsh for better zsh experience
USER pwuser
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" || true

USER root