FROM node:12-slim

ENV TZ=Asia/Bangkok

WORKDIR /tmp

RUN apt update -y \
    && apt install -y curl sudo git gnupg2 build-essential \
    && git clone https://github.com/StackExchange/blackbox.git \
    && cd blackbox && make copy-install \
    && rm -rf /tmp/blackbox \ 
    && curl -sf https://gobinaries.com/tj/node-prune | sh \
    && env SUDO_FORCE_REMOVE=yes apt remove -y curl sudo git build-essential \
    && apt autoremove -y \
    && apt clean --dry-run

WORKDIR /