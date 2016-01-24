Bitcoin Core Vagrant
============

[![License](http://img.shields.io/:License-MIT-yellow.svg)](LICENSE)

You probably want to adjust the bitcoin.conf file before you start the VM.

Starting the Vagrant VM:

> vagrant up

Access Bitcoin Core (from inside or outsite the VM):

> bitcoin-cli -rpcuser=bitcoinrpc -rpcpassword=password getinfo

Login to the VM:

> vagrant ssh
