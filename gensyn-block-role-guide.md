# 💻 Gensyn RL-Swarm Guide

## System Requirements

| Requirement         | Details                                           |
|--------------------|---------------------------------------------------|
| CPU Architecture    | arm64 or amd64                                   |
| Recommended RAM     | 24 GB                                            |
| CUDA Devices        | RTX 3090, RTX 4070, RTX 4090, A100, H100       |
| Python Version      | >= 3.10                                          |

## Rent GPU (Optional)
- Visit: [Quick Pod](https://console.quickpod.io)
- Sign up and verify email
- Deposit funds (crypto or credit card)
- Select Ubuntu 22.04
- Choose GPU (RTX 4090 recommended)
- Click “Create POD”
- Connect via Web Terminal or SSH

## Connect via SSH (GPU Only)
```bash
ssh-keygen
cat ~/.ssh/id_rsa.pub
```
- Copy the public key to GPU provider
- SSH into your GPU server

## Installation
```bash
sudo apt update && sudo apt install -y sudo python3 python3-venv python3-pip curl wget screen git lsof nano unzip iproute2 build-essential gcc g++
```
- Install CUDA:
```bash
curl -o cuda.sh https://raw.githubusercontent.com/zunxbt/gensyn-testnet/main/cuda.sh && chmod +x cuda.sh && . ./cuda.sh
```
- Create screen session:
```bash
screen -S gensyn
```
- Clone rl-swarm repo:
```bash
git clone https://github.com/gensyn-ai/rl-swarm.git
cd rl-swarm
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

## Tunnel localhost (optional)
- Install localtunnel:
```bash
npm install -g localtunnel
lt --port 3000
```

## Backups
- Backup `swarm.pem` file:
```bash
scp username@vps_ip:~/rl-swarm/swarm.pem ~/swarm.pem
```

## Node Status
- Check logs:
```bash
screen -r gensyn
```
- Detach from screen: `Ctrl+A` then `D`

## Troubleshooting
- Daemon failed to start in 15s:
```bash
nano $(python3 -c "import hivemind.p2p.p2p_daemon as m; print(m.__file__)")
```
- Change `startup_timeout: 15` to `120`
