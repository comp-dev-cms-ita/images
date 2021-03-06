FROM htcondor/execute:8.9.9-el7

ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
RUN chmod +x /bin/tini

RUN cd /etc/yum.repos.d \
    && wget https://repo.data.kit.edu/data-kit-edu-centos7.repo

RUN yum -y update \
    && yum -y install \
    binutils \
    bzip2-devel \
    cmake3 \
    dnf \
    gcc \
    gcc-c++ \
    gdbm-devel \
    git \
    jq \
    libffi-devel \
    libmicrohttpd \
    libseccomp \
    libsecret \
    libsodium \
    libuuid-devel \
    libX11-devel \
    libXext-devel \
    libXft-devel \
    libXpm-devel \
    make \
    openssl-devel \
    python \
    readline-devel \
    singularity \
    sqlite-devel \
    xz-devel \
    yad \
    zlib-devel

RUN dnf -y install oidc-agent-4.2.4 \
    && yum clean all \
    && rm -rf /var/cache/yum

# Overwrite python3 with python3.7 (Dask requirement)
RUN cd /usr/src \
    && wget https://www.python.org/ftp/python/3.7.12/Python-3.7.12.tgz \
    && tar xzf Python-3.7.12.tgz \
    && rm Python-3.7.12.tgz \
    && cd Python-3.7.12 \
    && ./configure --enable-optimizations \
    && make install

RUN python3 -m pip install -U pip setuptools wheel

# centos base packages
RUN pip3 install \
    chardet==3.0.4 \
    htcondor==8.9.9 \
    idna==2.7 \
    PySocks==1.6.8 \
    requests==2.14.2 \
    six==1.14.0 \
    urllib3==1.25.6

# Base dependencies
RUN pip3 install \
    click==7.1.2 \
    ipython \
    ipywidgets==7.6.5 \
    jupyter-server-proxy==3.1.0 \
    jupyterhub==1.5.0 \
    jupyterlab==3.2.2 \
    notebook==6.4.5 \
    toolz==0.11.1
