FROM centos:7

RUN curl -LsS https://rpm.nodesource.com/setup_8.x | bash -

RUN yum install -y nodejs && yum clean all

RUN yum install -y centos-release-scl deltarpm epel-release && yum clean all

RUN yum install -y boost-random btrfs-progs bzip2 ccache cmake cmake3 cryptsetup CUnit-devel Cython \
    devtoolset-7-gcc-c++ expat-devel fuse-devel gcc-c++ git gperf gperftools-devel iproute java-1.8.0-openjdk-devel \
    jq junit keyutils-libs-devel leveldb-devel libaio-devel libbabeltrace-devel libblkid-devel \
    libcurl-devel liboath-devel libtool libtool-ltdl-devel libuuid-devel libxml2-devel lttng-ust-devel lz4-devel mailcap \
    net-tools nss-devel openldap-devel openssl-devel parted python-cherrypy python-coverage python-devel \
    python-jwt python-nose python-pecan python-prettytable python-requests \
    python-routes python-sphinx python-tox python-virtualenv python-werkzeug \
    python2-bcrypt python2-pip python34-Cython python34-devel python34-setuptools rdma-core-devel \
    redhat-lsb-core redhat-rpm-config selinux-policy-devel selinux-policy-doc sharutils snappy-devel socat \
    systemd-devel sudo valgrind-devel xfsprogs xfsprogs-devel xmlsec1 xmlsec1-devel xmlsec1-nss \
    xmlsec1-openssl xmlsec1-openssl-devel xmlstarlet yasm yum-utils wget \
    && yum clean all

RUN sed -i 's/LIBLTDL=1 -I/LIBLTDL=1 -DXMLSEC_NO_SIZE_T -I/' /usr/bin/xmlsec1-config

RUN pip install -U pip \
    && pip install python-saml==2.4.2 tox==2.9.1

RUN curl -LsS -o node_exporter.tar.gz \
    https://github.com/prometheus/node_exporter/releases/download/v0.16.0/node_exporter-0.16.0.linux-amd64.tar.gz \
    && mkdir /opt/node_exporter \
    && tar -xzvf node_exporter.tar.gz --strip 1 -C /opt/node_exporter \
    && rm node_exporter.tar.gz

COPY e2e/google-chrome.repo /etc/yum.repos.d

RUN yum install -y google-chrome-stable && yum clean all

RUN mkdir /ceph

WORKDIR /ceph

ENV PATH="/opt/rh/devtoolset-7/root/usr/bin:$PATH"
ENV PYTHONDONTWRITEBYTECODE="1"

# To increase ccache hit rate
ENV SOURCE_DATE_EPOCH="358228200"
ENV BUILD_DATE="1981-05-09"
