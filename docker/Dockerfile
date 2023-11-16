FROM ubuntu:22.04

RUN apt update && apt install -y gcc g++ git cmake make libtool libleveldb-dev python3-pip daemontools-run tree vim  

RUN useradd --no-log-init --system --create-home --shell /bin/bash -G sudo -g sudo  -G root -g root -u 1001 electrumx

USER electrumx
WORKDIR /home/electrumx

RUN git clone https://github.com/spesmilo/electrumx.git \
    && cd electrumx \
    && pip install . \
    && pip install .[ujson]

RUN    mkdir -p /home/electrumx/db  \
    && mkdir service                \
    && mkdir logs                   \
    && mkdir -p scripts/electrumx   \
    && cp -R /home/electrumx/electrumx/contrib/daemontools/* /home/electrumx/scripts/electrumx \ 
    && cd /home/electrumx/service \
    && ln -s ~/scripts/electrumx/ electrumx

RUN mkdir certs

COPY --chown=electrumx certs/ certs

RUN echo "/home/electrumx/electrumx/electrumx_server"                > /home/electrumx/scripts/electrumx/env/ELECTRUMX
RUN echo "FACT0RN"                                                   > /home/electrumx/scripts/electrumx/env/COIN
RUN echo "mainnet"                                                   > /home/electrumx/scripts/electrumx/env/NET
RUN echo "/home/electrumx/db"                                        > /home/electrumx/scripts/electrumx/env/DB_DIRECTORY
RUN echo "electrumx"                                                 > /home/electrumx/scripts/electrumx/env/USERNAME
RUN echo "http://JPApoej89Djk:Lkja09KdpAo9_sd@127.0.0.1:8332"        > /home/electrumx/scripts/electrumx/env/DAEMON_URL
RUN echo "#!/bin/sh\nexec multilog s500000 n10 /home/electrumx/logs" > /home/electrumx/service/electrumx/log/run
RUN echo "/home/electrumx/certs/server.crt"                          > /home/electrumx/service/electrumx/env/SSL_CERTFILE
RUN echo "/home/electrumx/certs/server.key"                          > /home/electrumx/service/electrumx/env/SSL_KEYFILE
RUN echo ""                                                          > /home/electrumx/service/electrumx/env/PEER_ANNOUNCE
RUN echo echo "rpc://127.0.0.1:8000,tcp://127.0.0.1:50001,ssl://127.0.0.1:50002"> /home/electrumx/service/electrumx/env/SERVICES






