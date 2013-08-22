# DOCKER-VERSION 0.3.4
FROM    centos:6.4
MAINTAINER Tabito Ohtani "koko1000ban@gmail.com"

ADD . /pub

RUN yum groupinstall -y "Development Tools"
RUN yum install -y openssh-server openssh-clients
RUN echo 'root:root' | chpasswd
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config

# Suppress error message 'Could not load host key: ...'
RUN /usr/bin/ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -C '' -N ''
RUN /usr/bin/ssh-keygen -t rsa -f /etc/ssh/ssh_host_dsa_key -C '' -N ''

# key authorization
RUN mkdir /root/.ssh
RUN cat /pub/id_rsa.pub > /root/.ssh/authorized_keys
RUN chmod 700 /root/.ssh
RUN chmod 600 /root/.ssh/authorized_keys

EXPOSE 22
CMD /usr/sbin/sshd -D
