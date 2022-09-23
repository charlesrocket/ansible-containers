FROM debian:latest
LABEL maintainer="charlesrocket"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       sudo \
       build-essential \
       systemd \
       systemd-sysv \
       wget \
       iproute2 \
       libffi-dev \
       libssl-dev \
       procps \
       python3-pip \
       python3-dev \
       python3-setuptools \
       python3-wheel \
       python3-apt \
    && apt-get autoremove -y && apt-get clean \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip

RUN pip3 install cryptography ansible

RUN mkdir -p /etc/ansible && echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

RUN rm -f /lib/systemd/system/multi-user.target.wants/getty.target

VOLUME ["/sys/fs/cgroup"]
CMD ["/lib/systemd/systemd"]
