FROM stackbrew/ubuntu:14.04
MAINTAINER Thibault NORMAND <me@zenithar.org>

# Environment
ENV DEBIAN_FRONTEND noninteractive

# Fix locales
RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales

# Update Ubuntu
RUN echo udev hold | dpkg --set-selections && \
    echo initscripts hold | dpkg --set-selections && \
    echo upstart hold | dpkg --set-selections && \
    apt-get update -q && \
    apt-get -y upgrade

# Prevent daemon start during install
RUN echo "#!/bin/sh\nexit 101" > /usr/bin/policy-rc.d && \
    chmod +x /usr/bin/policy-rc.d

# Supervisord
RUN apt-get install -y supervisor && \
    mkdir -p /var/log/supervisor

# SSHD
RUN apt-get install -y openssh-server && \
    mkdir /var/run/sshd && \
    echo 'root:root' | chpasswd

# Utilities
RUN apt-get install -y vim less net-tools inetutils-ping curl git telnet nmap socat

# Others
RUN apt-get install -y vlan bridge-utils

# Python MysqlDB
RUN apt-get install -y python python-mysqldb

