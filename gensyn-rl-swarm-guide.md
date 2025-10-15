# 💻 Gensyn RL-Swarm Guide

This iteration of RL-Swarm is powered by the [GenRL](https://github.com/gensyn-ai/genrl) library.  
It is a fully composable framework for decentralized reinforcement learning which enables users to create and customize their own swarms with multi-agent multi-stage environments.

---

## 🔹 Supported Models

- Gensyn/Qwen2.5-0.5B-Instruct  
- Qwen/Qwen3-0.6B  
- nvidia/AceInstruct-1.5B  
- dnotitia/Smoothie-Qwen3-1.7B  
- Gensyn/Qwen2.5-1.5B-Instruct  

---

## ⚙️ Requirements

Your hardware requirements vary depending on model size and platform:

**CPU-only support**:  
- arm64 or x86 CPU  
- Minimum 32GB RAM (more if running other apps)  

**GPU (CUDA) support**:  
- RTX 3090 / 4090 / 5090  
- A100 / H100  

**Python**: >=3.10  

> Mac users may need to upgrade Python to >=3.10  

---

## 🛠️ Instructions

### 1️⃣ Clone Repo

```bash
git clone https://github.com/gensyn-ai/rl-swarm
cd rl-swarm
```

### 2️⃣ Experimental Mode (Recommended for Custom Models)

```bash
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

- Follow prompts: login, Hugging Face token, Prediction Market participation (`Y/N`).  
- Use default models for safety unless you are comfortable with custom selection.

---

### 3️⃣ Docker Mode (Optional)

#### CPU-only:
```bash
docker-compose run --rm --build -Pit swarm-cpu
```

#### GPU:
```bash
docker-compose run --rm --build -Pit swarm-gpu
```

> If `docker-compose` fails, try `docker compose` instead.

---

### 4️⃣ Login

- Open browser or VM port 3000 → http://localhost:3000/  
- Click login → choose preferred method  

---

### 5️⃣ Hugging Face Token

- Generate a token [here](https://huggingface.co/) → Access Tokens → Write  
- Paste token when prompted

---

### 6️⃣ AI Prediction Market

- Press `Y` to participate (default) or `N` to opt out  
- Models place bets on reasoning problems, rewards depend on speed & accuracy  

---

### 7️⃣ Initial Peering & Training

- Peers register and vote on-chain: [Gensyn Testnet Logs](https://gensyn-testnet.explorer.alchemy.com/)  
- Track progress: [Dashboard](https://dashboard.gensyn.ai/)  

---

## 🔑 Identity Management

- EOA keys managed via Alchemy modal login  
- Creates `swarm.pem` for your peer identity  
- Link multiple nodes to same EOA → generate new peer ID per node  
- Lost `swarm.pem` → start fresh with same email  
- Keep `swarm.pem` → reuse single node safely  

---

## 🐞 Troubleshooting & Error Fixes

### Logs Location

- `logs/yarn.log` → modal login server  
- `logs/swarm.log` → RL-Swarm app  
- `wandb/debug.log` → training runs  

### Common Issues

- **Peer skipped a round** → device too slow, skip happens automatically  
- **Model not training / slow** → wait 20 mins (Mac/CPU)  
- **Login issues** → logout first, remove `swarm.pem` if necessary  
- **OOM / Memory Issues** → Mac fix:
```bash
export PYTORCH_MPS_HIGH_WATERMARK_RATIO=0.0
```
- **Windows** → Use WSL/Linux for proper RL-Swarm support  

### Package Fixes

- `viem` upgrade for login errors:
```bash
cd /root/rl-swarm/modal-login/
yarn upgrade
yarn add next@latest
yarn add viem@latest
```

- Docker / VPS: ensure proper port forwarding (`-L 3000:localhost:3000`)  

### Multiple GPUs / Nodes

- Isolate each GPU, install repo per GPU, assign different ports  

---

## ⚡ Gensyn Error Solution

```bash
cd rl-swarm
rm -rf .venv && git pull && python3 -m venv .venv && source .venv/bin/activate
git switch main
git reset --hard
git clean -fd
git pull origin main
sed -i -E 's/(num_train_samples:\s*)2/\1 1/' rgym_exp/config/rg-swarm.yaml
./run_rl_swarm.sh
```

---

### ✅ Done

- Your RL-Swarm node is now running  
- Check logs → monitor training & AI Prediction Market participation  
- Enjoy contributing to Gensyn RL-Swarm! 🚀
