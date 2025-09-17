# aztec-node-setup

###### Beginner-friendly guide to running Aztec node

###### 



\# 🌐 Aztec Node Setup (Beginner Friendly)



This guide explains how to run an Aztec node step by step.  

👉 All commands are in copyable code boxes.  

👉 Each step tells you \*\*where to paste the command\*\*.



---



\## Step 1: Connect to Your Server (VPS only)



👉 \*\*Paste into your laptop terminal\*\* (replace `YOUR\_SERVER\_IP`):



```bash

ssh root@YOUR\_SERVER\_IP```





Enter your VPS password.

Now you’re inside your VPS terminal.



👉 If you’re using your own computer (Linux/Mac/WSL), just open Terminal and skip this step.





Step 2: Update \& Install Tools



👉 Paste into your VPS or personal device terminal:



```apt update \&\& apt upgrade -y

apt install curl git ufw unzip wget htop jq build-essential -y

curl -fsSL https://get.docker.com -o get-docker.sh \&\& sh get-docker.sh

apt install docker-compose -y```



Step 3: Create Aztec Folder



👉 Paste into your VPS or personal device terminal:



```mkdir aztec

cd aztec```









