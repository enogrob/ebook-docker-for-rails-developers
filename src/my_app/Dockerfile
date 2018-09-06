FROM ruby:2.4
MAINTAINER Roberto Nogueira <rnogueira@tecnogroup.com.br>

# Setup Proxies
COPY apt.conf /etc/apt
ENV HTTP_PROXY "http://172.16.160.150:8080"
ENV HTTPS_PROXY "https://172.16.160.150:8080"
ENV NO_PROXY "localhost,127.0.0.1"

# Install platform requirements for rails
RUN apt-get update -yqq
RUN apt-get install -yqq --no-install-recommends nodejs

# Install gem files
COPY Gemfile* /usr/src/app/
WORKDIR /usr/src/app
RUN bundle install

CMD ["rails", "s", "-b", "0.0.0.0"]
