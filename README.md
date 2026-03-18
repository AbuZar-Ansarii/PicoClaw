# 🦞 Run PicoClaw on phone 🦞

PicoClaw is an ultra-lightweight, open-source AI agent framework designed to run on resource-constrained hardware (like $10 RISC-V boards or old Android phones). It is a Go-native, "bare-metal" alternative to heavier frameworks like OpenClaw.

# Run these commands inside tetmux.

## update packages and intall ubuntu
If you haven't installed Ubuntu yet, use proot-distro:
```
pkg update && pkg upgrade -y
pkg install proot-distro -y
proot-distro install ubuntu
proot-distro login ubuntu
```
## 2. Prepare the Ubuntu Environment
Once you are inside the Ubuntu shell (it will say root@localhost), install the basic tools:
```
apt update && apt upgrade -y
apt install wget tar nano ca-certificates -y
```
## 3. Download and Setup PicoClaw
Now, download the ARM64 version of PicoClaw:
```
wget https://github.com/sipeed/picoclaw/releases/download/v0.2.2/picoclaw_Linux_arm64.tar.gz

tar -xzvf picoclaw_Linux_arm64.tar.gz

chmod +x picoclaw
mv picoclaw /usr/local/bin/
```
## 4. Create your Config File
Ubuntu uses the /root/ directory as home. Create the config folder and file:
```
mkdir -p ~/.picoclaw
```
## 5. Paste this config and Replace YOUR_TELEGRAM_TOKEN_HERE and ID  with your Bot token and ID (you can use your preffered ollama model):
```
cat <<EOF > ~/.picoclaw/config.json
{
  "agents": {
    "defaults": {
      "workspace": "/root/.picoclaw/workspace",
      "model": "my-local-model"
    }
  },
  "model_list": [
    {
      "model_name": "my-local-model",
      "model": "ollama/kimi-k2.5:cloud", 
      "api_base": "http://127.0.0.1:11434/v1",
      "api_key": "ollama"
    }
  ],
  "channels": {
    "telegram": {
      "enabled": true,
      "token": "YOUR_TELEGRAM_TOKEN_HERE",
      "allow_from": [TELEGRAM_ID_HERE]
    }
  }
}
EOF
```
## 6. Run PicoClaw

```
picoclaw gateway
```

