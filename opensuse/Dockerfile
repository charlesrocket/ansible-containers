FROM opensuse/leap:latest
LABEL maintainer="charlesrocket"

ENV container docker

RUN zypper -n install systemd; zypper clean ; \
    (cd /usr/lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /usr/lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /usr/lib/systemd/system/local-fs.target.wants/*; \
    rm -f /usr/lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /usr/lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /usr/lib/systemd/system/basic.target.wants/*;\
    rm -f /usr/lib/systemd/system/anaconda.target.wants/*;

RUN zypper -n install sudo python3-pip curl tar unzip rsync fuse-devel; zypper clean

RUN pip install ansible

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/usr/lib/systemd/systemd", "--system"]
