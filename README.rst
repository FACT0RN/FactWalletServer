.. image:: https://api.cirrus-ci.com/github/spesmilo/electrumx.svg?branch=master
    :target: https://cirrus-ci.com/github/spesmilo/electrumx
.. image:: https://coveralls.io/repos/github/spesmilo/electrumx/badge.svg
    :target: https://coveralls.io/github/spesmilo/electrumx

===============================================
ElectrumX - Reimplementation of electrum-server
===============================================

  :Licence: MIT
  :Language: Python (>= 3.8)
  :Original Author: Neil Booth

This project is a fork of `kyuupichan/electrumx <https://github.com/kyuupichan/electrumx>`_.
The original author dropped support for Bitcoin, which we intend to keep.

ElectrumX allows users to run their own Electrum server. It connects to your
full node and indexes the blockchain, allowing efficient querying of the history of
arbitrary addresses. The server can be exposed publicly, and joined to the public network
of servers via peer discovery. As of May 2020, a significant chunk of the public
Electrum server network runs ElectrumX.

Documentation
=============

See `readthedocs <https://electrumx-spesmilo.readthedocs.io/>`_.


Docker
======

docker build --tag fac_elecrum .

docker run -ti -v /data/git/electrumx/:/home/electrumx/electrumx --network host  fac_elecrum bas


FACT0RN SPECIFICS
=================

To run the FACT0RN Wallet Server you will need to modify a couple of things in docker/Dockerfile:

1. Line [32](https://github.com/FACT0RN/FactWalletServer/blob/master/docker/Dockerfile#L32): edit to write your fact0rn daemon's username and password.
2. The keys and certificates in the ``docker/certs`` path need to be unique to your server for security reasons. Create new ones and replace the ones there.
3. Only after doing steps 1 and 2, we now build the docker container from the docker folder.
4. Run the container as specified on the Docker section above. You may want to add `` --ulimit nofile=18000:200000`` to that docker command. Not needed, but if you have enough connections it might help.


