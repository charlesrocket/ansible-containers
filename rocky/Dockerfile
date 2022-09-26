FROM rockylinux/rockylinux
LABEL maintainer="charlesrocket"

RUN dnf -y update && dnf -y install dnf-plugins-core && dnf clean all

RUN dnf -y install \
           sudo \
           python3 \
           python3-pip \
           rsync \
           which && \
           dnf clean all

RUN alternatives --set python /usr/bin/python3

RUN python3 -m pip install --upgrade pip && \
    python3 -m pip install ansible

RUN ln -s /usr/local/bin/ansible* /usr/bin/

RUN sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers

RUN mkdir /etc/ansible && echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

VOLUME ["/sys/fs/cgroup"]

ENTRYPOINT ["/usr/sbin/init"]
