#
# Build it
#
# cd x86_64-apple-darwin
# docker build -t 3dechem/silicosit:darwin .
#
FROM multiarch/crossbuild
MAINTAINER Stefan Verhoeven "s.verhoeven@esciencecenter.nl"

ENV CROSS_TRIPLE=x86_64-apple-darwin

RUN wget -O openbabel-2.4.1.tar.gz 'https://downloads.sourceforge.net/project/openbabel/openbabel/2.4.1/openbabel-2.4.1.tar.gz?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fopenbabel%2Ffiles%2Fopenbabel%2F2.4.1%2F&ts=1502615257&use_mirror=vorboss' && \
    tar -zxf openbabel-2.4.1.tar.gz && cd openbabel-2.4.1  && \
    mkdir build && cd build && \
    crossbuild cmake ..  && \
    find . -type f -exec grep -l soname {} \; |xargs perl -pi -e 's/soname/install_name/'  && \
    crossbuild make  && crossbuild make install  && \
    cd ../.. && \
    wget http://silicos-it.be.s3-website-eu-west-1.amazonaws.com/_downloads/filter-it-1.0.2.tar.gz && \
    tar -zxf filter-it-1.0.2.tar.gz && \
    cd filter-it-1.0.2 && \
    mkdir build && cd build && \
    crossbuild cmake .. && \
    crossbuild make -j 2 && crossbuild make install && \ 
    cd ../.. && \
    rm -r filter-it-1.0.2 filter-it-1.0.2.tar.gz && \
    wget http://silicos-it.be.s3-website-eu-west-1.amazonaws.com/_downloads/strip-it-1.0.2.tar.gz && \
    tar -zxf strip-it-1.0.2.tar.gz && \
    cd strip-it-1.0.2 && \
    mkdir build && cd build && \
    crossbuild cmake .. && \
    crossbuild make -j 2 && crossbuild make install && \ 
    cd ../.. && \
    rm -r strip-it-1.0.2 strip-it-1.0.2.tar.gz && \
    wget http://silicos-it.be.s3-website-eu-west-1.amazonaws.com/_downloads/shape-it-1.0.1.tar.gz && \
    tar -zxf shape-it-1.0.1.tar.gz  && \
    cd shape-it-1.0.1/ && \
    mkdir build && cd build && \
    crossbuild cmake .. && \
    crossbuild make -j 2 && crossbuild make install && \ 
    cd ../.. && \
    rm -r shape-it-1.0.1 shape-it-1.0.1.tar.gz && \
    wget http://silicos-it.be.s3-website-eu-west-1.amazonaws.com/_downloads/align-it-1.0.4.tar.gz && \
    tar -zxf align-it-1.0.4.tar.gz  && \
    cd align-it-1.0.4/ && \
    perl -pi -e 's@/openbabel-2.0@@' cmake/modules/FindOpenBabel2.cmake && \
    mkdir build && cd build && \
    BABEL_INCLUDEDIR=/usr/local/include/openbabel-2.0 crossbuild cmake .. && \
    crossbuild make -j 2 && crossbuild make install && \ 
    cd ../.. && \
    rm -r align-it-1.0.4 align-it-1.0.4.tar.gz
