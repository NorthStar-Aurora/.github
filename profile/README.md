# 🌌 Neon Loom

**Weaving live intelligence into autonomous AI operations** — a complete platform for building and operating intelligent AI systems.

> 🚀 **Quick Start:** `bash <(curl -fsSL https://raw.githubusercontent.com/Neon-Loom/Neon-Loom/main/scripts/install.sh)`  
> 📖 **[Full Installation Guide](https://github.com/Neon-Loom/.github/blob/main/INSTALLATION.md)** | Specialized for **Debian/Ubuntu** systems

## What is Neon Loom?

Neon Loom transforms your documentation and conversations into continuously-improving AI models. It's your personal AI training and deployment platform that ingests knowledge, distills datasets, trains custom models, and serves them through beautiful web interfaces—all with automated nightly cycles.

**Core Platform:** [Neon-Loom/Neon-Loom](https://github.com/Neon-Loom/Neon-Loom) — Distillation, training, browser agent, and orchestration

## 🏗️ Ecosystem Components

<table><tr><td>

### 🚀 Inference and Orchestration

- 🔹 [Neon-Loom/inference-stack-ops](https://github.com/Neon-Loom/inference-stack-ops)
- 🔹 [Neon-Loom/superagi-gpu-ops](https://github.com/Neon-Loom/superagi-gpu-ops)

</td><td>

### 💬 Chat Interfaces

- 💬 [Neon-Loom/neon-openwebui-ops](https://github.com/Neon-Loom/neon-openwebui-ops)
- 💬 [Neon-Loom/librechat-ops](https://github.com/Neon-Loom/librechat-ops)

</td></tr></table>

### 🧪 Labs & Experimental

- 🧪 [Neon-Loom/urban-octo-giggle](https://github.com/Neon-Loom/urban-octo-giggle)
- 🧼 [Neon-Loom/sanitized_agi_ollama](https://github.com/Neon-Loom/sanitized_agi_ollama)

## 🎯 Getting Started

### System Requirements

- **OS:** Ubuntu 22.04+ or Debian 12+ *(installation specialized for Debian-based systems)*
- **RAM:** 8GB minimum (16GB+ recommended)
- **Storage:** 50GB+ free space
- **GPU:** NVIDIA GPU recommended (optional)

### Installation

**Automated Installer (Recommended):**

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/Neon-Loom/Neon-Loom/main/scripts/install.sh)
```

The installer will interactively ask about:
- Installation directory (default: `~/neon-loom`)
- SSL/TLS setup (Caddy vs Certbot)
- Firewall configuration (UFW vs IPTables)
- Component selection and network options

**Manual Installation:**

For advanced users who prefer complete control, see the [Installation Guide](https://github.com/Neon-Loom/.github/blob/main/INSTALLATION.md).

### Default Installation Structure

Neon Loom installs to `~/neon-loom/` by default, containing:
```
~/neon-loom/
├── config.env          # Main configuration
├── sources/            # Documentation to ingest
├── data/               # Training datasets
├── output/             # Model outputs
├── logs/               # System logs
└── neon-loom/          # Core platform repository
```

This location is customizable during installation.

## 📚 Documentation

- 📖 **[Installation Guide](https://github.com/Neon-Loom/.github/blob/main/INSTALLATION.md)** — Complete installation reference
- 📖 **[Setup Guide](https://github.com/Neon-Loom/Neon-Loom/blob/main/docs/SETUP_GUIDE.md)** — Manual configuration
- 📖 **[Networking Setup](https://github.com/Neon-Loom/Neon-Loom/blob/main/docs/NETWORKING_SETUP.md)** — Firewalls, reverse proxies, SSL
- 📖 **[Platform Layout](https://github.com/Neon-Loom/Neon-Loom/blob/main/docs/PLATFORM_LAYOUT.md)** — Architecture overview

## 💡 Key Features

- 🔄 **Fully Automated** — Nightly training cycles
- 🚀 **GPU Accelerated** — NVIDIA GPU support
- 🌐 **Web Browsing AI** — Live data from the web
- 💾 **Continuous Learning** — Learns from every conversation
- 📊 **Monitoring Built-in** — Health dashboards
- 🔒 **Security First** — No secrets in code
- 🐳 **Docker Ready** — Containerized services

## 🤝 Contributing

We welcome contributions! Each repository has its own contribution guidelines. Generally:

- Keep secrets out of Git
- Update documentation with code changes
- Run tests before submitting PRs
- Follow existing code style

## 📄 License

Neon Loom projects are released under the MIT License. See individual repositories for details.

---

> **Note:** Each repository contains specific deployment notes, GPU requirements, and operational runbooks. Check individual READMEs for component-specific details.
