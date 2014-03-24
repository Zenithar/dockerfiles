# Inspired from mboersma/znc

FROM stackbrew/ubuntu:13.10
MAINTAINER Thibault NORMAND <me@zenithar.org>

ENV DEBIAN_FRONTEND noninteractive

# install ZNC build prerequisites
RUN apt-get install -yq --force-yes coreutils g++ libssl-dev make wget
# build and install ZNC
RUN cd /usr/src && wget http://znc.in/releases/znc-1.2.tar.gz && tar zxvf znc-1.2.tar.gz
WORKDIR /usr/src/znc-1.2
RUN ./configure && make && make install

# clean up
RUN rm -Rf /usr/src/znc-1.2*
RUN apt-get remove -yq g++ libssl-dev make
RUN apt-get autoremove -yq && apt-get clean

# run ZNC as an unprivileged user
RUN useradd -m -d /opt/znc znc
ADD run /opt/znc/run
RUN chmod +x /opt/znc/run
RUN chown -R znc:znc /opt/znc
RUN touch /opt/znc/.oidentd.conf && chmod 644 /opt/znc/.oidentd.conf
RUN chmod 711 /opt/znc

# run thie image as a ZNC server
WORKDIR /opt/znc

ENTRYPOINT ["/opt/znc/run"]
