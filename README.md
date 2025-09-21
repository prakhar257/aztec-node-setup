# aztec-node-setup

###### Beginner-friendly guide to running Aztec node

###### 



\# 🌐 Aztec Node Setup (Beginner Friendly)



This guide explains how to run an Aztec node step by step.  

👉 All commands are in copyable code boxes.  

👉 Each step tells you \*\*where to paste the command\*\*.



## Step 1: Connect to VPS  

👉 Paste this into your **laptop terminal** (replace `YOUR_SERVER_IP` with your server’s IP):  

```bash
ssh root@YOUR_SERVER_IP

## Step 2: Update & Install Tools  

👉 Paste this into your **VPS terminal** (or your own device terminal if running locally):  

```bash
apt update && apt upgrade -y
apt install curl git ufw unzip wget htop jq build-essential -y
curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh
apt install docker-compose -y
## Step 3: Create Aztec Folder  

👉 Paste this into your **VPS terminal** (or your own device terminal if running locally):  

```bash
mkdir aztec
cd aztec

## Step 4: Create `.env` File  

👉 Paste this into your **VPS or local terminal** to open the file in an editor:  

```bash
nano .env

ETHEREUM_HOST=https://YOUR_SEPOLIA_RPC
BEACON_HOST=https://YOUR_BEACON_RPC
PRIVATE_KEYS=0xYOUR_PRIVATE_KEY
COINBASE=0xYOUR_WALLET_ADDRESS
P2P_IP=YOUR_SERVER_IP

## Step 5: Create `docker-compose.yml` File  

👉 Paste this into your **VPS or local terminal** to open the file in an editor:  

```bash
nano docker-compose.yml

version: '3.8'
services:
  sequencer:
    image: aztecprotocol/aztec:latest
    container_name: aztec-sequencer
    restart: always
    env_file: .env
    ports:
      - "40400:40400/tcp"
      - "40400:40400/udp"
      - "8080:8080"

👉 Save file in nano:

CTRL + O, press Enter

CTRL + X to exit

## Step 6: Run the Node  

👉 Paste this into your **VPS or local terminal** (make sure you are inside the `aztec` folder):  

```bash
docker compose up -d

docker logs -f aztec-sequencer

If you see lines like:

Downloaded L2 Block..
🎉 Your node is working successfully.

## Step 7: Open Ports (VPS only)  

👉 Paste this into your **VPS terminal** to allow required ports:  

```bash
ufw allow ssh
ufw allow 40400/tcp
ufw allow 40400/udp
ufw allow 8080/tcp
ufw enable

## Step 8: Optional — Dozzle Log Viewer  

👉 Paste this into your **VPS or local terminal** to run Dozzle:  

```bash
docker run -d --name dozzle \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -p 9999:8080 amir20/dozzle:latest

👉 Then open in your browser:

VPS → http://YOUR_SERVER_IP:9999

Local → http://localhost:9999

## ⚠️ Final Notes  

- `.env` file contains your **private key** → never share it or upload it to GitHub.  
- Replace placeholders (`YOUR_SEPOLIA_RPC`, `YOUR_BEACON_RPC`, `YOUR_PRIVATE_KEY`, `YOUR_WALLET_ADDRESS`, `YOUR_SERVER_IP`) with your actual details.  
- Use `YOUR_SERVER_IP` for VPS, or `127.0.0.1` if running locally.  
- Only **terminal commands** are inside copy boxes in this guide.  
- File contents (`.env`, `docker-compose.yml`) are shown as plain text → copy them manually into files.  

