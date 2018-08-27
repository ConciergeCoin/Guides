# Linux VPS CCC Daemon Installation Guide

## Connect to your Linux VPS over SSH

  * Use your favorite terminal application on Linux or Putty/Bitvise clients on Windows
  * Connect to a terminal session with the Linux VPS
  
## Update your system to the latest

  * From the terminal session, run the following commands
  ```
  sudo apt-get update
  sudo apt-get upgrade
  ```
  
## Download the CCC Linux Daemon

  * From the terminal session, run the following command
  ```
  wget https://github.com/ConciergeCoin/Concierge/releases/download/V1.0.0.0/Concierge-linux.tar.gz
  ```
  * From the terminal session, run the following command
  ```
  tar -xvf Concierge-linux.tar.gz
  ```
  
## Install CCC Linux Daemon Runtime Dependencies

  * From the terminal session, run the following commands
  ```
  sudo apt autoremove -y && sudo apt-get update
  sudo apt-get install -y libzmq3-dev libminiupnpc-dev libssl-dev libevent-dev
  sudo apt-get install -y build-essential libtool autotools-dev automake pkg-config
  sudo apt-get install -y bsdmainutils software-properties-common
  sudo apt-get install -y libboost-all-dev
  sudo add-apt-repository ppa:bitcoin/bitcoin -y
  sudo apt-get update
  sudo apt-get install -y libdb4.8-dev libdb4.8++-dev
  ```
  
## Create your CCC Linux Daemon configuration file

* From the terminal session, run the following commands
```
mkdir -p ~/.concierge
nano ~/.concierge/concierge.conf
```

* Now add the following lines to this file, replacing any < > field with your information
  * Note: If your setting up a Linux Hot/Cold Wallet, comment out the masternode entries
```
rpcuser=<rpcusername>
rpcpassword=<rpcpassword>
rpcport=51471
listen=1
server=1
daemon=1
staking=0
rpcallowip=127.0.0.1
logtimestamps=1
masternode=1
port=51470
externalip=<externalip>:51470
masternodeprivkey=<masternode private key>
```

* Get the latest node seeds 
* Copy and paste the addnode lines into the bottom of this file
* Save and Exit

## Start the CCC Linux Daemon

* From the terminal session, run the following commands
```
./concierged
```

## Wait for the CCC Linux Daemon to sync

* From the terminal session, run the following commands
```
watch ./concierge-cli getinfo
```
* Compare the "Block Height" value with the latest from the block explorer. When those are the same, your daemon is synchronized 
