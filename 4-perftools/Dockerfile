FROM centos:centos7
MAINTAINER Red Hat, Inc.

RUN yum install -y centos-release-scl-rh && \
    INSTALL_PKGS="devtoolset-4-systemtap devtoolset-4-valgrind devtoolset-4-dyninst devtoolset-4-dyninst-devel devtoolset-4-elfutils devtoolset-4-elfutils-devel devtoolset-4-oprofile devtoolset-4-oprofile-jit devtoolset-4-oprofile-devel" && \
    yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y

# Each language image can have 'contrib' a directory with extra files needed to
# run and build the applications.
COPY ./contrib/ /root

ENV HOME=/root \
    PATH=/root/bin:/opt/rh/devtoolset-4/root/usr/bin/:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN mkdir -p ${HOME} && \
    chmod u+x /root/bin/usage

USER 0

WORKDIR ${HOME}

ADD contrib/etc/scl_enable /root/etc/scl_enable

# Enable the SCL for all bash scripts.
ENV BASH_ENV=/root/etc/scl_enable \
    ENV=/root/etc/scl_enable \
    PROMPT_COMMAND=". /root/etc/scl_enable"

# Set the default CMD to print the usage of the perftools image
ENTRYPOINT ["container-entrypoint"]
CMD ["usage"]
