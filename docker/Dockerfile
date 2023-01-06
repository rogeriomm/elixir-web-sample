FROM elixir:latest

ENV VERSION=v18.13.0
#ENV DISTRO=linux-x64
ENV DISTRO=linux-arm64
#ENV DISTRO=linux-armv7l

RUN apt-get update && \
    apt-get install -y postgresql-client && \
    apt-get install -y inotify-tools

RUN wget https://nodejs.org/dist/$VERSION/node-$VERSION-$DISTRO.tar.xz -O /tmp/node.xz  && \
    mkdir -p /usr/local/lib/nodejs && \
    tar -xJvf /tmp/node.xz -C /usr/local/lib/nodejs

ENV PATH=/usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin:$PATH

RUN curl -L https://npmjs.org/install.sh | sh

RUN mix local.hex --force && \
    mix archive.install hex phx_new 1.5.3 --force && \
    mix local.rebar --force

ENV APP_HOME /app
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

CMD ["mix", "phx.server"]
