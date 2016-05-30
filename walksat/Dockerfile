FROM alpine:latest

RUN apk add --update \
        curl \
        zip \
        build-base \
    && rm -rf /var/cache/apk/*

ENV WALKSAT_BUCKET www.cs.rochester.edu/u/kautz/walksat
ENV WALKSAT_VERSION 51
ENV WALKSAT_SHA256 c3ca524af75c25dbdc70402c6ff37caa9b10c71030bac7c7eaf4ac11945e625f

WORKDIR /src
RUN set -x \
        && curl -fSL "https://${WALKSAT_BUCKET}/Walksat_v$WALKSAT_VERSION.zip" -o walksat.zip \
        && echo "${WALKSAT_SHA256} *walksat.zip" | sha256sum -c - \
        && unzip walksat.zip \
        && cd Walksat_v$WALKSAT_VERSION/ \
        && make \
        && mv walksat /bin/ \
        && cd .. \
        && chmod 755 /bin/walksat \
        && rm -rf Walksat_v$WALKSAT_VERSION \
        && rm walksat.zip

ENTRYPOINT ["/bin/walksat"]
