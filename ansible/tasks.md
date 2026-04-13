# ⚙️ Ansible Practicals List

---

## ✅ Q4 – Apache Installation and Setup

### 📝 Task:
Create an Ansible playbook to:
- Install `apache2`
- Enable and start the service
- Deploy a custom homepage at `/var/www/html/index.html`

---

## ✅ Q5 – Connectivity Check

### 📝 Task:
- Configure Ansible inventory file (`/etc/ansible/hosts`) with at least 3 hosts
- Run ping module to check connectivity
- Interpret the results (success/failure)

---

## ✅ Q10 – Multiple Package Installation

### 📝 Task:
Create an Ansible playbook to:
- Install multiple packages:
  - git
  - curl
  - vim
- Use loop mechanism
- Ensure state is `present`

---

## 🔥 Summary

- Q4 → Apache setup using playbook  
- Q5 → Inventory + connectivity testing  
- Q10 → Multiple package installation using loop  

👉 Total Ansible Practicals: **3**
---
---


# ⚙️ Ansible Practicals (Step-by-Step Execution)

---

# ✅ Q5 – Connectivity Check

## 🧠 Goal

* Setup inventory with multiple hosts
* Test connectivity using ping module

---

## 📍 Where to Run?

👉 All steps on **CONTROL NODE**

---

## 🔹 Step 1: Edit Inventory File

```bash
sudo nano /etc/ansible/hosts
```

## Add:

```ini
[servers]
node1 ansible_host=<MANAGED_NODE_IP1> ansible_user=ubuntu ansible_ssh_private_key_file=~/ansible-key.pem
node2 ansible_host=<MANAGED_NODE_IP2> ansible_user=ubuntu ansible_ssh_private_key_file=~/ansible-key.pem
node3 ansible_host=<MANAGED_NODE_IP3> ansible_user=ubuntu ansible_ssh_private_key_file=~/ansible-key.pem
```

📌 If you have only 1 node:

```ini
node1 ansible_host=<MANAGED_NODE_IP>
```

---

## 🔹 Step 2: Run Ping

```bash
ansible servers -m ping
```

---

## ✅ Expected Output

```json
node1 | SUCCESS => {
    "ping": "pong"
}
```

---

## ❌ Failure Example

```bash
UNREACHABLE! => {
    "msg": "Permission denied"
}
```

---

## 🧠 Interpretation

| Result      | Meaning       |
| ----------- | ------------- |
| SUCCESS     | Connection OK |
| UNREACHABLE | SSH issue     |
| FAILED      | Module issue  |

---

# ✅ Q4 – Apache Installation & Setup

## 🧠 Goal

* Install Apache
* Start & enable service
* Deploy custom webpage

---

## 📍 Where to Run?

👉 Create & run on **CONTROL NODE**

---

## 🔹 Step 1: Create Playbook

```bash
nano apache.yml
```

## Add:

```yaml
- name: Install and configure Apache
  hosts: servers
  become: yes

  tasks:
    - name: Install apache2
      apt:
        name: apache2
        state: present
        update_cache: yes

    - name: Start Apache service
      service:
        name: apache2
        state: started
        enabled: yes

    - name: Deploy custom homepage
      copy:
        content: "<h1>Hello from Ansible</h1>"
        dest: /var/www/html/index.html
```

---

## 🔹 Step 2: Run Playbook

```bash
ansible-playbook apache.yml
```

---

## 🔹 Step 3: Verify

👉 Open browser:

```bash
http://<MANAGED_NODE_IP>
```

---

# ✅ Q10 – Multiple Package Installation (Loop)

## 🧠 Goal

* Install multiple packages using loop

---

## 📍 Where to Run?

👉 CONTROL NODE

---

## 🔹 Step 1: Create Playbook

```bash
nano packages.yml
```

## Add:

```yaml
- name: Install multiple packages
  hosts: servers
  become: yes

  tasks:
    - name: Install packages
      apt:
        name: "{{ item }}"
        state: present
        update_cache: yes
      loop:
        - git
        - curl
        - vim
```

---

## 🔹 Step 2: Run Playbook

```bash
ansible-playbook packages.yml
```

---

## 🔹 Step 3: Verify

```bash
ansible servers -a "git --version"
ansible servers -a "curl --version"
ansible servers -a "vim --version"
```

---

# 🔥 Final Summary

| Question | What You Did           |
| -------- | ---------------------- |
| Q5       | Inventory + Ping       |
| Q4       | Apache Setup           |
| Q10      | Loop + Package Install |

---

# 🧠 Viva Questions (IMPORTANT)

* What is inventory file?
* Difference between ad-hoc and playbook?
* What is `become`?
* What is loop in Ansible?
* Why use YAML?

---
