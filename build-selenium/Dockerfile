FROM selenium/standalone-chrome:3.4.0

USER root
ENV LANGUAGE de_DE.UTF-8
ENV LANG de_DE.UTF-8

RUN apt-get update -qqy \
    && apt-get -qqy --no-install-recommends install \
        iputils-ping \
        iproute2 \
        net-tools \
    && rm -rf /var/lib/apt/lists/* \
    && locale-gen de_DE.UTF-8 \
    && dpkg-reconfigure --frontend noninteractive locales \
    && apt-get update -qqy \
    && apt-get -qqy --no-install-recommends install \
        language-pack-de \
    && rm -rf /var/lib/apt/lists/*

USER seluser