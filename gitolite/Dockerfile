FROM stackbrew/ubuntu:13.10
MAINTAINER Thibault NORMAND <me@zenithar.org>

# update packages
ENV DEBIAN_FRONTEND noninteractive
RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E1DD270288B4E6030699E45FA1715D88E1DF1F24
RUN echo "deb http://ppa.launchpad.net/git-core/ppa/ubuntu saucy main" >> /etc/apt/sources.list
RUN apt-get update && apt-get -y install git openssh-server
RUN mkdir -p /var/run/sshd

# fetch the gitolite source (latest upstream by default)...
RUN umask 0022
RUN mkdir -p /usr/local/src
RUN git clone git://github.com/sitaramc/gitolite /usr/local/src/gitolite

# install gitolite...
RUN /usr/local/src/gitolite/install -to /usr/local/bin

# install our run script
RUN mkdir -p /usr/local/sbin
ADD gitolite-run /usr/local/sbin/gitolite-run
RUN chown root.root /usr/local/sbin/gitolite-run && chmod 0755 /usr/local/sbin/gitolite-run

# ...and our admin public key
ADD admin.pub /usr/local/src/admin.pub
RUN chown root.root /usr/local/src/admin.pub && chmod 0644 /usr/local/src/admin.pub

# add our gitolite system user
RUN useradd --home /srv/git --system --comment 'gitolite system user' git

# our externally bits.
VOLUME ["/srv"]
EXPOSE 22
ENTRYPOINT ["/usr/local/sbin/gitolite-run"]

# --------------
#
# These will be run as part of the initial build of any *children* containers.
# This should allow us to be able to easily create containers with specific
# ssh keypairs.

# builds FROM this one will do the full install to the /srv volume -- this is
# handled in gitolite-run, however.

ONBUILD ADD admin.pub /usr/local/src/admin.pub

