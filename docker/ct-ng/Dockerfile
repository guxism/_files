FROM ubuntu:16.04


RUN useradd -m ctng && echo "ctng:ctng" | chpasswd && \
    addgroup wheel && \
    usermod -aG wheel ctng

RUN apt-get update
RUN apt-get install -y gcc g++ gperf bison flex texinfo help2man make libncurses5-dev \
    python3-dev autoconf automake libtool libtool-bin gawk wget bzip2 xz-utils unzip \
    patch libstdc++6 git libelf-dev vim

USER ctng
WORKDIR /home/ctng

RUN wget http://crosstool-ng.org/download/crosstool-ng/crosstool-ng-1.23.0.tar.xz && tar xvf crosstool-ng-1.23.0.tar.xz

WORKDIR /home/ctng/crosstool-ng
RUN git show --summary && \
    ./bootstrap && \
    ./configure --prefix=/home/ctng/.local && \
    make && \
    make install
ENV PATH=/home/ctng/.local/bin:$PATH

WORKDIR /home/ctng/
