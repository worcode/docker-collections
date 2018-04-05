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
RUN apt update && apt upgrade -y
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

# set usr work DIR
WORKDIR /usr/src/app

# test elixir yarn command
RUN elixir --version
RUN yarn --version