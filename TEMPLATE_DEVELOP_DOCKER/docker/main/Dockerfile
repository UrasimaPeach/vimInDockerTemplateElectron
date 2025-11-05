FROM ubuntu:24.04
WORKDIR /app
ARG UID
ARG GID
ARG USERNAME
ENV LANG=C.UTF-8
ENV LANGUAGE=en_US
ENV NODE_VERSION=20
ENV DISPLAY=host.docker.internal:0.0
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Tokyo

VOLUME /app
VOLUME /root/.vim
VOLUME /root/.vimrc
RUN
RUN groupadd -g ${GID} ${USERNAME} -f && \
  useradd -m -s /bin/bash -u ${UID} -g ${GID} ${USERNAME} &&
  apt update && \
  apt upgrade -y && \
  apt install -y curl vim git&& \
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash && \
  export NVM_DIR="$HOME/.nvm" && \
  [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
  [ -s "$NVM_DIR/bash_completion" ] && . "$NVM_DIR/bash_completion"  && \
  nvm install $NODE_VERSION &&\
  apt install -y \
    libgtkextra-dev \
    libgconf2-dev \
    libnss3 \
    libasound2 \
    libxtst-dev \
    libxss1 \
    libgtk-3-0 \
    libdrm2 \
    libgbm1 \
    libcanberra-gtk* \
    rpm \
    wine \
    mono-devel &&\
    dpkg --add-architecture i386 && apt update && apt install -y wine32
VOLUME /app
