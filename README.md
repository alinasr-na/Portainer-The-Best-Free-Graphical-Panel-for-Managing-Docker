# Portainer — The Best Free Graphical Panel for Managing Docker  
**Like cPanel for Docker!** Installs in just **2 minutes** 🚀

---

## 📦 Project: Install Portainer on VPS

This guide helps you install **Portainer CE** (free version) on a Linux server (like Ubuntu/Debian) with Docker and manage containers, networks, volumes, and more via a web-based GUI.

---

## 🧰 Requirements

- 🐧 Linux Server (Ubuntu/Debian)
- 🐳 **Docker** installed
- 🌐 Browser access and server IP

> If Docker isn't installed, run these first:
```bash
sudo apt update && sudo apt install docker.io -y
sudo systemctl enable --now docker
```

---

## 🚀 Installation Steps (2 Minutes!)

### Step 1: Create a Volume for Portainer Data
```bash
docker volume create portainer_data
```

### Step 2: Run Portainer
```bash
docker run -d -p 9000:9000 -p 8000:8000 \
  --name portainer \
  --restart always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:latest
```

> Port `8000` is for **Edge Agent** (optional — for future use)

---

### Step 3: Open Port in Firewall
```bash
sudo ufw allow 9000
```

> If using `firewalld` or `iptables`, open port 9000.

---

### Step 4: Access the Web Panel
Open in your browser:

```
http://YOUR_VPS_IP:9000
```

> Replace `YOUR_VPS_IP` with your server IP  
> Example: `http://45.32.123.45:9000`

---

## 🎯 First Login

1. **Set admin password** (at least 8 characters)
2. Choose username (e.g., `admin`)
3. Select **"Connect to local Docker environment"**
4. You're in! 🎉

---

## 🌟 Key Features of Portainer

| Feature | Description |
|--------|-------------|
| 🐳 Container Management | Start, stop, remove, logs, terminal |
| 📦 Image Management | Pull, push, delete |
| 🌐 Networks | Bridge, Overlay, Macvlan |
| 💾 Volumes | Data management |
| ⚙️ Stacks (Compose) | Upload `docker-compose.yml` and deploy |
| 🔐 Users & Access | Roles and teams |
| 🔄 One-Click Updates | Upgrade with ease |

---

## 🛠️ Useful Commands

```bash
# Check Portainer status
docker ps | grep portainer

# View logs
docker logs -f portainer

# Update Portainer to latest version
docker stop portainer
docker rm portainer
docker pull portainer/portainer-ce:latest
# Re-run Step 2 command
```

---

## 🔒 Security (Recommended)

1. **HTTPS with Let's Encrypt** (via Nginx reverse proxy)
2. **Change port 9000** to a non-standard one
3. **Strong authentication** + complex password
4. **Restrict access by IP** in firewall

---

## 🚀 What's Next?

- Upload your `docker-compose.yml` projects
- Add multiple environments (Local + Remote)
- Use **Templates** for quick installs (WordPress, Node.js, etc.)

---

## 📂 Suggested Project Structure (for GitHub)

```
portainer-setup/
├── docker-compose.yml        # Optional: for Stack management
├── README.md                 # This file
└── .env                      # (Optional) Environment variables
```

> You can use this `docker-compose.yml` to manage Portainer with Compose:

```yaml
version: '3.8'
services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: always
    ports:
      - "9000:9000"
      - "8000:8000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - portainer_data:/data

volumes:
  portainer_data:
```

Then:
```bash
docker-compose up -d
```

---

**All set!**  
Now manage your Docker environment like a pro — **with your mouse** 🖱️✨

---

*Made with ❤️ for developers and sysadmins*  
*If this helped, please ⭐ star the repo!*
