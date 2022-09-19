FROM fedora:latest
LABEL maintainer="charlesrocket"

RUN dnf -y update && dnf clean all

RUN dnf -y install systemd && dnf clean all && \
    (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*;\
    rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN dnf makecache \
    && dnf -y install \
    sudo \
    python3-pip \
    python3-dnf  \
    which && \
    dnf clean all

RUN pip3 install ansible

RUN mkdir -p /etc/ansible

RUN echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

VOLUME ["/sys/fs/cgroup", "/tmp", "/run"]

CMD ["/usr/sbin/init"]
