FROM alpine:latest
LABEL maintainer="charlesrocket"

RUN apk add --no-cache sudo ansible openssh

VOLUME ["/sys/fs/cgroup"]

ENTRYPOINT ["/sbin/init"]
