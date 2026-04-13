# 🧩 Puppet Practicals List

---

## ✅ Q2 – MOTD Configuration

### 📝 Task:
Create a Puppet manifest to:
- Manage `/etc/motd` file  
- Add a custom message  
- Set:
  - Owner: root  
  - Permission: 0644  

---

## ✅ Q3 – Utilities Setup

### 📝 Task:
Create a Puppet manifest to:
- Install packages:
  - git
  - curl
  - vim  
- Ensure `cron` service is enabled and running  
- Create directory `/opt/tools` with permission `0755`  
- Create file `/opt/tools/info.txt` with content  

---

## ✅ Q6 – Apache Web Server Automation

### 📝 Task:
Create a Puppet manifest to:
- Install `apache2`  
- Enable and start the service  
- Deploy custom homepage at `/var/www/html/index.html`  

---

## ✅ Q7 – Nginx Web Server Setup

### 📝 Task:
Create a Puppet manifest to:
- Install `nginx`  
- Enable and start the service  
- Deploy custom webpage at `/usr/share/nginx/html/index.html`  

---

## ✅ Q8 – Shared Directory Management

### 📝 Task:
Create a Puppet manifest to:
- Create `/opt/shared_data` directory  
- Set:
  - Owner: devops  
  - Group: devops  
  - Permission: 0775  
- Ensure recursive directory creation  

---

## 🔥 Summary

- Q2 → MOTD file management  
- Q3 → Package + service + file setup  
- Q6 → Apache web server automation  
- Q7 → Nginx web server automation  
- Q8 → Directory management  

👉 Total Puppet Practicals: **5**
