FROM centos:centos7.9.2009

RUN yum -y update 

RUN mkdir -p /home/local/java
COPY ./jdk-8u341-linux-x64.tar.gz /home/local/java
RUN tar -zxvf /home/local/java/jdk-8u341-linux-x64.tar.gz -C /home/local/java

ENV JAVA_HOME=/home/local/java/jdk1.8.0_341
ENV PATH=$JAVA_HOME/bin:$PATH
ENV CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

RUN yum install -y net-tools curl netcat perl nc which openssh-server openssh-clients  openssl openssl-devel

# ssh.
RUN ssh-keygen -q -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key -N '' 
RUN ssh-keygen -q -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key -N ''
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_ed25519_key -N ''

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/.*StrictHostKeyChecking ask/StrictHostKeyChecking no/' /etc/ssh/ssh_config

# 直接在此处设置免密登录,便于后续的操作。
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa && \ 
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
    chmod 700 ~/.ssh && \
    chmod 600 ~/.ssh/id_rsa && \
    chmod 644 ~/.ssh/authorized_keys

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]


