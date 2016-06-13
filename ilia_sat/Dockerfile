FROM alpine:latest

RUN apk add --update \
        build-base \
    && rm -rf /var/cache/apk/*

WORKDIR /src
COPY Makefile /src/
COPY main_clean.cpp /src/
RUN make \
        && mv ilia_sat /bin/ \
        && cd .. \
        && chmod 755 /bin/ilia_sat \
        && rm -rf src/

ENTRYPOINT ["/bin/ilia_sat"]
