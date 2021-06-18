FROM alpine:3.14

RUN apk add --no-cache lua5.1 \
    lua5.1-cjson \
    lua5.1-filesystem \
    lua5.1-maxminddb \
    lua5.1-rex-pcre

ENTRYPOINT ["lua"]
