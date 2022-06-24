FROM node:carbon

ARG PACKAGE=open5gs
ARG VERSION=2.4.7

RUN set -e; \
    cd /usr/src; \
    rm -rf ./$PACKAGE; \
    curl -SLO "https://github.com/open5gs/$PACKAGE/archive/v$VERSION.tar.gz"; \
    tar -xvf v$VERSION.tar.gz; \
    mv ./$PACKAGE-$VERSION/ ./$PACKAGE;

WORKDIR /usr/src/open5gs/webui
RUN npm install && \
    npm run build

# Install updates and dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        iproute2 \
        ethtool \
        iputils-ping \
        net-tools \
        procps \
        grep &&\
    apt-get remove -y curl && \
    apt-get autoremove -y && \
    apt-get autoclean

WORKDIR /
