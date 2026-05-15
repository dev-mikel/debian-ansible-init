![Status](https://img.shields.io/badge/status-active-blue)
![Automation](https://img.shields.io/badge/type-Ansible%20Automation-green)
![Domain](https://img.shields.io/badge/domain-Debian%20%2F%20VPS-orange)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

# **ansible-development — DevOps / Infrastructure Automation**

### *Ansible baseline for Debian-based server provisioning and hardening*

**Status:** Active infrastructure automation project.
**Audience:** DevOps engineers, infrastructure admins, platform engineers, and operators.

---

# **Table of Contents**
- [1. Overview](#1-overview)
- [2. Scope](#2-scope)
- [3. Included Automation](#3-included-automation)
- [4. Tested Environment](#4-tested-environment)
- [5. Repository Layout](#5-repository-layout)
- [6. Main Roles](#6-main-roles)
- [7. Example Use Cases](#7-example-use-cases)
- [8. Estimated Time Savings](#8-estimated-time-savings)
- [9. Before Using This Repository](#9-before-using-this-repository)
- [10. About](#10-about)

---

# **1. Overview**

This repository provides a practical Ansible baseline for provisioning Debian-based systems in a reproducible way.

The main focus is DevOps and infrastructure work: initial host setup for fresh VPS instances, cloud servers, workstations, and lab environments. It reduces manual effort during bootstrap, improves consistency across hosts, and keeps security and tooling setup repeatable.

The automation covers infrastructure preparation, service installation, access control, hardening, and shell customization. It is especially useful when you need to standardize the first hours of work on a new host across multiple systems.

### **Typical outcomes**
- consistent server bootstrap
- repeatable hardening steps
- reduced configuration drift
- faster provisioning across multiple hosts
- easier rebuilds and redeployments

---

# **2. Scope**

### Deliverables included
- Ansible playbooks and roles
- Inventory structure for development use
- Shared group and host variables
- Templates and handlers
- Validation tasks
- Reusable automation for Debian-based environments

### Not included
- Application source code
- Production infrastructure management
- CI/CD pipelines
- Cloud provider orchestration
- Managed secrets storage outside the repository

---

# **3. Included Automation**

This repository covers or prepares automation for:

- SSH server configuration and hardening
- UFW firewall rules
- Fail2ban
- Docker installation and baseline setup
- Node.js installation
- npm and pnpm selection
- Node Exporter
- New Relic infrastructure agent
- Coolify deployment support
- Git and GitHub SSH configuration
- Zsh installation 
- Oh My Posh prompt configuration
- Custom dark prompt theme designed by the author
- Tailscale-based access and network rules

---

# **4. Tested Environment**

The repository was developed and validated in a local lab environment based on:

- Linux Mint 22.3
- KVM
- QEMU
- libvirt
- virt-install
- cloud-init
- qcow2 backing images
- UEFI / OVMF
- libvirt NAT networking

That environment was used to simulate realistic Debian-style provisioning flows before targeting cloud-style server bootstrap use cases.

The repository was also exercised with Tailscale and the New Relic infrastructure agent to validate service installation and configuration paths.

---

# **5. Repository Layout**

- `ansible.cfg` — Ansible configuration
- `inventories/development/` — development inventory and host/group variables
- `group_vars/` — shared variables
- `playbooks/` — orchestration entry points
- `roles/` — reusable role logic
- `templates/` — Jinja2 templates
- `handlers/` — role handlers
- validation tasks — files prefixed with `val_` for checks separate from operational tasks

---

# **6. Main Roles**

- `roles/Debiancustom` — Debian customization default role set
- `roles/Debiancustom2` — secondary customization role

The duplicated-looking Debian roles are preserved intentionally. They may diverge by target, ordering, defaults, or operational scope, so they should not be merged without a deliberate review.

---

# **7. Example Use Cases**

### **1. Fresh cloud VPS bootstrap**
Provision a clean Debian-based VPS with:

- secure SSH access
- firewall rules
- fail2ban protection
- monitoring agent installation
- shell and Git configuration
- runtime tooling for application deployment

### **2. Server hardening baseline**
Use the repository to establish a hardened default for:

- SSH access control
- trusted source restrictions
- port exposure reduction
- login protection
- access policy standardization

### **3. Developer or operator workstation**
Use the same automation to build a repeatable Linux workstation with:

- custom Zsh installation and configuration
- GitHub SSH setup
- Node.js tooling
- Docker runtime
- prompt and shell enhancements
- an author-designed dark Oh My Posh theme with utility-focused prompt features

### **4. Self-hosted service node**
Use the automation to prepare a host for services such as Coolify and related supporting tools while keeping the environment consistent and maintainable.

---

# **8. Estimated Time Savings**

The complete automation workflow typically executes in approximately 5–10 minutes depending on:

- VPS provider performance
- network speed
- package mirror responsiveness
- Docker and external repository download times
- host resources

A fully manual setup commonly takes several hours when it includes:

- package installation
- repository and GPG configuration
- SSH hardening
- firewall setup
- monitoring agent installation
- Docker setup
- runtime tooling installation
- shell customization
- validation and troubleshooting

### **Project value**

For multiple VPS instances or repeated rollouts, the value grows because the same declarative automation can be reused without rebuilding the configuration by hand.

The operational value is not only execution speed, but also:

- reproducibility
- reduction of configuration drift
- repeatable server bootstrap
- consistent hardening
- minimized operator error
- standardized provisioning workflows
- easier rebuild and redeployment processes

---

# **9. Before Using This Repository**

Review and customize the environment-specific values before running the playbooks against production or internet-facing systems.

### Recommended preparation steps
- Replace placeholder values such as `CHANGE_ME`
- Review inventory variables and host definitions
- Configure your own SSH keys and secrets
- Validate firewall and SSH exposure rules
- Adjust Tailscale, monitoring, and telemetry settings as needed
- Review package selections and enabled services
- Verify Docker-related configurations for your environment
- Test the playbooks against a non-production host first
- Validate all changes with `ansible-playbook --syntax-check`
- Keep sensitive values outside version control whenever possible

For public or cloud VPS deployments, also verify:

- provider networking assumptions
- SSH accessibility
- sudo availability
- DNS and domain configuration
- port exposure policies
- backup and recovery strategy

This repository is intended as a reusable automation baseline and should be adapted to the operational and security requirements of each environment.

It works best as infrastructure scaffolding for repeatable provisioning rather than a one-off setup script.

### Vault usage history
This repository previously included `inventories/development/group_vars/all/vault.yml` for GitHub SSH key material.

It kept private key material out of the plain YAML defaults while still supporting automated GitHub SSH setup during testing and provisioning.

Typical vault commands were:

```bash
ansible-vault view inventories/development/group_vars/all/vault.yml --ask-vault-pass
ansible-vault decrypt inventories/development/group_vars/all/vault.yml --ask-vault-pass
ansible-vault edit inventories/development/group_vars/all/vault.yml --ask-vault-pass
```

If the file is removed from the public repository, keep the secret material outside version control and recreate it locally when needed.

---

# **10. About**

**Author:** Miguel Ladines  
**Role:** Electronics Engineer / Embedded Systems & Full Stack Developer
**License:** MIT