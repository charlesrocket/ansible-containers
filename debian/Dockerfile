FROM debian:latest
LABEL maintainer="charlesrocket"

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       sudo \
       systemd \
       systemd-sysv \
       build-essential \
       wget \
       libffi-dev \
       libssl-dev \
       python3-pip \
       python3-dev \
       python3-setuptools \
       python3-wheel \
    && rm -rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get autoremove -y && apt-get clean

RUN pip3 install --no-cache-dir --upgrade pip \
    && pip3 install --no-cache-dir ansible

COPY initctl_faker .
RUN chmod +x initctl_faker && rm -fr /sbin/initctl && ln -s /initctl_faker /sbin/initctl

RUN mkdir -p /etc/ansible && printf "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

RUN rm -f /lib/systemd/system/multi-user.target.wants/getty.target

VOLUME ["/sys/fs/cgroup"]
CMD ["/lib/systemd/systemd"]
