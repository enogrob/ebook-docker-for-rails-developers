FROM ruby:2.4
MAINTAINER Roberto Nogueira <rnogueira@tecnogroup.com.br>

# Setup Proxies
COPY apt.conf /etc/apt
ENV HTTP_PROXY "http://172.16.160.150:8080"
ENV HTTPS_PROXY "https://172.16.160.150:8080"
ENV NO_PROXY "localhost,127.0.0.1"

# Install platform requirements for rails
RUN apt-get update -yqq

# Allow apt to work with https-based sources
RUN apt-get install -yqq --no-install-recommends \
apt-transport-https

# Ensure we install an up-to-date version Node
# See https://github.com/yarnpkg/yarn/issues/2888
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -

# Ensure latest packages for Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | \
tee /etc/apt/sources.list.d/yarn.list

# Install packages
RUN apt-get update -yqq && apt-get install -yqq --no-install-recommends \
nodejs \
yarn

# Install gem files
COPY Gemfile* /usr/src/app/
WORKDIR /usr/src/app
RUN bundle install
