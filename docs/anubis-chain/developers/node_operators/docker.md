---
title: Run Anubis Nodes using Docker - Anubis Develop
---

# How to Run A Fullnode Using Anubis Docker Image

## Resources
* Docker image: https://github.com/anubis-chain/anubis/pkgs/container/anubis
* Dockerfile: https://github.com/anubis-chain/anubis/blob/master/Dockerfile

## Supported Platforms

We support running a Anubis docker image on **Mac OS X**, **Linux**, and **Windows**.

## Steps to Run a Fullnode in Docker

### Install Docker
* Desktop Users: https://docs.docker.com/get-docker/
* Ubuntu Linux: https://docs.docker.com/engine/install/ubuntu/

#### Post install:

Start docker during boot up:
```
systemctl enable docker.service
systemctl enable containerd.service
```
Add user "ubuntu" to group docker so the user has privileges to run docker commands:
```
usermod -aG docker ubuntu
```

### Pull Anubis Node Image

* Get latest version: https://github.com/anubis-chain/anubis/pkgs/container/anubis
```
docker pull ghcr.io/anubis-chain/anubis:latest
```

### Download Anubis Node Config Files

Download **genesis.json** and **config.toml** by:

Mainnet
```bash
wget   $(curl -s https://api.github.com/repos/anubis-chain/anubis/releases/latest |grep browser_ |grep mainnet |cut -d\" -f4)
unzip mainnet.zip
```
Testnet
```bash
wget   $(curl -s https://api.github.com/repos/anubis-chain/anubis/releases/latest |grep browser_ |grep testnet |cut -d\" -f4)
unzip testnet.zip
```

### Running Docker Container
1. Dockers Variables and Config file Location

Important **Environment Variables** to note: 
```
$ANUBIS_HOME = /anubis
$DATA_DIR = /data
```
File location:

* ANUBIS_CONFIG=${ANUBIS_HOME}/config/config.toml
* ANUBIS_GENESIS=${ANUBIS_HOME}/config/genesis.json

2. Docker Volumes to Mount

Essentially we need to bind mount two directories: 

|    Mount        | Local  | Docker                     |
| ----------------- | ------------- | -------------------------------------- |
| Blockchain data | data/node | /anubis/node    |
| Config files | config  | /anubis/config  |

3. Download data on local host
Download latest chaindata snapshot from [here](https://github.com/anubis-chain/anubis-snapshots). Follow the guide to structure your files.

4. Start container

You can also use *ETHEREUM OPTIONS* to overwrite settings in the configuration file:
```
docker run -v $(pwd)/config:/anubis/config -v $(pwd)/data/node:/anubis/node -p 8575:8575 --rm --name anubis -it ghcr.io/anubis-chain/anubis:1.0.0_hr --http.addr 0.0.0.0 --http.port 8575 --http.vhosts '*' --verbosity 5 --history.logs 576000
```

> **Note**: Consider adding `--history.logs.disable` for better performance, but `eth_getLogs` will be slower.

* *-p 8575:8575*: This will map port 8575 from host to container, so it exposes 8575 on host node.
* *--http --http.addr 0.0.0.0*: Extra Geth flags to enable RPC and listen on all network interfaces of the container.

**NOTE**: port **8575** is the default port for the RPC service on TESTNET. If you are using mainnet the default port is **8545**.

5. Start Geth console
```
geth attach http://localhost:8575
```
### How to access the container

Execute bash (shell/terminal) on the container named bsc:

```
docker exec -it anubis bash
```
Once logged in you can perform regular tasks you would do on a node without docker.

### How to Check Node Running Status

#### Check Synchronization

Start Geth Console:
```
geth attach ipc:node/geth.ipc
```
Once started, run:
```
>eth.syncing
```
#### Check Geth Logs
```
tail -f node/anubis.log
```
