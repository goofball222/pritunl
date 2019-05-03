FROM alpine

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION

LABEL \
    org.label-schema.vendor="The Goofball - goofball222@gmail.com" \
    org.label-schema.url="https://github.com/goofball222/pritunl" \
    org.label-schema.name="Pritunl Server" \
    org.label-schema.version=$VERSION \
    org.label-schema.vcs-url="https://github.com/goofball222/pritunl.git" \
    org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.license="Apache-2.0" \
    org.label-schema.schema-version="1.0"

ENV \
    DEBUG=false \
    GOPATH="/go" \
    GOCACHE=off \
    PRITUNL_OPTS= \
    REVERSE_PROXY=false

WORKDIR /opt/pritunl

ADD root /

RUN set -x \
    && apk add -q --no-cache --virtual .build-deps \
        bzr curl gcc git go libffi-dev linux-headers \
        musl-dev openssl-dev python-dev py-pip \
    && apk add -q --no-cache \
        bash ca-certificates iptables ip6tables \
        openssl openvpn procps py-setuptools \
        py-dnspython tzdata \
    && pip install --upgrade pip \
    && go get github.com/pritunl/pritunl-dns \
    && go get github.com/pritunl/pritunl-web \
    && cp /go/bin/* /usr/bin \
    && cd /tmp \
    && curl -sSL https://github.com/pritunl/pritunl/archive/${VERSION}.tar.gz -o /tmp/${VERSION}.tar.gz \
    && tar -zxf /tmp/${VERSION}.tar.gz \
    && cd /tmp/pritunl-${VERSION} \
    && python2 setup.py build \
    && pip install -r requirements.txt \
    && mkdir -p /var/lib/pritunl \
    && python2 setup.py install \
    && apk del -q --purge .build-deps \
    && rm -rf /go /root/.cache/* /tmp/* /var/cache/apk/*

EXPOSE 80/tcp 443/tcp 1194/tcp 1194/udp 9700/tcp

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["pritunl"]

