# aztec-node-setup

###### Beginner-friendly guide to running Aztec node

###### 



\# 🌐 Aztec Node Setup (Beginner Friendly)



This guide explains how to run an Aztec node step by step.  

👉 All commands are shown in copyable code boxes.  

👉 Each step tells you \*\*where to paste the command\*\*.



---



\## Step 1: Connect to Your Server (VPS only)



👉 \*\*Paste this into your laptop terminal\*\* (replace `YOUR\_SERVER\_IP` with your VPS IP):



```bash

ssh root@YOUR\_SERVER\_IP





Enter your VPS password.

Now you’re inside your VPS terminal.



👉 If you’re using your own computer (Linux/Mac/WSL), just open Terminal and skip this step.





Step 2: Update \& Install Tools



👉 Paste this into your VPS or personal device terminal:



apt update \&\& apt upgrade -y

apt install curl git ufw unzip wget htop jq build-essential -y

curl -fsSL https://get.docker.com -o get-docker.sh \&\& sh get-docker.sh

apt install docker-compose -y





Step 3: Create Aztec Folder



👉 Paste into your VPS or personal device terminal:



mkdir aztec

cd aztec



This creates a folder called aztec and moves you inside it.

All files will be created inside this folder.





Step 4: Create .env File



👉 Paste into your VPS or personal device terminal:



nano .env



This opens a blank file in the editor.

👉 Now paste this inside the file (do NOT paste into terminal):



ETHEREUM\_HOST=https://YOUR\_SEPOLIA\_RPC

BEACON\_HOST=https://YOUR\_BEACON\_RPC

PRIVATE\_KEYS=0xYOUR\_PRIVATE\_KEY

COINBASE=0xYOUR\_WALLET\_ADDRESS

P2P\_IP=YOUR\_SERVER\_IP



Replace placeholders with your values:



YOUR\_SEPOLIA\_RPC → from Alchemy/Infura/QuickNode



YOUR\_BEACON\_RPC → beacon RPC URL



YOUR\_PRIVATE\_KEY → your wallet’s private key (SECRET)



YOUR\_WALLET\_ADDRESS → your Ethereum address



YOUR\_SERVER\_IP → VPS IP (or 127.0.0.1 if running locally)



👉 Save file in nano: CTRL+O, Enter → exit with CTRL+X



Step 5: Create docker-compose.yml



👉 Paste into your VPS or personal device terminal:



nano docker-compose.yml



This opens another blank file.



👉 Now paste this inside the file (do NOT paste into terminal):



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



👉 Save file in nano: CTRL+O, Enter → exit with CTRL+X



Step 6: Run Node



👉 Paste into your VPS or personal device terminal (inside aztec folder):



docker compose up -d



👉 Check logs (paste into terminal):



docker logs -f aztec-sequencer



If you see:

Downloaded L2 Block...



🎉 Your node is working.



Step 7: Open Ports (VPS only)



👉 Paste into your VPS terminal:



ufw allow ssh

ufw allow 40400/tcp

ufw allow 40400/udp

ufw allow 8080/tcp

ufw enable



Step 8: Optional — Dozzle Log Viewer



👉 Paste into your VPS or personal device terminal:



docker run -d --name dozzle \\

&nbsp; -v /var/run/docker.sock:/var/run/docker.sock \\

&nbsp; -p 9999:8080 amir20/dozzle:latest



Then open in browser:



VPS → http://YOUR\_SERVER\_IP:9999



Local → http://localhost:9999

