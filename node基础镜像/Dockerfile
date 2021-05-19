FROM debian:latest

# replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# update the repository sources list
# and install dependencies
RUN apt-get update \
    && apt-get install -y curl \
    && apt-get -y autoclean

# nvm environment variables
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 15.9.0


RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash

# install node and npm
RUN source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

# add node and npm to path so the commands are available
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

# confirm installation
RUN node -v
RUN npm -v

RUN apt-get  install -y libpng-dev
RUN apt-get  install -y python
RUN apt install -y build-essential gcc make libpng-dev
RUN apt install -y  automake libtool
RUN  apt install -y nasm 
RUN apt install -y  wget 

RUN npm config set registry https://registry.npm.taobao.org
RUN npm install -g pngquant-bin
RUN npm install yarn -g
RUN yarn config set registry https://registry.npm.taobao.org/
RUN yarn config set sass-binary-site http://npm.taobao.org/mirrors/node-sass


# RUN apt install vim -y

RUN set -ex \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        autoconf \
        libtool \
        libpng-dev \
        pkg-config \
        nasm \
    && wget -q -O /tmp/libpng12.deb http://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb \
         && dpkg -i /tmp/libpng12.deb \
         && rm /tmp/libpng12.deb \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/*

RUN apt-get update

