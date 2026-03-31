Perfect — basic knowledge is enough, this setup is straightforward. Here's everything you need step by step.

---

**Instance recommendation**

For a paper trading bot with logging, `t3.small` is the sweet spot:
- 2 vCPU, 2GB RAM — enough for your async bot + FastAPI + signal logging
- ~£12-15/month in eu-west-2 (London) — keep latency to Kraken low
- Upgrade to `t3.medium` when you go live with real money

---

**Step 1 — Launch the instance**

In AWS Console:
1. EC2 → Launch Instance
2. **AMI:** Ubuntu Server 24.04 LTS
3. **Instance type:** `t3.small`
4. **Region:** `eu-west-2` (London)
5. **Key pair:** create a new one, download the `.pem` file, keep it safe
6. **Security group rules:**
```
SSH        TCP  22    Your IP only (not 0.0.0.0)
FastAPI    TCP  8000  Your IP only
```
7. **Storage:** 20GB gp3 (default is fine)
8. Launch

---

**Step 2 — Connect and set up the server**

```bash
# on your local machine
chmod 400 your-key.pem
ssh -i your-key.pem ubuntu@YOUR_EC2_PUBLIC_IP

# on the server — update and install Python
sudo apt update && sudo apt upgrade -y
sudo apt install python3.11 python3.11-venv python3-pip git -y
```

---

**Step 3 — Clone your repo and install dependencies**

```bash
git clone https://github.com/YOUR_USERNAME/trading-bot.git
cd trading-bot
python3.11 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

---

**Step 4 — Set up your .env**

```bash
cp .env.example .env
nano .env  # fill in your Kraken API keys
```

---

**Step 5 — Run with systemd so it restarts automatically**

This is the important one — you want the bot to survive crashes and reboots without you manually restarting it.

Create a service file:

```bash
sudo nano /etc/systemd/system/tradingbot.service
```

Paste this:

```ini
[Unit]
Description=Trading Bot
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/trading-bot
EnvironmentFile=/home/ubuntu/trading-bot/.env
ExecStart=/home/ubuntu/trading-bot/venv/bin/python main.py
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

Enable and start it:

```bash
sudo systemctl daemon-reload
sudo systemctl enable tradingbot
sudo systemctl start tradingbot
sudo systemctl status tradingbot
```

Do the same for the FastAPI server:

```bash
sudo nano /etc/systemd/system/tradingbot-api.service
```

```ini
[Unit]
Description=Trading Bot API
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/trading-bot
EnvironmentFile=/home/ubuntu/trading-bot/.env
ExecStart=/home/ubuntu/trading-bot/venv/bin/uvicorn api.main:app --host 0.0.0.0 --port 8000
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable tradingbot-api
sudo systemctl start tradingbot-api
```

---

**Step 6 — Useful commands day to day**

```bash
# check bot is running
sudo systemctl status tradingbot

# view live logs
sudo journalctl -u tradingbot -f

# restart after a code update
git pull
sudo systemctl restart tradingbot

# check API is up
curl http://localhost:8000/status
```

---

**Step 7 — Update CLAUDE.md**

Worth adding the deployment setup so Claude Code knows where the bot lives. Want me to update the CLAUDE.md with the AWS deployment section?
