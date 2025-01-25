



# Use the minimal Debian image
FROM debian:stable-slim

# Installs required dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    wget \
    curl \
    gnupg \
    build-essential \
    libxml2-dev \
    libncurses5-dev \
    libsqlite3-dev \
    uuid-dev \
    libjansson-dev \
    libssl-dev \
    libedit-dev \
    pkg-config \
    bzip2 \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Installs pjproject manually, bypassing SSL certificate verification
WORKDIR /usr/src
RUN wget https://github.com/pjsip/pjproject/archive/refs/tags/2.14.1.tar.gz  --no-check-certificate && \
    tar zxvf 2.14.1.tar.gz && \
    cd pjproject-2.14.1 && \
    ./configure CFLAGS="-DNDEBUG -DPJ_HAS_IPV6=1" --prefix=/usr/local --enable-shared && \
    make && make install && ldconfig && \
    rm -rf /usr/src/2.14.1.tar.gz* /usr/src/pjproject-2.14.1

# Downloads and installs Asterisk 21, disabling the use of built-in pjproject
RUN wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-21-current.tar.gz && \
    tar zxvf asterisk-21-current.tar.gz && \
    cd asterisk-21.* && \
    export LD_LIBRARY_PATH=/usr/local/lib && \
    export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig && \
    ./configure --without-pjproject-bundled --with-pjproject=/usr/local --with-ssl=openssl && \
    make menuselect.makeopts && \
    make && \
    make install && \
    make samples && \
    make config && \
    ldconfig && \
    rm -rf /usr/src/asterisk-21*

# Configures the network ports for Asterisk
EXPOSE 5060/udp
EXPOSE 10000-10100/udp

# Runs Asterisk
CMD ["/usr/sbin/asterisk", "-vvv", "-f"]




