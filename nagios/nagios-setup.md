# 🧠 Nagios Setup Guide (AWS - EC2)

## 📌 Architecture

* **puppet-master** → Nagios Server
* **puppet-agent** → Nagios Client (NRPE)

---

# 🚀 PART 1: Nagios Server Setup (puppet-master)

---

## 🔹 Step 1: Update System

```bash
sudo apt update && sudo apt upgrade -y
```

👉 Ensures system packages are up-to-date before installation.

---

## 🔹 Step 2: Install Required Dependencies

```bash
sudo apt install -y apache2 php libapache2-mod-php build-essential \
libgd-dev unzip wget daemon \
libmcrypt-dev libssl-dev bc gawk dc snmp libnet-snmp-perl gettext
```

👉 Installs required libraries and tools needed to compile and run Nagios.

---

## 🔹 Step 3: Create Nagios User & Group

```bash
sudo useradd nagios
sudo groupadd nagcmd
sudo usermod -a -G nagcmd nagios
sudo usermod -a -G nagcmd www-data
```

👉 Creates a dedicated user and group for Nagios security and command execution.

---

## 🔹 Step 4: Download Nagios Core

```bash
cd /tmp
wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.14.tar.gz
tar -xzf nagios-4.4.14.tar.gz
cd nagios-4.4.14
```

👉 Downloads and extracts Nagios source code.

---

## 🔹 Step 5: Compile Nagios

```bash
./configure --with-command-group=nagcmd
make all
```

👉 Prepares and compiles Nagios with proper permissions.

---

## 🔹 Step 6: Install Nagios

```bash
sudo make install
sudo make install-init
sudo make install-config
sudo make install-commandmode
```

👉 Installs Nagios binaries, configs, and service files.

---

## 🔹 Step 7: Setup Web Interface

```bash
sudo make install-webconf
sudo a2enmod rewrite
sudo a2enmod cgi
```

👉 Enables Apache configuration required for Nagios UI.

---

## 🔹 Step 8: Create Web Login

```bash
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
```

👉 Creates login credentials for Nagios web interface.

---

## 🔹 Step 9: Install Nagios Plugins

```bash
cd /tmp
wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
tar -xzf nagios-plugins-2.3.3.tar.gz
cd nagios-plugins-2.3.3

./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
sudo make install
```

👉 Plugins are required for monitoring (CPU, disk, etc.).

---

## 🔹 Step 10: Start Services

```bash
sudo systemctl restart apache2
sudo systemctl enable apache2
sudo systemctl start nagios
sudo systemctl enable nagios
```

👉 Starts and enables Nagios and Apache services.

---

## 🔹 Step 11: Install NRPE Plugin (Server Side)

```bash
sudo apt install -y nagios-nrpe-plugin
```

👉 Allows Nagios server to communicate with remote clients.

---

## 🔹 Step 12: Add NRPE Command Definition

```bash
sudo nano /usr/local/nagios/etc/objects/commands.cfg
```

Add:

```bash
define command {
    command_name    check_nrpe
    command_line    /usr/lib/nagios/plugins/check_nrpe -H $HOSTADDRESS$ -c $ARG1$
}
```

👉 Defines how Nagios executes remote checks.

---

## 🔹 Step 13: Add Client Host Configuration

```bash
sudo nano /usr/local/nagios/etc/objects/clients.cfg
```

```bash
define host {
    use             linux-server
    host_name       puppet-agent
    alias           Nagios Client
    address         <AGENT_PRIVATE_IP>
}

define service {
    use                     generic-service
    host_name               puppet-agent
    service_description     CPU Load
    check_command           check_nrpe!check_load
}
```

👉 Adds the client machine and its monitoring service.

---

## 🔹 Step 14: Include Config File

```bash
sudo nano /usr/local/nagios/etc/nagios.cfg
```

Add:

```bash
cfg_file=/usr/local/nagios/etc/objects/clients.cfg
```

👉 Tells Nagios to load client configuration.

---

## 🔹 Step 15: Validate Configuration (VERY IMPORTANT)

```bash
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

👉 Checks for errors before restarting (prevents failures).

---

## 🔹 Step 16: Restart Nagios

```bash
sudo systemctl restart nagios
```

👉 Applies all configurations.

---

---

# 💻 PART 2: Nagios Client Setup (puppet-agent)

---

## 🔹 Step 1: Update System

```bash
sudo apt update
```

👉 Ensures latest package list.

---

## 🔹 Step 2: Install NRPE & Plugins

```bash
sudo apt install -y nagios-nrpe-server nagios-plugins
```

👉 Installs agent that communicates with Nagios server.

---

## 🔹 Step 3: Configure NRPE

```bash
sudo nano /etc/nagios/nrpe.cfg
```

Find:

```bash
allowed_hosts=127.0.0.1
```

Change to:

```bash
allowed_hosts=127.0.0.1,<NAGIOS_SERVER_PRIVATE_IP>
```

👉 Allows only Nagios server to query this client.

---

## 🔹 Step 4: Restart NRPE

```bash
sudo systemctl restart nagios-nrpe-server
sudo systemctl enable nagios-nrpe-server
```

👉 Starts NRPE service.

---

## 🔹 Step 5: Verify NRPE

```bash
sudo systemctl status nagios-nrpe-server
```

👉 Should show **active (running)**.

---

---

# 🔗 PART 3: Test Connection

Run on **puppet-master**:

```bash
/usr/lib/nagios/plugins/check_nrpe -H <AGENT_PRIVATE_IP>
```

👉 Expected output:

```
NRPE vX.X.X
```

---

---

# 🌐 PART 4: Access Web UI

```
http://<PUBLIC_IP>/nagios
```

* Username: `nagiosadmin`
* Password: (your set password)

---

---

# ⚠️ Common Errors & Fixes

---

## ❌ Nagios not starting

👉 Fix:

```bash
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

---

## ❌ check_nrpe not found

👉 Fix:

```bash
sudo apt install nagios-nrpe-plugin
```

---

## ❌ Host stuck in PENDING

👉 Wait 1–2 mins OR schedule check manually.

---

## ❌ Swap CRITICAL

👉 Normal in AWS (no swap) — ignore.

---

---

# 🎯 Final Outcome

You will have:

* ✅ Nagios Server running
* ✅ Client connected
* ✅ CPU monitoring working
* ✅ Web UI accessible

----
----
----


# 📘 Adding Services in Existing Nagios Setup

## 📌 Context

* **Nagios Server:** `puppet-master`
* **Nagios Client:** `puppet-agent`
* Communication via **NRPE (port 5666)**
* Existing setup already monitors **CPU Load**

---

# 🧠 Concept

* **Host = Machine (puppet-agent)**
* **Service = What to monitor (Disk, Users, Processes, etc.)**

👉 To add new services:

* Configure **service definitions on server**
* Ensure **corresponding commands exist on client (NRPE)**

---

# 🚀 PART 1: Add Services on Nagios Server (puppet-master)

---

## 🔹 Step 1: Open Client Config File

```bash
sudo nano /usr/local/nagios/etc/objects/clients.cfg
```

👉 This file contains:

* Host definition
* All service definitions for that host

---

## 🔹 Step 2: Add New Service Blocks

### ✅ Disk Usage

```bash
define service {
    use                     generic-service
    host_name               puppet-agent
    service_description     Disk Usage
    check_command           check_nrpe!check_disk
}
```

---

### ✅ Current Users

```bash
define service {
    use                     generic-service
    host_name               puppet-agent
    service_description     Current Users
    check_command           check_nrpe!check_users
}
```

---

### ✅ Total Processes

```bash
define service {
    use                     generic-service
    host_name               puppet-agent
    service_description     Total Processes
    check_command           check_nrpe!check_procs
}
```

---

## 🔹 Step 3: Validate Configuration (MANDATORY)

```bash
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

👉 Purpose:

* Detect syntax errors
* Prevent Nagios service failure

---

## 🔹 Step 4: Restart Nagios

```bash
sudo systemctl restart nagios
```

👉 Applies new service configurations

---

## 🔹 Step 5: Verify in Web UI

* Navigate to: **Services**
* Confirm new services appear:

  * Disk Usage
  * Current Users
  * Total Processes

---

# ⚠️ PART 2: Ensure Commands Exist on Client (puppet-agent)

---

## 🔹 Step 1: Check Existing NRPE Commands

```bash
cat /etc/nagios/nrpe.cfg | grep command
```

👉 Look for:

* `check_disk`
* `check_users`
* `check_procs`

---

## 🔹 Step 2: If Commands Already Exist

👉 No action needed — services will work directly

---

## 🔴 Step 3: If Command is MISSING (Important Case)

👉 You MUST manually define it in NRPE config

---

### 🔹 Open NRPE Config

```bash
sudo nano /etc/nagios/nrpe.cfg
```

---

### 🔹 Add Missing Commands (Examples)

```bash
command[check_disk]=/usr/lib/nagios/plugins/check_disk -w 20% -c 10% -p /
command[check_users]=/usr/lib/nagios/plugins/check_users -w 5 -c 10
command[check_procs]=/usr/lib/nagios/plugins/check_procs -w 250 -c 400
```

👉 These define what NRPE executes when server requests data

---

## 🔹 Step 4: Restart NRPE Service

```bash
sudo systemctl restart nagios-nrpe-server
```

👉 Applies new command definitions

---

## 🔹 Step 5: Test from Server (Recommended)

On **puppet-master**:

```bash
/usr/lib/nagios/plugins/check_nrpe -H <AGENT_PRIVATE_IP> -c check_disk
```

👉 Expected:

* Output showing disk status (OK/WARNING/CRITICAL)

---

# 🚨 Common Errors & Fixes

---

## ❌ Service shows UNKNOWN

👉 Cause:

* Command not defined in NRPE

👉 Fix:

* Add command in `/etc/nagios/nrpe.cfg`
* Restart NRPE

---

## ❌ Nagios not restarting

👉 Cause:

* Syntax error in `clients.cfg`

👉 Fix:

```bash
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

---

## ❌ NRPE connection failed

👉 Causes:

* Wrong IP in `allowed_hosts`
* Port 5666 blocked

---

# 🎯 Final Outcome

After completing this:

* ✅ Multiple services added to existing host
* ✅ Server properly configured
* ✅ Client provides required metrics
* ✅ Monitoring visible in Nagios UI

---

# 🧠 Key Takeaways

* Services are defined **on server**
* Commands are executed **on client**
* NRPE acts as communication bridge
* Always validate config before restart

---

