FROM ubuntu:bionic

ARG GIT_COMMIT=unknown
ARG BUILD_ID=unknown
ARG BUILD_DATE=unknown
ARG BUILD_VERSION=0.1.0
ARG NAME=suricata-profiling
ARG VENDOR=awesome-inc
ARG http_proxy
ARG https_proxy

# cf.: http://label-schema.org/rc1/
LABEL org.label-schema.build-date="${BUILD_DATE}" \
      org.label-schema.name="${NAME}" \
      org.label-schema.description="Suricata docker container with enabled profiling and nfq" \
      org.label-schema.vcs-url="https://github.com/awesome-inc/docker-selks.git" \
      org.label-schema.vcs-ref="${GIT_COMMIT}" \
      org.label-schema.vendor="${VENDOR}" \
      org.label-schema.version="${BUILD_VERSION}" \
      org.label-schema.schema-version="1.0"

ENV GIT_COMMIT=$GIT_COMMIT
ENV BUILD_ID=$BUILD_ID
ENV http_proxy=$http_proxy
ENV https_proxy=$https_proxy

ADD config/ /etc/suricata/

# Prerequisites as of https://redmine.openinfosecfoundation.org/projects/suricata/wiki/Ubuntu_Installation_from_GIT
RUN apt-get update && \
    apt-get -y --no-install-recommends install libpcre3 libpcre3-dbg libpcre3-dev \
    build-essential autoconf automake libtool libpcap-dev libnet1-dev liblz4-dev \
    libyaml-0-2 libyaml-dev pkg-config zlib1g zlib1g-dev libcap-ng-dev libcap-ng0 \
    make libmagic-dev libjansson-dev git-core \
    libnetfilter-queue-dev libnetfilter-queue1 libnfnetlink-dev libnfnetlink0 \
    ca-certificates curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Add user and group
RUN addgroup --gid 2000 suri && \
    adduser --system --uid 2000 --gid 2000 suri && \
# build with nfq support, profiling support and also download emerging threats (thanks to make install-full)
   git clone https://github.com/OISF/suricata.git && cd suricata && \
   git clone https://github.com/OISF/libhtp.git -b 0.5.x && \
   ./autogen.sh && \
   ./configure --enable-profiling --enable-nfqueue --prefix=/usr --sysconfdir=/etc --localstatedir=/var && \
# --enable-rust  # not working yet
    make && make install-full && \
    cd .. && rm -rf /suricata/

CMD ["suricata", "-c", "/etc/suricata/suricata.yaml", "-i", "eth0"]
