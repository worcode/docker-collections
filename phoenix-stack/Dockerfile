FROM ubuntu:latest

RUN locale-gen en_US.UTF-8 

# system env
ENV TZ=Asia/Bangkok
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

RUN mkdir /sources
RUN mkdir /usr/src/app
WORKDIR /sources

# set TZ
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# set mirror site
RUN sed -i -e 's/archive.ubuntu.com/mirrors.bangmod.cloud/g' /etc/apt/sources.list
RUN sed -i -e 's/security.ubuntu.com/mirrors.bangmod.cloud/g' /etc/apt/sources.list
RUN apt update
RUN apt install wget \
    curl \
    build-essential \
    apt-transport-https \
    -y

# add yarn repo
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# add elixir repo
RUN wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && dpkg -i erlang-solutions_1.0_all.deb

# update and install repo
RUN apt update && apt install yarn \
    esl-erlang \
    elixir \
    -y

# add inotify-tools
RUN wget http://github.com/downloads/rvoicilas/inotify-tools/inotify-tools-3.14.tar.gz
RUN mkdir -p inotify && tar -xvf inotify-tools-3.14.tar.gz -C inotify --strip 1
RUN cd inotify \
    && ./configure --prefix=/usr \
    && make \
    && make install

RUN apt upgrade -y

# upgrade hex, add phoenix
RUN mix local.hex --force \
    mix archive.install https://github.com/phoenixframework/archives/raw/master/phx_new.ez --force

# test elixir yarn command
RUN elixir --version
RUN yarn --version
RUN mix help