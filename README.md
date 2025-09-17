# aztec-node-setup

###### Beginner-friendly guide to running Aztec node

###### 



###### \# 🌐 Aztec Node Setup (Beginner Friendly)

###### 

###### This guide explains how to run an Aztec node.  

###### Only copy-paste commands are in code blocks with the GitHub “copy” button.

###### 

###### ---

###### 

###### \## Step 1: Connect to Server (VPS only)

###### 

###### ```bash

###### ssh root@YOUR\_SERVER\_IP



Step 2: Update \& Install Tools

apt update \&\& apt upgrade -y

apt install curl git ufw unzip wget htop jq build-essential -y

curl -fsSL https://get.docker.com -o get-docker.sh \&\& sh get-docker.sh

apt install docker-compose -y



Step 3: Make Folder

mkdir aztec

cd Aztec



Step 4: Create .env File



Open file:



nano .env





Paste inside file (⚠️ do not paste into terminal):



ETHEREUM\_HOST=https://YOUR\_SEPOLIA\_RPC

BEACON\_HOST=https://YOUR\_BEACON\_RPC

PRIVATE\_KEYS=0xYOUR\_PRIVATE\_KEY

COINBASE=0xYOUR\_WALLET\_ADDRESS

P2P\_IP=YOUR\_SERVER\_IP





Save in nano: CTRL+O, Enter → CTRL+X.



Step 5: Create docker-compose.yml



Open file:



nano docker-compose.yml





Paste inside file:



version: '3.8'

services:

&nbsp; sequencer:

&nbsp;   image: aztecprotocol/aztec:latest

&nbsp;   container\_name: aztec-sequencer

&nbsp;   restart: always

&nbsp;   env\_file: .env

&nbsp;   ports:

&nbsp;     - "40400:40400/tcp"

&nbsp;     - "40400:40400/udp"

&nbsp;     - "8080:8080"



Step 6: Run Node

docker compose up -d





Check logs:



docker logs -f aztec-sequencer



Optional: Open Ports (VPS only)

ufw allow ssh

ufw allow 40400/tcp

ufw allow 40400/udp

ufw allow 8080/tcp

ufw enable





Optional: Dozzle Log Viewer

docker run -d --name dozzle \\

&nbsp; -v /var/run/docker.sock:/var/run/docker.sock \\

&nbsp; -p 9999:8080 amir20/dozzle:latest

