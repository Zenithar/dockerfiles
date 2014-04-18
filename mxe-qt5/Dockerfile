FROM zenithar/mxe:latest

MAINTAINER Thibault NORMAND <me@zenithar.org>

RUN git clone https://github.com/mxe/mxe.git /opt/mxe
WORKDIR /opt/mxe
RUN make gcc
RUN make qt5

