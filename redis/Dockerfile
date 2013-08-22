# DOCKER-VERSION 0.3.4
FROM    centos:6.4

RUN  rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

ADD . /src

# setup redis
RUN  yum install -y logrotate
RUN  cd /src; rpm -ivh redis-2.6.14-1.el6.x86_64.rpm
RUN echo "1" >> /proc/sys/vm/overcommit_memory
EXPOSE 6379

# setup sshd
RUN yum install -y openssh-server openssh-clients
RUN echo 'root:root' | chpasswd
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config

## Permit error message 'Could not load host key: ...'
RUN /usr/bin/ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -C '' -N ''
RUN /usr/bin/ssh-keygen -t rsa -f /etc/ssh/ssh_host_dsa_key -C '' -N ''
EXPOSE 22

# setup supervisor
RUN yum install -y supervisor
RUN cat /src/Supervisorfile >> /etc/supervisord.conf


CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"] 


# dame...
#CMD /usr/sbin/sshd -D
#CMD ["/usr/sbin/redis-server | (sleep 1 && /usr/sbin/sshd -D)"]
#CMD "/usr/sbin/redis-server"
