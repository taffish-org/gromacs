FROM ghcr.io/taffish-org/debian:12

LABEL maintainer="taffish@163.com"

WORKDIR /root

RUN apt-get update && apt-get install -y curl git gcc g++ make cmake libssl-dev

RUN cd / && curl -LO https://github.com/Kitware/CMake/archive/refs/tags/v3.31.5.tar.gz && \
    tar -zxvf /v3.31.5.tar.gz && rm /v3.31.5.tar.gz && cd /CMake-3.31.5/ && \
    /CMake-3.31.5/bootstrap && make && make install && cp /CMake-3.31.5/bin/cmake /usr/local/bin/

RUN cd / && curl -LO https://github.com/gromacs/gromacs/archive/refs/tags/v2025.1.tar.gz && \
    tar -zxvf /v2025.1.tar.gz && rm /v2025.1.tar.gz && cd /gromacs-2025.1/ && \
    mkdir /gromacs-2025.1/build/ && cd /gromacs-2025.1/build/ && \
    cmake .. -DGMX_BUILD_OWN_FFTW=ON -DREGRESSIONTEST_DOWNLOAD=ON && \
    make && make check && make install && . /usr/local/gromacs/bin/GMXRC

ENV PATH=/gromacs-2025.1/build/bin:${PATH}

ENV TAFFISH_ENV=TAFFISH
ENV TAFFISH_NAME=gromacs
