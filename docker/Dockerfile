FROM ubuntu:22.04

RUN apt update && apt install -y gcc g++ git cmake make libtool libleveldb-dev python3-pip daemontools-run tree vim s6

RUN useradd --no-log-init --system --create-home --shell /bin/bash -G sudo -g sudo  -G root -g root -u 1001 electrumx

USER electrumx
WORKDIR /home/electrumx/electrumx

COPY . .

RUN    pip install -c constraints.txt . \
    && pip install -c constraints.txt .[ujson] \
    && pip install -c constraints.txt "aiorpcx==0.22.0" \
    && pip install -c constraints.txt pylru

WORKDIR /home/electrumx

RUN    mkdir -p /home/electrumx/db  \
    && mkdir -p /home/electrumx/service                \
    && mkdir -p /home/electrumx/logs                   \
    && mkdir -p /home/electrumx/scripts/electrumx   \
    && mkdir -p /home/electrumx/certs \
    && cp -R /home/electrumx/electrumx/contrib/daemontools/* /home/electrumx/scripts/electrumx \
    && cd /home/electrumx/service \
    && ln -s /home/electrumx/scripts/electrumx/ electrumx

COPY --chown=electrumx docker/certs/ certs

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
RUN echo "tcp://:50001,ssl://:50002,ws://:50003,wss://:50004"        > /home/electrumx/service/electrumx/env/SERVICES
RUN echo "0"                                                         > /home/electrumx/service/electrumx/env/COST_SOFT_LIMIT
RUN echo "0"                                                         > /home/electrumx/service/electrumx/env/COST_HARD_LIMIT

ENTRYPOINT ["/usr/bin/s6-svscan","/home/electrumx/service"]

