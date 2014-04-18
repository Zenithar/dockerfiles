FROM ubuntu:13.10

MAINTAINER Thibault NORMAND <me@zenithar.org>

RUN echo "deb http://llvm.org/apt/saucy/ llvm-toolchain-saucy-3.4-binaries main" >> /etc/apt/sources.list
RUN echo "deb-src http://llvm.org/apt/saucy/ llvm-toolchain-saucy-3.4-binaries main" >> /etc/apt/sources.list

RUN apt-get -y update && apt-get -y --force-yes install autoconf automake \ 
		       bash bison bzip2 \
                       cmake flex gettext git g++ intltool \
                       libffi-dev libtool libltdl-dev libssl-dev \
                       libxml-parser-perl make openssl patch perl \
                       pkg-config scons sed unzip wget xz-utils \
		       g++-multilib libc6-dev-i386 \
		       clang-3.4-dev clang-3.4 autopoint


