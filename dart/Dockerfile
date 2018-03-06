FROM ubuntu:latest

RUN mkdir /sources
WORKDIR /sources

# set mirror site
RUN sed -i -e 's/archive.ubuntu.com/mirrors.bangmod.cloud/g' /etc/apt/sources.list
RUN apt update && apt upgrade -y

# install dart
RUN apt install -y curl wget build-essential apt-transport-https 
RUN sh -c 'curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -'
RUN sh -c 'curl https://storage.googleapis.com/download.dartlang.org/linux/debian/dart_stable.list > /etc/apt/sources.list.d/dart_stable.list'
RUN apt update
RUN export PATH=/usr/lib/dart/bin:$PATH
RUN apt install -y dart/stable
