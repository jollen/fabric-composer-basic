
# fabric-composer-basic

Hyperledger Fabric quick start.

# Getting Started

## Prerequisite

* OS: Ubuntu 16.04 or newer
* Machine: AMD x86_64

## Install GO, Node.js (6.x)

Install GO:

```
$ sudo curl -O https://storage.googleapis.com/golang/go1.8.linux-amd64.tar.gz
$ tar zxvf go1.8.linux-amd64.tar.gz
$ sudo mv go /usr/local
```

Add these three lines to ```~/.profile```:

```
export GOROOT=/usr/local/go 
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

Source your profile:

```
$ . ~/.profile
```

Install Node.js:

```
$ curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
$ sudo apt-get install -y nodejs
```

## Install Docker CE, config docker as a non-root user, and docker-compose

```
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo apt-key fingerprint 0EBFCD88    
```

```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

```
$ sudo apt-get update
$ sudo apt-get install docker-ce
```

Add a new ```docker``` group, and put the logined user to this group:

```
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
```

Now, please **log out and log in again**, then install Docker Compose with user *root*:

```
$ sudo su
# curl -L https://github.com/docker/compose/releases/download/1.17.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
# chmod a+x /usr/local/bin/docker-compose 
# exit
```

# Usage

## Download

```
$ sudo apt-get install make
$ git clone https://github.com/jollen/fabric-composer-basic.git
$ cd fabric-composer-basic
```

## Setup Docker Images

Pull required Docker images:

```sh
$ make setup
```

To check all images pulled:

```sh
$ docker images -a
```

## Bootup Fabric Network

After initialization and setup, you can use ```make start``` to start the example Hyperledger fabric network which has 4 peers and 2 organizations and initialize peers:

```sh
$ make start
$ make init
```

The command ```make init``` actually does the following setup:

* create a new application channel `businesschannel`
* join all peers into the channel
* install and instantiate chaincode `example02` for testing

This `make init` command will only need to be done once. 

## Stop the network

To stop the fabric network:

```bash
$ make stop
```

## Clean environment

Clean all Docker containers and images:

```bash
$ make clean
```

You have to ```make init``` again and once before start a new fabric network by ```make start```.

# Readme

* [Official - Hyperledger Fabric Getting Started](http://hyperledger-fabric.readthedocs.io/en/latest/getting_started.html)
* [Official - Hyperledger Fabric](https://github.com/hyperledger/fabric/)
* [Install Hyperledger Fabric 1.0 Quick Start Edit](https://github.com/jollen/Hyperledger-Fabric-Install)
* [docker-compose-files](https://github.com/yeasy/docker-compose-files)
