# 🧩 Ansible Setup on AWS (Step-by-Step Notes)

## 🧠 Architecture Overview

```
Local Machine → Control Node (Ansible) → Managed Node
```

* Control Node: Runs Ansible
* Managed Node: Target machine

---

# 🚀 Step 1: Launch EC2 Instances (AWS)

## Instances Required

* 1 Control Node
* 1 Managed Node

## Configuration

* OS: Ubuntu 22.04
* Instance Type: t2.micro
* Key Pair: `ansible-key.pem`

## Security Group

* SSH (22) → My IP
* HTTP (80) → Anywhere

---

# 🔐 Step 2: Connect to Control Node

## 👉 Run on LOCAL MACHINE

```bash
ssh -i ansible-key.pem ubuntu@<CONTROL_NODE_IP>
```

---

# ⚙️ Step 3: Install Ansible

## 👉 Run on CONTROL NODE

```bash
sudo apt update
sudo apt install ansible -y
```

## Verify

```bash
ansible --version
```

---

# 🔑 Step 4: Generate SSH Key (Control Node)

## 👉 Run on CONTROL NODE

```bash
ssh-keygen
```

Press Enter for all prompts

---

# ❌ Step 5: (Failed Approach - Important Learning)

## 👉 Run on CONTROL NODE

```bash
ssh-copy-id ubuntu@<MANAGED_NODE_IP>
```

## ❌ Error:

```
Permission denied (publickey)
```

## 📌 Reason:

* AWS does NOT allow password authentication
* Only `.pem` key-based login is allowed

---

# ✅ Step 6: Correct Approach (Using .pem Key)

---

## 🔹 Copy .pem Key to Control Node

## 👉 Run on LOCAL MACHINE

```bash
scp -i ansible-key.pem ansible-key.pem ubuntu@<CONTROL_NODE_IP>:/home/ubuntu/
```

---

## 🔹 Set Permissions

## 👉 Run on CONTROL NODE

```bash
chmod 400 ansible-key.pem
```

---

## 🔹 Test SSH to Managed Node

## 👉 Run on CONTROL NODE

```bash
ssh -i ansible-key.pem ubuntu@<MANAGED_NODE_IP>
```

## ✅ Expected:

* Login without error

---

# 📂 Step 7: Create Inventory File

## 👉 Run on CONTROL NODE

```bash
nano inventory
```

## Add:

```ini
[servers]
node1 ansible_host=<MANAGED_NODE_IP> ansible_user=ubuntu ansible_ssh_private_key_file=~/ansible-key.pem
```

Save: `CTRL + X → Y → ENTER`

---

# 🧪 Step 8: Test Ansible Connection

## 👉 Run on CONTROL NODE

```bash
ansible -i inventory servers -m ping
```

## ✅ Expected Output:

```json
node1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

---

# ❌ Common Errors & Fixes

## 1. Permission denied (publickey)

**Fix:**

```bash
chmod 400 ansible-key.pem
```

---

## 2. UNREACHABLE

* Check Security Group (port 22)
* Check correct IP
* Check key path

---

## 3. Host key verification failed

```bash
ssh-keygen -R <MANAGED_NODE_IP>
```

---

# 🧠 Key Concepts (Viva Ready)

* Ansible works agentless (uses SSH)
* Control node runs all commands
* Managed node executes tasks
* Inventory defines target systems
* AWS requires `.pem` key authentication

---

# ✅ Final Summary

| Step                | Machine         |
| ------------------- | --------------- |
| SSH to control node | Local           |
| Install Ansible     | Control Node    |
| ssh-keygen          | Control Node    |
| Copy .pem file      | Local → Control |
| chmod key           | Control Node    |
| SSH test            | Control Node    |
| Create inventory    | Control Node    |
| Run ansible ping    | Control Node    |

---

# 🚀 Next Step

👉 Ad-hoc Commands:

* File copy
* Package install
* Service management

---
---


# ⚡ Ansible Ad-hoc Commands (Practical 2)

## 🧠 What are Ad-hoc Commands?

* One-line commands used for **quick tasks**
* No need to write full playbooks
* Useful for:

  * Testing
  * Quick fixes
  * Simple automation

---

# 📍 Where to Run?

👉 ALL commands run on:

* ✅ **CONTROL NODE**

---

# 🔹 Step 1: Test Connectivity

```bash
ansible -i inventory servers -m ping
```

✅ Output:

```json
"ping": "pong"
```

---

# 🔹 Step 2: Check Uptime (Command Module)

```bash
ansible -i inventory servers -m command -a "uptime"
```

📌 Runs command on managed node

---

# 🔹 Step 3: Install Package (apt module)

```bash
ansible -i inventory servers -m apt -a "name=nginx state=present" --become
```

📌 Explanation:

* `name=nginx` → package
* `state=present` → install
* `--become` → sudo access

---

# 🔹 Step 4: Check Service Status

```bash
ansible -i inventory servers -m service -a "name=nginx state=started" --become
```

---

# 🔹 Step 5: Create File

```bash
ansible -i inventory servers -m file -a "path=/home/ubuntu/test.txt state=touch"
```

---

# 🔹 Step 6: Copy File from Control → Managed

## 👉 First create file (CONTROL NODE)

```bash
echo "Hello from Ansible" > hello.txt
```

## 👉 Copy using Ansible

```bash
ansible -i inventory servers -m copy -a "src=hello.txt dest=/home/ubuntu/hello.txt"
```

---

# 🔹 Step 7: Remove File

```bash
ansible -i inventory servers -m file -a "path=/home/ubuntu/test.txt state=absent"
```

---

# 🔹 Step 8: Gather System Info (Facts)

```bash
ansible -i inventory servers -m setup
```

📌 Shows:

* OS
* IP
* Memory
* CPU

---

# 🔹 Step 9: Use Shell Module

```bash
ansible -i inventory servers -m shell -a "df -h"
```

📌 Difference:

* `command` → safer
* `shell` → supports pipes, variables

---

# ❌ Common Errors

## 1. Permission denied

👉 Add:

```bash
--become
```

---

## 2. Module failed

👉 Run:

```bash
sudo apt update
```

---

## 3. nginx not starting

👉 Check:

```bash
systemctl status nginx
```

---

# 🧠 Important Concepts (Viva)

* Ad-hoc commands = quick automation
* Modules = building blocks (ping, apt, copy, file)
* `--become` = sudo privilege
* `command` vs `shell`
---
---

