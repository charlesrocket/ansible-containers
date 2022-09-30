FROM archlinux:latest
LABEL maintainer="charlesrocket"

RUN \
    pacman --noconfirm --sync --refresh --sysupgrade \
        systemd \
        procps && \
    (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
        rm -f /lib/systemd/system/default.target ; \
        rm -f /lib/systemd/system/multi-user.target.wants/* ; \
        rm -f /lib/systemd/system/local-fs.target.wants/* ; \
        rm -f /lib/systemd/system/sockets.target.wants/*udev* ; \
        rm -f /lib/systemd/system/sockets.target.wants/*initctl* ; \
        rm -f /lib/systemd/system/basic.target.wants/* ; \
        rm -f /lib/systemd/system/anaconda.target.wants/* ; \
        rm -f /lib/systemd/system/systemd-timesyncd* ; \
        rm -f /lib/systemd/system/systemd-resolved* ; \
        rm -f /lib/systemd/system/systemd-networkd* ; \
        rm -f /lib/systemd/system/systemd-homed* ; \
        rm -f /lib/systemd/system/systemd-userdbd* ; \
        rm -f /lib/systemd/system/remote-cryptsetup* ; \
        rm -rf /lib/systemd/system/remote-fs* ; \
        rm -f /lib/systemd/system/systemd-network-generator* ; \
        rm -f /lib/systemd/system/systemd-pstore* ; \
        rm -f /lib/systemd/system/systemd-boot-update ; \
        rm -f /etc/systemd/system/dbus-org.freedesktop* ; \
        rm -f /etc/systemd/system/*.wants/*

RUN \
    pacman \
        --noconfirm --sync --refresh --sysupgrade && \
    pacman \
        --noconfirm --sync --refresh \
          sudo \
          ansible \
          python-setuptools \
          python-pip \
          openssh \
          gawk \
          unzip \
          tar \
          rsync \
          fuse

RUN echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

RUN pacman --noconfirm --sync -cc && rm -rf tmp/*

CMD ["/usr/lib/systemd/systemd"]
