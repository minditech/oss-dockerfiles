FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y \
        curl \
        zlib1g-dev \
        build-essential
ENV CLASP_BUCKET downloads.sourceforge.net/project/potassco
ENV CLASP_VERSION 3.1.4
ENV CLASP_SHA256 f6a7d8a90c3f216f778410ea7189b74a902750477fcce1a6b8c992fb08c372fe

WORKDIR /src
RUN set -x \
        && curl -fSL "http://${CLASP_BUCKET}/clasp/$CLASP_VERSION/clasp-$CLASP_VERSION-source.tar.gz" -o clasp.tar.gz \
        && echo "${CLASP_SHA256} *clasp.tar.gz" | sha256sum -c - \
        && tar -xzvf clasp.tar.gz \
        && cd clasp-${CLASP_VERSION}/ \
        && ./configure.sh --prefix=/ \
        && cd build/release \
        && make install \
        && cd ../../.. \
        && chmod 755 /bin/clasp \
        && rm -rf clasp-${CLASP_VERSION} \
        && rm clasp.tar.gz

ENTRYPOINT ["/bin/clasp"]
