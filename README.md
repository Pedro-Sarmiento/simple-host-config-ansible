# Ansible playbook — ML & DB host provisioning

![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white)
![Debian](https://img.shields.io/badge/Debian-A81D33?style=flat-square&logo=debian&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)

Multi-group Ansible playbook that provisions two server roles: **DB hosts** (Nginx + dedicated user) and **ML hosts** (Python virtual environment with data science dependencies). Demonstrates idempotent provisioning across heterogeneous environments from a single inventory.

---

## Why this matters

This setup mirrors a typical real-world scenario where a small AI team needs to provision separate hosts for distinct roles — a database server and a model-serving environment — with different dependency profiles, idempotently and from a single inventory. It's a minimal but realistic example of the kind of infrastructure work that keeps ML systems running in production.

---

## Project structure

```
host-config-ansible/
├── playbook.yml        # Main playbook
├── inventory.yml       # Host inventory
└── README.md
```

---

## Groups and tasks

**DB:**
- Installs Nginx
- Creates the `nginx` user
- Writes a `/etc/provisioned` file with the provisioning date

**ML:**
- Installs Python, pip, and venv
- Creates a virtual environment at `/opt/venv`
- Installs Pandas inside the virtual environment
- Writes a `/etc/provisioned` file with the provisioning date

---

## Requirements

- Debian 12/13
- Ansible 2.9+
- Sudo access on the target host

---

## Usage

### 1. Clone the repository

```bash
git clone git@github.com:Pedro-Sarmiento/host-config-ansible.git
cd host-config-ansible
```

### 2. Run the playbook

```bash
ansible-playbook -i inventory.yml playbook.yml --ask-become-pass
```

### 3. Verify provisioning

```bash
cat /etc/provisioned
```

---

## Idempotency

The playbook can be executed multiple times without side effects or errors. Subsequent runs will only apply changes if the target state diverges from the desired state.

---

## License

MIT
