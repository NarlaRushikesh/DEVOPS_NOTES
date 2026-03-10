# 1. Configuration Management

## What is Configuration?

Configuration refers to **how a system or server is set up**.

It includes:
- Operating System
- Installed Software
- System Settings
- Security Rules
- Network Configuration
- Running Services

### Example Configuration of a Server

```
OS: Ubuntu
Java Version: 17
Web Server: Nginx
Port: 8080
Firewall: Enabled
```

All these settings together form the **system configuration**.

---

# What is Configuration Management?

Configuration Management is the **process of automatically managing and maintaining system configurations across multiple servers**.

It ensures that all systems remain **consistent, reliable, and properly configured**.

Instead of configuring each server manually, we define the configuration **once** and apply it to **all servers automatically**.

---

# Why Configuration Management is Needed

Managing servers manually causes many problems:

- Time consuming
- Human errors
- Inconsistent environments
- Difficult to scale infrastructure

### Example Without Configuration Management

```
Server1 → Java 17
Server2 → Java 11
Server3 → Java Missing
```

This creates **inconsistent environments**.

### Example With Configuration Management

Configuration defined once:

```
Install Java 17
Install Nginx
Start Nginx Service
```

Result:

```
Server1 → Correct
Server2 → Correct
Server3 → Correct
Server100 → Correct
```

All servers become **consistent**.

---

# Real Life Analogy

Think of **McDonald's burger recipe**.

Every burger tastes the same because they follow a **standard recipe**.

Example recipe:

```
Bun
Patty
Cheese
Sauce
```

Workers follow the same instructions everywhere.

Similarly, configuration management tools act like **a recipe for servers**.

---

# What Configuration Management Tools Do

Configuration management tools can:

- Install software
- Configure system files
- Manage services (start/stop/restart)
- Manage users and permissions
- Enforce security settings
- Maintain consistency across servers

Example:

If someone removes Nginx manually:

```
sudo systemctl stop nginx
```

Configuration management tool will **detect it and restart it automatically**.

---

# Popular Configuration Management Tools

Some widely used tools:

| Tool | Description |
|-----|-------------|
| Puppet | Configuration automation tool |
| Chef | Infrastructure automation |
| Ansible | Agentless configuration management |
| SaltStack | Remote configuration tool |

In this course we are learning **Puppet**.

---

# Key Benefits

- Automation of system configuration
- Consistent environments
- Faster server setup
- Reduced human errors
- Easier infrastructure scaling
- Self-healing systems

---

# Simple Definition (Interview Friendly)

Configuration Management is the process of **automatically maintaining and managing system configurations across multiple servers to ensure consistency and reliability.**

---

# Summary

Configuration Management means:

```
Write configuration once
Apply it to all servers
Maintain consistency automatically
```

Instead of manually managing many servers, configuration management tools **automate everything**.

----

# 2. Pull vs Push Model

This concept explains **how configuration changes are delivered to servers** in a configuration management system.

There are two main models:

1. Push Model
2. Pull Model

---

# Push Model

## Definition

In the **Push Model**, the **central server or administrator sends configuration instructions directly to the client machines (servers).**

The servers simply **receive and execute the instructions**.

---

## How It Works

The administrator machine connects to all servers and pushes the configuration.

```
Admin Server
     |
     |----> Server1
     |----> Server2
     |----> Server3
     |----> Server4
```

---

## Example

Suppose we want to install **Nginx** on multiple servers.

The administrator runs a command:

```
Install Nginx on all servers
```

Execution flow:

```
Admin → Server1 → Install Nginx
Admin → Server2 → Install Nginx
Admin → Server3 → Install Nginx
```

---

## Real Life Analogy

Think of a **teacher distributing exam papers**.

```
Teacher → Student1
Teacher → Student2
Teacher → Student3
```

Students do not request the paper.  
The teacher **pushes it to them**.

---

## Advantages

- Immediate execution
- Easy to control from central system
- Simple architecture

---

## Disadvantages

- Difficult to manage thousands of servers
- Admin must maintain connections to all machines
- May cause network overload

---

## Tools That Use Push Model

Example tools:

- **Ansible**
- **SaltStack (can also support pull)**

---

# Pull Model

## Definition

In the **Pull Model**, the **client machines request configuration from the central server**.

The servers periodically check if there are **new updates or configurations**.

---

## How It Works

```
          Puppet Master
           /    |    \
          /     |     \
      Server1 Server2 Server3
         ↑        ↑        ↑
         |        |        |
   Pull configuration from master
```

Servers contact the central server and ask for configuration updates.

---

## Example

Every fixed interval (e.g., 30 minutes), the server asks:

```
Do you have any new configuration?
```

If yes, it downloads and applies it.

Execution flow:

```
Server1 → Puppet Master → Get configuration
Server2 → Puppet Master → Get configuration
Server3 → Puppet Master → Get configuration
```

---

## Real Life Analogy

Think of a **notice board in a school**.

Students check the notice board regularly.

```
Student → Notice Board → Check for updates
```

If a new notice is posted, they follow it.

---

## Advantages

- Highly scalable
- Servers manage their own updates
- Works well with large infrastructure

---

## Disadvantages

- Changes are not applied immediately
- Depends on the polling interval

---

## Tools That Use Pull Model

Examples:

- **Puppet**
- **Chef**

---

# Push vs Pull Comparison

| Feature | Push Model | Pull Model |
|------|------|------|
| Who initiates the action | Admin server | Client server |
| Communication | Server pushes configuration | Clients request configuration |
| Scalability | Limited scalability | Highly scalable |
| Example tools | Ansible | Puppet, Chef |

---

# Easy Way to Remember

Push Model:

```
Admin → Servers
```

Pull Model:

```
Servers → Master
```

---

# Puppet Architecture Model

Puppet follows the **Pull Model**.

```
Puppet Master → Stores configurations
Puppet Agent → Pulls configurations from the master
```

Agents periodically request configuration updates from the Puppet Master.

---

# Interview Definition

**Push Model**

Configuration changes are **sent from the central server to client machines directly**.

**Pull Model**

Client machines **periodically request configuration updates from a central server**.

---

# Summary

Push Model:

```
Admin pushes configuration to servers
```

Pull Model:

```
Servers pull configuration from central server
```

Puppet uses the **Pull Model**.

---

# 3. Introduction to Puppet

## What is Puppet?

Puppet is an **open-source configuration management tool** used to **automatically manage and configure servers**.

It allows administrators to:
- Install software
- Configure systems
- Manage services
- Maintain consistency across multiple servers

Instead of manually configuring each server, administrators **write configuration once**, and Puppet applies it automatically across all machines.

---

# Simple Definition

**Puppet** is a tool that **automates server configuration and management across multiple machines.**

---

# Why Puppet is Needed

Consider a company with **hundreds of servers**.

Each server must have:

```
Ubuntu OS
Java Installed
Nginx Installed
Firewall Enabled
Same configuration files
```

Without automation, an administrator must manually configure every server.

Example:

```
Login → Server1
Install Java
Install Nginx

Login → Server2
Install Java
Install Nginx
...
Login → Server500
```

Problems:
- Time consuming
- Human errors
- Inconsistent configurations

---

# How Puppet Solves This Problem

With Puppet, the administrator defines the configuration **once**.

Example configuration:

```
Install Nginx
Ensure Nginx service is running
```

Puppet automatically applies this configuration to all servers.

---

# Self-Healing Infrastructure

If someone manually stops Nginx:

```
sudo systemctl stop nginx
```

Puppet detects the issue and **automatically starts the service again**.

This ensures servers always remain in the **correct configuration state**.

---

# Desired State Concept

Puppet works based on the **Desired State Model**.

The administrator defines how the system **should look**.

Example:

Desired state:

```
Nginx installed
Nginx service running
```

If the server deviates from this state, Puppet **automatically corrects it**.

Example:

```
Current State → Nginx stopped
Desired State → Nginx running
```

Puppet will start the service automatically.

---

# Main Components of Puppet

Puppet mainly works with two components:

### Puppet Master

The **central server** that stores configuration instructions.

Example configuration stored on master:

```
Install Nginx
Create user "developer"
Start Nginx service
```

---

### Puppet Agent

Installed on **client machines (servers)**.

The agent periodically contacts the Puppet Master and asks for updates.

Example request:

```
Do you have any new configuration?
```

If updates exist, the agent downloads and applies them.

---

# Puppet Workflow

Basic workflow:

```
Puppet Master → Stores configurations
Server (Agent) → Requests configuration
Agent → Applies configuration
```

---

# Example Puppet Scenario

Suppose the administrator wants to install Nginx on all servers.

Puppet configuration:

```
Install nginx
Ensure nginx service is running
```

Result:

```
Server1 → nginx installed
Server2 → nginx installed
Server3 → nginx installed
```

Even if nginx is removed manually, Puppet reinstalls it automatically.

---

# Puppet Language Example

Puppet uses its own **declarative configuration language**.

Example Puppet code:

```
package { 'nginx':
  ensure => installed,
}

service { 'nginx':
  ensure => running,
}
```

Meaning:

```
Install nginx
Ensure nginx service is running
```

---

# Where Puppet is Used

Puppet is widely used in:

- DevOps automation
- Cloud infrastructure
- Data centers
- Large-scale server management

---

# Companies Using Puppet

Examples:

- Google
- Cisco
- PayPal
- Spotify

---

# Key Features of Puppet

- Automation of server configuration
- Infrastructure as Code
- Consistent environments
- Scalable infrastructure management
- Self-healing systems

---

# Puppet Architecture Overview

```
        Puppet Master
             |
             |
    ---------------------
    |        |         |
 Server1   Server2   Server3
  Agent     Agent     Agent
```

Agents pull configuration from the Puppet Master.

---

# Interview Definition

Puppet is an **open-source configuration management tool used to automate server setup, software installation, and system configuration across multiple machines.**

---

# Summary

Puppet helps to:

```
Automate server configuration
Maintain consistent environments
Manage large numbers of servers easily
```

Administrators write configuration once, and Puppet **automatically enforces it across all systems**.


---


# 4. Why Puppet

## Introduction

Managing servers manually becomes difficult as the number of servers increases.  
Configuration management tools like **Puppet** solve this problem by **automating server setup and configuration**.

Puppet ensures that all systems maintain the **same configuration and desired state**.

---

# Problems Without Puppet

Consider a system administrator managing **hundreds of servers**.

Each server must have:

```
Ubuntu
Java installed
Nginx installed
Security updates
Same configuration files
```

Without automation, the administrator must manually configure every server.

Example:

```
Login → Server1
Install Java
Install Nginx

Login → Server2
Install Java
Install Nginx
...
Login → Server200
```

### Issues

- Time consuming
- Human errors
- Inconsistent server configurations
- Difficult to scale infrastructure

---

# Solution: Puppet

Puppet automates server configuration.

Instead of configuring every server manually:

```
Admin writes configuration once
Puppet applies configuration to all servers
```

Example configuration:

```
Install nginx
Ensure nginx service is running
```

Puppet automatically applies this to every server.

---

# Major Reasons to Use Puppet

## 1. Automation

Puppet automates repetitive tasks such as:

- Installing software
- Managing services
- Creating users
- Updating configuration files

Example:

```
Install nginx
Start nginx service
```

Puppet performs these tasks automatically across servers.

---

## 2. Consistency Across Servers

Without Puppet:

```
Server1 → Java 17
Server2 → Java 11
Server3 → Java missing
```

With Puppet:

```
Server1 → Java 17
Server2 → Java 17
Server3 → Java 17
```

All systems remain **consistent**.

---

## 3. Infrastructure as Code (IaC)

Puppet allows infrastructure to be written as **code**.

Example Puppet code:

```
package { 'nginx':
  ensure => installed,
}
```

Benefits:

- Version control using Git
- Easy updates
- Easy rollback
- Better documentation

---

## 4. Scalability

Puppet can manage very large infrastructures.

Example:

```
10 servers → easy
100 servers → manageable
10000 servers → still manageable
```

Puppet scales easily for large environments.

---

## 5. Self-Healing Infrastructure

Puppet continuously checks the system state.

Example:

Desired state:

```
Nginx must be running
```

If someone stops nginx manually:

```
sudo systemctl stop nginx
```

Puppet automatically corrects the issue and restarts the service.

---

## 6. Faster Server Setup

Without Puppet:

```
Server setup time → 3 to 4 hours
```

With Puppet:

```
Server setup time → few minutes
```

Servers can be configured automatically.

---

# Real Life Example

A company launches **100 new servers**.

Without Puppet:

```
Each server must be configured manually
```

With Puppet:

```
Install Puppet Agent
Apply Puppet configuration
All servers are configured automatically
```

This saves a large amount of time and effort.

---

# Real Life Analogy

Think of a **factory assembly line**.

Without automation:

```
Workers assemble products manually
```

With automation:

```
Machines assemble products automatically
```

Puppet works like an **automation machine for servers**.

---

# Advantages of Puppet

- Automation of server management
- Consistent system configurations
- Scalable infrastructure
- Self-healing systems
- Infrastructure as Code
- Faster deployment and setup

---

# Interview Answer

**Why is Puppet used?**

Puppet is used to **automate server configuration, maintain consistency across systems, manage large infrastructures efficiently, and implement infrastructure as code**.

---

# Summary

Puppet helps to:

```
Automate server configuration
Maintain consistent environments
Scale infrastructure easily
Automatically fix configuration issues
```


-----

# 5. Components of Puppet

Puppet consists of several core components that work together to automate server configuration and management.

Main components of Puppet:

1. Puppet Master
2. Puppet Agent
3. Manifest
4. Module
5. Catalog
6. Facter

---

# 1. Puppet Master

## Definition

The **Puppet Master** is the **central server** that stores and manages all configuration instructions.

It is responsible for controlling and managing all client machines in the infrastructure.

---

## Responsibilities

The Puppet Master:

- Stores configuration files (manifests)
- Sends configurations to agents
- Compiles catalogs
- Manages communication with agents
- Ensures systems maintain the desired state

---

## Example

Administrator defines configuration:

```
Install nginx
Ensure nginx service is running
```

This configuration is stored on the **Puppet Master**.

Client servers request this configuration from the master.

---

## Architecture Example

```
        Puppet Master
              |
      --------------------
      |        |        |
   Server1   Server2   Server3
    Agent      Agent     Agent
```

---

# 2. Puppet Agent

## Definition

The **Puppet Agent** is software installed on client machines (servers).

It communicates with the Puppet Master and applies configurations locally.

---

## Responsibilities

The Puppet Agent:

- Requests configuration from the master
- Receives compiled catalog
- Applies configuration to the server
- Reports status back to the master

---

## Working Process

Agents periodically contact the Puppet Master (default interval ~30 minutes).

Example request:

```
Server → Puppet Master
Do you have any new configuration?
```

If updates exist, the agent downloads and applies them.

---

# 3. Manifest

## Definition

A **Manifest** is a file that contains **Puppet configuration instructions**.

It defines how a system should be configured.

Manifest files use the extension:

```
.pp
```

---

## Example Manifest

```
package { 'nginx':
  ensure => installed,
}

service { 'nginx':
  ensure => running,
}
```

Meaning:

```
Install nginx
Ensure nginx service is running
```

---

# 4. Module

## Definition

A **Module** is a collection of Puppet files organized together to manage a specific configuration.

Modules help structure Puppet code and make it reusable.

---

## Example Modules

Examples of modules:

```
nginx module
mysql module
user management module
```

Each module handles one specific functionality.

---

## Example Module Structure

```
nginx/
 ├── manifests/
 │     └── init.pp
 ├── templates/
 ├── files/
```

Modules make Puppet code **organized and scalable**.

---

# 5. Catalog

## Definition

A **Catalog** is the **final compiled configuration** generated by the Puppet Master for a client.

It contains all the instructions the Puppet Agent must apply.

---

## Flow

```
Manifest → Puppet Master → Catalog → Puppet Agent
```

Example catalog instructions:

```
Install nginx
Start nginx service
```

The agent executes these instructions to configure the system.

---

# 6. Facter

## Definition

**Facter** is a system profiling tool that collects information about the system.

It gathers facts about the client machine.

---

## Information Collected by Facter

Examples:

```
Operating System
IP Address
Hostname
Memory
CPU
Network Interfaces
```

Example output:

```
OS: Ubuntu
IP Address: 192.168.1.10
Hostname: server1
Memory: 8GB
```

---

## Why Facter is Important

Puppet can use this information to apply different configurations to different systems.

Example:

```
If OS = Ubuntu → Install nginx
If OS = Windows → Install IIS
```

---

# Puppet Component Interaction

The components work together in the following sequence:

```
Admin writes Manifest
        ↓
Stored on Puppet Master
        ↓
Agent contacts Master
        ↓
Master compiles Catalog
        ↓
Agent applies configuration
```

---

# Puppet Architecture Overview

```
        Puppet Master
             |
        (Stores manifests)
             |
      ---------------------
      |        |        |
   Server1  Server2  Server3
    Agent     Agent     Agent
       |
     Facter collects system information
```

---

# Summary Table

| Component | Description |
|------|------|
| Puppet Master | Central server that stores configurations |
| Puppet Agent | Client software that applies configurations |
| Manifest | Configuration file written in Puppet language |
| Module | Organized collection of Puppet files |
| Catalog | Final compiled configuration sent to agent |
| Facter | Tool that collects system information |

---

# Key Takeaway

Puppet components work together to:

```
Define system configuration
Distribute configuration to servers
Ensure systems remain in the desired state
```
