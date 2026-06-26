# 🐳 Automating Docker Installation on AWS EC2 Using Ansible

## 📌 Project Overview

This project demonstrates how to automate Docker installation on multiple AWS EC2 Ubuntu instances using **Ansible**.

Instead of manually connecting to each server, Ansible is used to configure all servers from a single control node (WSL Ubuntu on Windows).

---

## 🛠️ Tech Stack

* Ansible
* AWS EC2 (Ubuntu)
* WSL Ubuntu
* SSH
* Docker
* YAML

---

## 📁 Project Structure

```text
ansible-docker-project/
│── inventory.ini
│── ansible.cfg
│── docker-install.yml
└── README.md
```

---

## 🏗️ Architecture

```text
                Windows Laptop
                      │
                 WSL Ubuntu
              (Ansible Control Node)
                      │
                 SSH using PEM Key
                      │
          ┌───────────┴───────────┐
          │                       │
      Ubuntu EC2 VM1         Ubuntu EC2 VM2
          │                       │
          └──── Docker Installed ─┘
```

---

## 🚀 Prerequisites

* AWS Account
* Two Ubuntu EC2 Instances
* Security Group allowing SSH (Port 22)
* PEM Key Pair
* WSL Ubuntu
* Ansible Installed

---

## 📄 Inventory File (`inventory.ini`)

```ini
[docker_servers]
vm1 ansible_host=<EC2_PUBLIC_IP_1> ansible_user=ubuntu
vm2 ansible_host=<EC2_PUBLIC_IP_2> ansible_user=ubuntu
```
<img width="725" height="125" alt="Screenshot 2026-06-27 003446" src="https://github.com/user-attachments/assets/4f44654d-15ac-42f8-a4a8-1b315b89d25a" />

---

## ⚙️ Ansible Configuration (`ansible.cfg`)

```ini
[defaults]
inventory = inventory.ini
host_key_checking = False
private_key_file = ~/devops-key.pem
remote_user = ubuntu
```
<img width="622" height="126" alt="Screenshot 2026-06-27 013145" src="https://github.com/user-attachments/assets/9849a4e5-f355-4287-ac81-74021247de33" />

---

## 📜 Playbook (`docker-install.yml`)

The playbook performs the following tasks:

* Updates the package cache
* Installs required packages
* Installs Docker
* Starts the Docker service
* Enables Docker at boot
* Adds the Ubuntu user to the Docker group

<img width="918" height="857" alt="Screenshot 2026-06-27 012757" src="https://github.com/user-attachments/assets/5d65b3f9-9db6-4e88-9e03-16e134861b73" />

---

## ▶️ Commands Used

### Verify Ansible Installation

```bash
ansible --version
```

### Test Connectivity

```bash
ansible docker_servers -m ping
```
<img width="1390" height="602" alt="Screenshot 2026-06-27 005122" src="https://github.com/user-attachments/assets/bf8e1b04-7e21-4a91-b651-5ea68c6fd52f" />


### Run the Playbook

```bash
ansible-playbook docker-install.yml
```
<img width="1893" height="940" alt="Screenshot 2026-06-27 011818" src="https://github.com/user-attachments/assets/07728951-e542-4f5b-a2b1-126d3abc2928" />


### Verify Docker Installation

```bash
ansible docker_servers -a "docker --version"
```
<img width="987" height="132" alt="image" src="https://github.com/user-attachments/assets/f81528e2-bf11-4d5f-a112-5c76c139bbab" />

---

## ✅ Output

* Successfully connected to multiple EC2 instances using Ansible.
* Docker installed automatically on all target Ubuntu servers.
* Docker service started and enabled.
* User added to the Docker group.

---

## 📚 Key Learnings

* Ansible Inventory
* Ansible Configuration
* Playbooks
* YAML Syntax
* SSH Authentication
* Configuration Management
* Infrastructure Automation
* Docker Automation on AWS

---

## 👨‍💻 Author

**Sameer Dhumal**

If you found this project helpful, feel free to ⭐ the repository.
