FROM ubuntu:17.10

ENV LANG en_US.utf8
ENV APP_CONTAINER_DIR /usr/src/app

# set workspace
WORKDIR ${APP_CONTAINER_DIR}

# modify, update ubuntu repos
RUN cp /etc/apt/sources.list /etc/apt/sources.list.ori \
    && sed -i -e 's/archive.ubuntu.com/mirrors.bangmod.cloud/g' /etc/apt/sources.list \
    && apt update \
    && apt install -y \
        curl \
        git \
        build-essential \
        locales \
        apt-utils \
    && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

# install sources
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt update \
    && apt install -y \
        nodejs
RUN apt install -y --no-install-recommends yarn

# modify .bashrc
RUN echo '\n\
    alias nodejs=node \n\
    \n' \ 
    >> $HOME/.bashrc \
    && chmod +x $HOME/.bashrc \
    && . $HOME/.bashrc

# cmd testing
RUN node -v \
    && npm -v \
    && yarn -v \
    && yarn global add vue-cli