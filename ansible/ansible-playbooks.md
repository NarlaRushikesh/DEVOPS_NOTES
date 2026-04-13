# ⚡ Advanced Ansible Playbooks (Important)

---

# ✅ 1. Variables in Playbooks

## 🧠 Why?

* Avoid hardcoding values
* Make playbooks reusable

---

## 📍 Where to Run?

👉 CONTROL NODE

---

## 🔹 Example

```bash
nano var_playbook.yml
```

```yaml
- name: Install package using variable
  hosts: servers
  become: yes

  vars:
    package_name: nginx

  tasks:
    - name: Install package
      apt:
        name: "{{ package_name }}"
        state: present
```

---

## ▶️ Run

```bash
ansible-playbook var_playbook.yml
```

---

# ✅ 2. Handlers (VERY IMPORTANT)

## 🧠 Why?

* Run tasks ONLY when changes occur

---

## 🔹 Example

```bash
nano handler_playbook.yml
```

```yaml
- name: Handler Example
  hosts: servers
  become: yes

  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present

    - name: Update config file
      copy:
        content: "Hello Handler"
        dest: /var/www/html/index.html
      notify: Restart nginx

  handlers:
    - name: Restart nginx
      service:
        name: nginx
        state: restarted
```

---

## ▶️ Run

```bash
ansible-playbook handler_playbook.yml
```

---

## 🧠 Key Point

* Handler runs ONLY if file changes

---

# ✅ 3. Templates (Jinja2)

## 🧠 Why?

* Dynamic configuration files

---

## 🔹 Step 1: Create Template

```bash
nano index.j2
```

```html
<h1>Hello {{ name }}</h1>
```

---

## 🔹 Step 2: Playbook

```bash
nano template_playbook.yml
```

```yaml
- name: Template Example
  hosts: servers
  become: yes

  vars:
    name: Ansible User

  tasks:
    - name: Deploy template
      template:
        src: index.j2
        dest: /var/www/html/index.html
```

---

## ▶️ Run

```bash
ansible-playbook template_playbook.yml
```

---

# 🧠 Key Concepts Summary

| Concept   | Purpose               |
| --------- | --------------------- |
| Variables | Reusability           |
| Handlers  | Conditional execution |
| Templates | Dynamic files         |

---

