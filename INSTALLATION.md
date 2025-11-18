# 🚀 Neon Loom Installation Guide

> **Platform Support:** These installation instructions are specialized for **Debian** and **Ubuntu** systems.

## Overview

Neon Loom is a comprehensive AI operations platform that transforms your documentation and conversations into continuously-improving AI models. This guide covers installation across the Neon Loom ecosystem.

## System Requirements

### Supported Operating Systems
- **Ubuntu** 22.04 LTS or later
- **Debian** 12 (Bookworm) or later

> ⚠️ **Important:** These installation scripts and procedures are specifically designed and tested for Debian-based distributions. Other Linux distributions may require manual adaptation.

### Hardware Requirements
- **CPU:** Modern multi-core processor (4+ cores recommended)
- **RAM:** 8GB minimum, 16GB+ recommended
- **Storage:** 50GB+ free disk space (more for large model training)
- **GPU:** NVIDIA GPU recommended for training and inference (optional but highly beneficial)

### Network Requirements
- Internet access for package downloads and model fetching
- (Optional) SSL/TLS certificates for production deployments
- (Optional) Reverse proxy for internet-facing deployments

## Installation Locations

Neon Loom installs to `~/neon-loom` by default, which serves as the base directory for:
- Configuration files (`config.env`)
- Documentation sources
- Training datasets
- Model outputs
- Logs and monitoring data

This location can be customized during installation if needed.

## Quick Start: Automated Installation

The easiest way to install Neon Loom is using the automated installer. It will interactively guide you through setup, asking about your preferences for various components.

### What the Installer Does

The automated installer will:

1. **Detect your environment**
   - Checks OS version (Debian/Ubuntu)
   - Detects available GPU hardware
   - Verifies system requirements

2. **Ask configuration questions**
   - Installation directory (default: `~/neon-loom`)
   - SSL/TLS setup: **Caddy** (automatic HTTPS) vs **Certbot** (Let's Encrypt with manual setup)
   - Firewall choice: **IPTables** (traditional) vs **UFW** (user-friendly)
   - Network configuration options
   - Service enablement preferences

3. **Install prerequisites**
   - System packages (curl, git, python3, etc.)
   - Docker Engine and Docker Compose
   - NVIDIA drivers (if GPU detected)
   - Ollama runtime for AI model serving
   - Selected reverse proxy (Caddy or Nginx)
   - Selected firewall tools (iptables or UFW)

4. **Deploy core services**
   - OpenWebUI (web interface for AI chat)
   - Browser agent (web browsing capabilities)
   - Distillation worker (dataset generation)
   - Monitoring services (optional)

5. **Create configuration**
   - Generate `~/neon-loom/config.env`
   - Create systemd service files
   - Set up log directories

### Running the Installer

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/Neon-Loom/Neon-Loom/main/scripts/install.sh)
```

The installer is interactive and will prompt you for choices at each step:

```
🌟 Neon Loom Installer
Detected: Ubuntu 22.04 LTS

📍 Installation directory [~/neon-loom]: 
🔐 SSL/TLS setup - Choose your option:
    1) Caddy (automatic HTTPS)
    2) Certbot (Let's Encrypt, manual setup)
    Selection [1]: 

🔥 Firewall setup - Choose your option:
    1) UFW (user-friendly)
    2) IPTables (traditional)
    Selection [1]:

... (additional prompts)
```

### Installation Options Explained

#### SSL/TLS Options

**Option 1: Caddy (Recommended for most users)**
- ✅ Automatic HTTPS certificate management
- ✅ Auto-renewal of certificates
- ✅ Simple configuration
- ✅ Built-in reverse proxy
- ❌ Less flexible for complex setups

**Option 2: Certbot with Nginx/Apache**
- ✅ More control over web server configuration
- ✅ Works with existing web servers
- ✅ Industry standard
- ❌ Manual certificate management
- ❌ Requires more configuration

#### Firewall Options

**Option 1: UFW (Recommended for most users)**
- ✅ User-friendly command-line interface
- ✅ Simple rule syntax
- ✅ Good defaults for common scenarios
- ❌ Less granular control

**Option 2: IPTables**
- ✅ Maximum control and flexibility
- ✅ Standard Linux firewall
- ✅ Better for complex network setups
- ❌ Steeper learning curve
- ❌ More complex rule syntax

### Post-Installation Steps

After installation completes:

```bash
# 1. Verify services are running
systemctl --user status neon-loom-distill.service
systemctl --user status neon-loom-browser.service

# 2. Check OpenWebUI is accessible
curl -I http://localhost:3000

# 3. View logs
journalctl --user -u neon-loom-distill.service -f
```

## Manual Installation

For advanced users who prefer manual control, see the detailed setup guide:

📖 **[Manual Setup Guide](https://github.com/Neon-Loom/Neon-Loom/blob/main/docs/SETUP_GUIDE.md)**

Manual installation gives you complete control over:
- Custom installation paths
- Specific package versions
- Service configuration
- Network topology

## Component-Specific Installation

### Core Platform (Neon-Loom)

The main Neon Loom platform provides distillation, training, and orchestration:

**Repository:** [Neon-Loom/Neon-Loom](https://github.com/Neon-Loom/Neon-Loom)

```bash
# Clone the repository
git clone https://github.com/Neon-Loom/Neon-Loom.git ~/neon-loom

# Run the installer
cd ~/neon-loom
bash scripts/install.sh
```

**Key Components:**
- Documentation distillation services
- Automated training pipelines
- Browser agent for web-based AI queries
- OpenWebUI integration
- Monitoring and health dashboards

### Inference Stack Operations

GPU-accelerated inference and model serving:

**Repository:** [Neon-Loom/inference-stack-ops](https://github.com/Neon-Loom/inference-stack-ops)

Provides:
- Ollama deployment configurations
- vLLM integration
- Model optimization scripts
- GPU resource management

### SuperAGI GPU Operations

Advanced agent orchestration with GPU acceleration:

**Repository:** [Neon-Loom/superagi-gpu-ops](https://github.com/Neon-Loom/superagi-gpu-ops)

Provides:
- SuperAGI platform deployment
- GPU-accelerated agent workflows
- Long-running task automation

### OpenWebUI Operations

Customized OpenWebUI deployments:

**Repository:** [Neon-Loom/neon-openwebui-ops](https://github.com/Neon-Loom/neon-openwebui-ops)

Provides:
- Themed OpenWebUI configurations
- Custom pipelines and tools
- Integration templates

### LibreChat Operations

Alternative chat interface:

**Repository:** [Neon-Loom/librechat-ops](https://github.com/Neon-Loom/librechat-ops)

Provides:
- LibreChat deployment configs
- Multi-provider integration
- Custom branding

## Network Security Setup

For production deployments, proper network security is essential.

### Firewall Configuration

#### Using UFW (Simple)

```bash
# Install UFW (if not already installed)
sudo apt-get install ufw

# Allow SSH (important - don't lock yourself out!)
sudo ufw allow 22/tcp

# Allow HTTP and HTTPS
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Allow Ollama (if remote access needed)
sudo ufw allow 11434/tcp

# Enable firewall
sudo ufw enable

# Check status
sudo ufw status verbose
```

#### Using IPTables (Advanced)

```bash
# Save current rules
sudo iptables-save > ~/iptables.backup

# Flush existing rules
sudo iptables -F

# Default policies
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT ACCEPT

# Allow loopback
sudo iptables -A INPUT -i lo -j ACCEPT

# Allow established connections
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allow SSH
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow HTTP/HTTPS
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Save rules
sudo iptables-save | sudo tee /etc/iptables/rules.v4
```

### Reverse Proxy Setup

#### Using Caddy (Automatic HTTPS)

```bash
# Install Caddy
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy

# Configure Caddy (example)
sudo tee /etc/caddy/Caddyfile > /dev/null <<EOF
yourdomain.com {
    reverse_proxy localhost:3000
}
EOF

# Restart Caddy
sudo systemctl restart caddy
```

#### Using Nginx with Certbot

```bash
# Install Nginx and Certbot
sudo apt-get update
sudo apt-get install -y nginx certbot python3-certbot-nginx

# Configure Nginx
sudo tee /etc/nginx/sites-available/neon-loom > /dev/null <<EOF
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host \$host;
        proxy_set_header X-Real-IP \$remote_addr;
        proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto \$scheme;
    }
}
EOF

# Enable site
sudo ln -s /etc/nginx/sites-available/neon-loom /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx

# Get SSL certificate
sudo certbot --nginx -d yourdomain.com
```

For complete networking setup details, see:
📖 **[Networking Setup Guide](https://github.com/Neon-Loom/Neon-Loom/blob/main/docs/NETWORKING_SETUP.md)**

## Troubleshooting

### Installation Fails on Non-Debian Systems

**Problem:** Installer exits with "Unsupported OS" error

**Solution:** The Neon Loom installer is specifically designed for Debian and Ubuntu. For other distributions:
1. Review the installer script to understand required components
2. Manually install equivalent packages for your distribution
3. Follow the manual installation guide
4. Consider contributing a PR with support for your distribution

### GPU Not Detected

**Problem:** NVIDIA GPU not available in containers

**Solution:**
```bash
# Install NVIDIA Container Toolkit
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker

# Test GPU access
docker run --rm --gpus all ubuntu nvidia-smi
```

### Services Won't Start

**Problem:** systemd services fail to start

**Solution:**
```bash
# Check service status
systemctl --user status neon-loom-distill.service

# View detailed logs
journalctl --user -u neon-loom-distill.service -n 100

# Verify configuration
cat ~/neon-loom/config.env

# Check for permission issues
ls -la ~/neon-loom
```

### Port Already in Use

**Problem:** Installation fails because port 3000 or 11434 is already in use

**Solution:**
```bash
# Find what's using the port
sudo lsof -i :3000

# Option 1: Stop the conflicting service
sudo systemctl stop <service-name>

# Option 2: Configure Neon Loom to use different ports
# Edit docker-compose.yml or config.env to change port mappings
```

## Getting Help

- 📖 **Documentation:** Check the [Neon-Loom/Neon-Loom](https://github.com/Neon-Loom/Neon-Loom) repository
- 🐛 **Issues:** Report problems via [GitHub Issues](https://github.com/Neon-Loom/Neon-Loom/issues)
- 💬 **Discussions:** Ask questions in [GitHub Discussions](https://github.com/Neon-Loom/Neon-Loom/discussions)
- 📚 **Detailed Guides:** See the `docs/` directory in the main repository

## Next Steps

After successful installation:

1. **Configure your installation** - Edit `~/neon-loom/config.env`
2. **Access OpenWebUI** - Navigate to `http://localhost:3000`
3. **Add documentation sources** - Place docs in `~/neon-loom/sources/`
4. **Review operational guides** - Check the platform documentation
5. **Set up monitoring** - Configure health dashboards and alerts

Happy weaving! 🧵✨
