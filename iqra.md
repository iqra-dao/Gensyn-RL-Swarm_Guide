# 💻 Gensyn Node Setup Guide (Mac / Linux)
**Created by [@WebTigerX](https://x.com/WebTigerX)**  

This is a simple, clear, and complete guide to set up and run your Gensyn RL Swarm Node.  
Follow the steps below carefully, and you’ll have your node running smoothly 🚀  

---

## ⚙️ 1. System Requirements

- Ubuntu 22.04 / 24.04 or macOS  
- Minimum 2GB RAM, 10GB storage  
- Stable Internet connection  
- VPS Recommended  

---

## 🧰 2. Install Python and Basic Tools

### Linux
```bash
sudo apt update && sudo apt install -y python3 python3-pip python3-venv curl wget screen git lsof
```

### macOS
```bash
brew install python
```

Check version:
```bash
python3 --version
```

---

## 🧱 3. Install Node.js, npm, and Yarn

### Linux
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

### macOS
```bash
brew install node
npm install -g yarn
```

Check versions:
```bash
node -v
npm -v
yarn -v
```

---

## 🚀 4. Start the Node

Create screen (for VPS):
```bash
screen -S gensyn
```

Clone the repository:
```bash
git clone https://github.com/gensyn-ai/rl-swarm.git
cd rl-swarm
```

Create virtual environment:
```bash
python3 -m venv .venv
source .venv/bin/activate
```

Run the node:
```bash
./run_rl_swarm.sh
```

> Follow on-screen instructions. Use the default model by pressing Enter when asked.  
> Choose “Y” when asked to join the AI Prediction Market.

Detach from screen: `Ctrl + A + D`  
Reattach later:
```bash
screen -r gensyn
```

---

## 🔍 5. How to Login (Access Port 3000)

Open a new terminal and run:
```bash
sudo apt install ufw -y
sudo ufw allow 22
sudo ufw allow 3000/tcp
sudo ufw enable
```

Install Cloudflared:
```bash
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
sudo dpkg -i cloudflared-linux-amd64.deb
cloudflared tunnel --url http://localhost:3000
```

Now open the generated link in your browser to log in.  

---

## 🐞 6. Common Fixes

### Terminated Node
```bash
deactivate
rm -rf .venv
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

If the node still fails, wait 1–2 minutes or restart the VPS.  

---

## 📲 7. Telegram Notification Setup

### Step 1: Create a Bot
Open [@BotFather](https://t.me/BotFather) on Telegram.  
Send `/newbot`, set a name, and copy your **Bot Token**.

### Step 2: Get Chat ID
Go to:
```
https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates
```
Replace `YOUR_BOT_TOKEN` and send a message to your bot first.  
Your Chat ID will appear in the result.

### Step 3: Install GSwarm Tool
```bash
go install github.com/Deep-Commit/gswarm/cmd/gswarm@latest
```

Run setup:
```bash
gswarm
```
Enter your Bot Token, Chat ID, and your Gensyn EOA address.  

✅ Telegram setup complete — you’ll now get node alerts instantly.

---

## 💬 8. Discord Verification

1. Go to **Gensyn Discord** → `#swarm-link` channel  
2. Type `/link-telegram` to get your code  
3. Go to your bot chat → send `/verify CODE`  
🎯 You’ll get your verified role automatically.

---

## 🔁 9. Update Node to Latest Version

```bash
cd rl-swarm
git switch main
git reset --hard
git clean -fd
git pull origin main
./run_rl_swarm.sh
```

If you get errors, re-run using the Terminated Node Fix above.

---

## ⚠️ 10. Fix: Connection Refused Error `[Errno 111]`

This usually happens after an update.  
Fix it by running:

```bash
cd rl-swarm
git stash && git pull
sudo rm rgym_exp/src/manager.py
nano rgym_exp/src/manager.py
```

Paste the updated manager.py file code from Gensyn Discord (shared by **xailong_6969**).  
Save it: `Ctrl + O`, Enter, `Ctrl + X`.

Then restart:
```bash
deactivate
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

✅ Node will reconnect and run fine again.

---

## 🎯 11. Extra Tips

- Keep VPS running 24/7 for stable uptime  
- Save your `swarm.pem` file safely  
- Avoid using manual model names  
- Always check Gensyn Discord for updates  

---

### 🧠 Made with patience by [@WebTigerX](https://x.com/WebTigerX)
Helping new builders run and maintain Gensyn nodes easily ⚡
