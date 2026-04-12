# 🌐 Nagios Web Server Monitoring (Apache)

## 📌 Objective

To monitor a **web server (Apache)** running on:

* **Client:** puppet-agent
* **Server:** puppet-master (Nagios)

---

# 🧠 Concept

* Apache runs on **client**
* Nagios checks it using **check_http plugin**
* If web server is:

  * Running → ✅ OK
  * Stopped → ❌ CRITICAL

---

# 🚀 PART 1: Setup Apache on Client (puppet-agent)

---

## 🔹 Step 1: Install Apache

```bash
sudo apt update
sudo apt install -y apache2
```

👉 Installs Apache web server

---

## 🔹 Step 2: Start Apache

```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

👉 Starts and enables Apache service

---

## 🔹 Step 3: Verify Apache

Open in browser:

```text
http://<AGENT_PUBLIC_IP>
```

👉 Expected:

* Apache default page loads ✅

---

# 🔗 PART 2: Test Connectivity from Nagios Server

---

## 🔹 Step 4: Test using curl (on puppet-master)

```bash
curl http://<AGENT_PRIVATE_IP>
```

👉 Purpose:

* Ensure Nagios server can reach client web server

👉 Expected:

* HTML response output ✅

---

# ⚙️ PART 3: Configure Nagios to Monitor HTTP

---

## 🔹 Step 5: Open Client Config File (on puppet-master)

```bash
sudo nano /usr/local/nagios/etc/objects/clients.cfg
```

---

## 🔹 Step 6: Add HTTP Service

```bash
define service {
    use                     generic-service
    host_name               puppet-agent
    service_description     HTTP Web Server
    check_command           check_http
}
```

👉 Uses built-in `check_http` plugin to monitor web server

---

# 🧪 PART 4: Apply Configuration

---

## 🔹 Step 7: Validate Config

```bash
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

👉 Ensures no syntax errors

---

## 🔹 Step 8: Restart Nagios

```bash
sudo systemctl restart nagios
```

👉 Applies new monitoring configuration

---

# 📊 PART 5: Verify in Nagios UI

---

## 🔹 Step 9: Open Nagios Dashboard

```text
http://<NAGIOS_SERVER_PUBLIC_IP>/nagios
```

---

## 🔹 Step 10: Check Service Status

Navigate to:

* **Services**

👉 You should see:

* `HTTP Web Server → OK`

---

# 🧪 PART 6: Failure Testing (Important)

---

## 🔴 Step 11: Stop Apache (on puppet-agent)

```bash
sudo systemctl stop apache2
```

---

## 🔄 Step 12: Wait or Force Check

* Wait 1–2 minutes OR
* Schedule check from UI

---

## 🔴 Expected Result

* `HTTP Web Server → CRITICAL`

---

## 🟢 Step 13: Restart Apache

```bash
sudo systemctl start apache2
```

👉 Status returns to:

* `OK`

---

# ⚠️ Common Errors & Fixes

---

## ❌ HTTP shows CRITICAL (even when running)

👉 Check:

* Apache is running
* Correct IP used (PRIVATE IP in config)

---

## ❌ No response in curl

👉 Fix:

* Check security group (port 80 open)
* Check Apache status

---

## ❌ Service not appearing

👉 Fix:

* Restart Nagios
* Validate config

---

# 🎯 Final Outcome

After completing this:

* ✅ Web server successfully deployed
* ✅ Nagios monitoring HTTP service
* ✅ Failure detection working
* ✅ Real-world monitoring implemented

---

# 🧠 Key Takeaways

* `check_http` is a built-in Nagios plugin
* Nagios monitors services using plugins
* Service state changes based on availability
* Useful for uptime monitoring in real systems

---
