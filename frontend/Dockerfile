#FROM node:13.5.0-alpine
#
#ENV PATH /var/www/frontend/node_modules/.bin:$PATH
#RUN apk update && \
#    apk upgrade && \
#    apk add git g++ gcc libgcc libstdc++ linux-headers make python && \
#    apk update
#
## install libsass
#RUN git clone https://github.com/sass/sassc && cd sassc && \
#    git clone https://github.com/sass/libsass && \
#    SASS_LIBSASS_PATH=/sassc/libsass make && \
#    mv bin/sassc /usr/bin/sassc && \
#    cd ../ && rm -rf /sassc
#
## created node-sass binary
#ENV SASS_BINARY_PATH=/usr/lib/node_modules/node-sass/build/Release/binding.node
#RUN git clone --recursive https://github.com/sass/node-sass.git && \
#    cd node-sass && \
#    git submodule update --init --recursive && \
#    npm install && \
#    node scripts/build -f && \
#    cd ../ && rm -rf node-sass
#
## add binary path of node-sass to .npmrc
#RUN touch $HOME/.npmrc && echo "sass_binary_cache=${SASS_BINARY_PATH}" >> $HOME/.npmrc
#
#ENV SKIP_SASS_BINARY_DOWNLOAD_FOR_CI true
#ENV SKIP_NODE_SASS_TESTS true


ARG LARADOCK_PHP_VERSION
FROM laradock/workspace:2.6.1-${LARADOCK_PHP_VERSION}

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y install curl
RUN curl -sL https://deb.nodesource.com/setup_13.x  | bash -

RUN apt-get update && apt-get install -y nodejs ruby-dev rubygems-integration
RUN gem install sass -v 3.4.1
RUN npm install -g @vue/cli

WORKDIR /var/www/frontend

EXPOSE 8080

# start app
CMD ["npm", "run", "serve"]

