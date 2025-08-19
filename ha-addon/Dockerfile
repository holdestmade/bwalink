ARG BUILD_FROM
FROM ${BUILD_FROM}

# Update and install necessary packages in a single RUN to reduce image layers
RUN apk update && apk add --no-cache \
    bash \
    curl \
    ruby \
    ruby-dev \
    ruby-bundler \
    libffi-dev \
    zlib-dev \
    socat \
    tzdata \
    build-base \
  && bundle config set deployment 'true' \

RUN gem install specific_install && \
    gem specific_install -l https://github.com/holdestmade/balboa_worldwide_app.git -b main

  && apk del build-base \
  && rm -rf /var/cache/apk/* /tmp/* /var/tmp/*

ADD docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

CMD ["/docker-entrypoint.sh"]
