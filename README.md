# aztec-node-setup

###### Beginner-friendly guide to running Aztec node

###### 



###### \# 🌐 Aztec Node Setup (Beginner Friendly)



This guide explains how to run an Aztec node step by step.  

It tells you exactly \*\*what to copy-paste into terminal\*\*, \*\*what to paste into files\*\*, and \*\*what not to paste anywhere\*\*.



---



##### \## 🖥️ Step 1: Choose Where to Run



\### Option A: Own Device

\- Use Linux (Ubuntu 22.04) or Mac.  

\- Open \*\*Terminal app\*\* → run commands there.  

\- Windows users → install WSL Ubuntu or use VPS.



\### Option B: VPS (Recommended)

Rent a server from:

\- Contabo, Hetzner, Vultr, DigitalOcean  



Specs: \*\*4 CPU, 8 GB RAM, 250 GB SSD, Ubuntu 22.04\*\*.  

Provider gives you: IP address, username (`root`), password.



---



##### \## 🔌 Step 2: Connect to Server

###### 

###### \### If using own device

###### Just open \*\*Terminal\*\* → skip to Step 3.



###### \### If using VPS

👉 \*\*Copy-paste into your laptop terminal\*\* (replace `YOUR\_SERVER\_IP`):  

```bash

ssh root@YOUR\_SERVER\_IP





Then enter your VPS password.

Now you’re inside your server terminal.











##### **🔄 Step 3: Update \& Install Tools**

###### 

###### **👉 Copy-paste into server terminal:**



apt update \&\& apt upgrade -y

apt install curl git ufw unzip wget htop jq build-essential -y

curl -fsSL https://get.docker.com -o get-docker.sh \&\& sh get-docker.sh

apt install docker-compose -y











##### 📂 Step 4: Make Aztec Folder

###### 

###### 👉 Copy-paste into server terminal:



mkdir aztec

cd aztec











##### 📝 Step 5: Create .env File

###### 

###### 1 👉 Copy-paste into server terminal:



nano .env





###### This opens a text editor.

###### 

###### 2 👉 Now paste the following text inside the editor (DO NOT paste this into terminal directly):



ETHEREUM\_HOST=https://YOUR\_SEPOLIA\_RPC  

BEACON\_HOST=https://YOUR\_BEACON\_RPC  

PRIVATE\_KEYS=0xYOUR\_PRIVATE\_KEY   # SECRET, never share  

COINBASE=0xYOUR\_WALLET\_ADDRESS  

P2P\_IP=YOUR\_SERVER\_IP  



###### 

###### 3 Replace placeholders:



YOUR\_SEPOLIA\_RPC → from Alchemy/Infura/QuickNode



YOUR\_BEACON\_RPC → from provider



YOUR\_PRIVATE\_KEY → your wallet’s private key (secret)



YOUR\_WALLET\_ADDRESS → your Ethereum address



###### 

###### 4 Save file:



CTRL + O, Enter → saves



CTRL + X → exits editor



YOUR\_SERVER\_IP → your VPS/public IP







##### 📝 Step 6: Create docker-compose.yml



###### 1 👉 Copy-paste into server terminal:



nano docker-compose.yml





###### 2 This opens a text editor.

###### 👉 Now paste the following text inside the editor (DO NOT paste this into terminal directly):

###### 

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



###### 3 Save file:



CTRL + O, Enter → saves



CTRL + X → exits editor



###### 👉 Now your aztec folder contains 2 files: .env and docker-compose.yml.









##### 🚀 Step 7: Run the Node



###### 👉 Copy-paste into server terminal:



docker compose up -d





###### Check logs:



docker logs -f aztec-sequencer





###### If you see:



Downloaded L2 Block...



###### 🎉 Your node is running.





##### ⚠️ Secrets \& Replacements



PRIVATE\_KEYS → secret, never post online



YOUR\_SEPOLIA\_RPC / YOUR\_BEACON\_RPC → RPC URLs from provider



YOUR\_WALLET\_ADDRESS → your Ethereum wallet



YOUR\_SERVER\_IP → your VPS IP (check with hostname -I)





###### ✅ Done!



You now have an Aztec node live.



###### Optional log viewer (Dozzle):

👉 Copy-paste into server terminal:



docker run -d --name dozzle \\

&nbsp; -v /var/run/docker.sock:/var/run/docker.sock \\

&nbsp; -p 9999:8080 amir20/dozzle:latest





###### Then open in browser:

###### http://YOUR\_SERVER\_IP:9999



###### 

