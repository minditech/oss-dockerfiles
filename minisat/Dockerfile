FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y \
        curl \
        zlib1g-dev \
        build-essential

ENV MINISAT_BUCKET minisat.se/downloads
ENV MINISAT_VERSION 2.2.0
ENV MINISAT_SHA256 92957d851cdc3baddfe07b5fc80ed5a0237c489d0c52ae72f62844b3b46d7808
ENV MROOT /src/minisat

WORKDIR /src
RUN set -x \
        && curl -fSL "http://${MINISAT_BUCKET}/minisat-$MINISAT_VERSION.tar.gz" -o minisat.tar.gz \
        && echo "${MINISAT_SHA256} *minisat.tar.gz" | sha256sum -c - \
        && tar -xzvf minisat.tar.gz \
        && cd minisat/simp \
        && make rs \
        && cp minisat_static /bin/ \
        && cd ../.. \
        && chmod 755 /bin/minisat_static \
        && rm -rf minisat \
        && rm minisat.tar.gz

ENTRYPOINT ["/bin/minisat_static"]
