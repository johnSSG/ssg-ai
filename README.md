# getsimplicity.dev AI + LAMP Server

Self-hosted production stack on Ubuntu 24.04 with NVIDIA RTX 4000 Ada GPU acceleration.

## Architecture

- Traefik v3 → reverse proxy + automatic Let's Encrypt TLS
- Ollama → local LLM inference (full GPU offload)
- Open WebUI → ChatGPT-like interface at https://ai.getsimplicity.dev
- LAMP → PHP 8.1 + Apache + MariaDB at https://getsimplicity.dev
- Samba share → /var/www (edit files directly from Windows/Mac)
- Cockpit → web server management[](https://your-server:9090)

Everything is managed with Ansible roles + a single docker-compose.yml that is force-recreated on every run.

## Domains (A records must point to this server)

- getsimplicity.dev      → LAMP / PHP site
- ai.getsimplicity.dev   → Open WebUI
- api.getsimplicity.dev  → raw OpenAI-compatible API

## Quick Start

git clone https://github.com/yourname/ai-bootstrap.git
cd ai-bootstrap

# Edit domains, email, and passwords
group_vars/all.yml

# One-time collections
ansible-galaxy collection install community.docker community.general --force

# Deploy / update everything
ansible-playbook -K -i inventory/localhost.yml site.yml

## Daily Usage

- PHP files → /var/www/html/
- Custom Apache .conf files → /opt/ai-stack/lamp/sites-available/
- Samba share → \\ai-server\www, \\ai-server\fileserver 

## Direct Access (server only)

- Ollama raw API: http://ai-server:11434
- Cockpit: https://ai-server:9090

## Secrets

Edit group_vars/all.yml before first run.
For production use ansible-vault on group_vars/all.yml.

