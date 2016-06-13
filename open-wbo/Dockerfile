FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y \
        curl \
        zlib1g-dev \
        zip \
        build-essential
ENV OPEN_WBO_SHA256 7cd52ea84b831dcfbe1986c0bd91d8358361c2436b88055ee37db34700589797

WORKDIR /src
RUN set -x \
        && curl -fSL "http://sat.inesc-id.pt/open-wbo/download_new.php?link=c99927e86b09bfa75df375fe2edc3371" -o open-wbo.zip \
        && echo "${OPEN_WBO_SHA256} *open-wbo.zip" | sha256sum -c - \
        && unzip open-wbo.zip \
        && cd open-wbo/ \
        && make rs \
        && cp open-wbo_static /bin/ \
        && cd .. \
        && chmod 755 /bin/open-wbo_static \
        && rm -rf open-wbo \
        && rm open-wbo.zip

ENTRYPOINT ["/bin/open-wbo_static"]
