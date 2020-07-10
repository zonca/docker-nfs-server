FROM centos:centos7

RUN \
    yum -y --setopt=tsflags=nodocs install nfs-utils openssh-server openssh-clients rsync && \
    mkdir -p /share && \
    chmod 777 /share && \
    yum clean all

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''

RUN  \
    mkdir -p /var/lib/nfs/rpc_pipefs /var/lib/nfs/v4recovery && \
    echo "rpc_pipefs    /var/lib/nfs/rpc_pipefs rpc_pipefs      defaults        0       0" >> /etc/fstab && \
    echo "nfsd  /proc/fs/nfsd   nfsd    defaults        0       0" >> /etc/fstab

EXPOSE 111/udp 2049/tcp

COPY exports /etc/
COPY nfsd.sh /usr/bin/nfsd.sh
RUN chmod +x /usr/bin/nfsd.sh

EXPOSE 22

ENTRYPOINT /usr/bin/nfsd.sh
