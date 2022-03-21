FROM alpine

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION

LABEL \
    org.opencontainers.image.vendor="The Goofball - goofball222@gmail.com" \
    org.opencontainers.image.url="https://github.com/goofball222/pritunl" \
    org.opencontainers.image.title="Pritunl Server" \
    org.opencontainers.image.description="Pritunl Server" \
    org.opencontainers.image.version=$VERSION \
    org.opencontainers.image.source="https://github.com/goofball222/pritunl" \
    org.opencontainers.image.revision=$VCS_REF \
    org.opencontainers.image.created=$BUILD_DATE \
    org.opencontainers.image.licenses="Apache-2.0"

ENV \
    DEBUG=false \
    GOPATH="/go" \
    GOCACHE="/tmp/gocache" \
    GO111MODULE=on \
    PRITUNL_OPTS= \
    REVERSE_PROXY=false \
    WIREGUARD=false

WORKDIR /opt/pritunl

ADD root /

RUN set -x \
    && apk add -q --no-cache --virtual .build-deps \
        cargo curl gcc git \
        go libffi-dev linux-headers make \
        musl-dev openssl-dev python3-dev py3-pip \
        rust \
    && apk add -q --no-cache \
        bash ca-certificates ipset iptables \
        ip6tables openssl openvpn procps \
        py3-dnspython py3-requests py3-setuptools tzdata \
        wireguard-tools \
    && pip3 install --upgrade pip \
    && go get github.com/pritunl/pritunl-dns \
    && go get github.com/pritunl/pritunl-web \
    && cp /go/bin/* /usr/bin \
    && cd /tmp \
    && curl -sSL https://github.com/pritunl/pritunl/archive/refs/tags/${VERSION}.tar.gz -o /tmp/${VERSION}.tar.gz \
    && tar -zxf /tmp/${VERSION}.tar.gz \
    && cd /tmp/pritunl-${VERSION} \
    && python3 setup.py build \
    && pip3 install -r requirements.txt \
    && mkdir -p /var/lib/pritunl \
    && python3 setup.py install \
    && apk del -q --purge .build-deps \
    && rm -rf /go /root/.cache/* /tmp/* /var/cache/apk/*

EXPOSE 80/tcp 443/tcp 1194/tcp 1194/udp 1195/udp 9700/tcp

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["pritunl"]

