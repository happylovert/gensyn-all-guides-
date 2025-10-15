# 🚀 Gensyn All Guides

Welcome to the complete **Gensyn guides repository**.  
This repo contains step-by-step guides for running **RL-Swarm Node**, setting up **Swarm Role**, obtaining **Block Role**, and fixing common **Errors**.

---

## 📚 Guides

### 1️⃣ [Gensyn RL-Swarm Guide](gensyn-rl-swarm-guide.md)
Step-by-step guide to set up and run the **RL-Swarm Node** on Linux, Mac, VPS, or GPU. Includes:
- System requirements
- GPU rental instructions
- Node installation
- Running the node
- Backups and status checking
- Troubleshooting

---

### 2️⃣ [Gensyn Swarm Role Guide](gensyn-swarm-role-guide.md)
Guide to configure your **Swarm Role** and connect with **Telegram Bot**:
- Installing Go
- Setting up Telegram Bot
- Configuring GSwarm
- Linking Discord & Telegram
- Upgrade to new releases

---

### 3️⃣ [Gensyn Block Role Guide](gensyn-block-role-guide.md)
Step-by-step guide to get the **BLOCK Role** using:
- OctaSpace Marketplace
- Hugging Face Token
- GensynAI BlockAssist
- Minecraft verification
- Discord verification

---

### 4️⃣ [Gensyn Error Solutions](gensyn-error-solutions.md)
Solve common errors while running RL-Swarm Node:
- Node termination errors
- Virtual environment issues
- Updating node & configs
- Full command sequence to fix issues

```bash
cd rl-swarm
rm -rf .venv && git pull && python3 -m venv .venv && source .venv/bin/activate
git switch main
git reset --hard
git clean -fd
git pull origin main
sed -i -E 's/(num_train_samples:\s*)2/\1 1/' rgym_exp/config/rg-swarm.yaml
./run_rl_swarm.sh
