# 1. 🚀 Infrastructure as Code (IaC) — Notes

---

## 🧠 1. What is Infrastructure?

Infrastructure refers to all the components required to run an application:

* Servers (VMs / EC2)
* Networks (VPC, Subnets)
* Storage (Disks, S3)
* Load Balancers
* Databases
* Security configurations

> 👉 Infrastructure = Environment where your application runs

---

## ❌ 2. Traditional Infrastructure (Before IaC)

### 🔧 Manual Process:

1. Login to server
2. Install OS
3. Install dependencies
4. Configure network
5. Deploy application

---

### 🚨 Problems:

* Human errors
* No consistency (Dev ≠ Prod)
* Not scalable
* No version tracking
* Time-consuming

---

## 🔥 3. What is Infrastructure as Code (IaC)?

### ✅ Definition:

Infrastructure as Code (IaC) is the practice of provisioning and managing infrastructure using machine-readable configuration files instead of manual processes.

---

## 🧩 4. Core Idea

Instead of manually setting up infrastructure:

```text
"Create 2 servers with 4GB RAM and install Nginx"
```

👉 IaC tools automate everything based on code.

---

## 🍳 5. Real-World Analogy

| Without IaC            | With IaC               |
| ---------------------- | ---------------------- |
| Cooking without recipe | Cooking with recipe    |
| Inconsistent results   | Same result every time |
| Hard to repeat         | Easily repeatable      |

---

## ⚙️ 6. How IaC Works

1. Write configuration file (code)
2. Tool reads the code
3. Compares:

   * Desired state (defined in code)
   * Current state (actual infrastructure)
4. Makes changes to match desired state

---

## 🧠 Key Concept: Desired State

> IaC focuses on **what infrastructure should exist**, not how to create it.

---

## 🔁 7. Idempotency

### ✅ Definition:

Running the same IaC code multiple times results in the same infrastructure without duplication.

### 🧩 Example:

* Define: 1 server
* Run multiple times → still only 1 server exists

---

## ⚡ 8. Types of IaC

### 🟢 Declarative (Used by Terraform)

* Focus: **What to achieve**
* Example: "Create 3 servers"

### 🔵 Imperative

* Focus: **How to achieve**
* Example:

  1. Create server
  2. Install OS
  3. Configure network

---

## 🧠 Declarative vs Imperative

| Feature       | Declarative | Imperative   |
| ------------- | ----------- | ------------ |
| Focus         | What        | How          |
| Complexity    | Simple      | Complex      |
| Maintenance   | Easy        | Hard         |
| Example Tools | Terraform   | Bash Scripts |

---

## 🧩 9. Key Principles of IaC

### ✅ Version Control

* Store infrastructure code in Git
* Track changes & rollback

### ✅ Automation

* No manual intervention

### ✅ Reusability

* Write once, use multiple times

### ✅ Consistency

* Same setup across environments

### ✅ Self-Documentation

* Code explains infrastructure

---

## 🌍 10. Real-World Example

### Scenario:

* 10 servers
* Load balancer
* Database

### ❌ Without IaC:

* Manual setup
* Slow and error-prone

### ✅ With IaC:

* Write code once
* Deploy in minutes

---

## 🧠 11. Popular IaC Tools

| Tool      | Type        |
| --------- | ----------- |
| Terraform | Declarative |
| Ansible   | Imperative  |
| Puppet    | Declarative |
| Chef      | Imperative  |

---

## 🔥 12. Why IaC is Used

* 🚀 Faster deployment
* 🔄 Reliable setup
* 📈 Scalable infrastructure
* 🔐 Better security
* 💰 Cost-efficient

---

## ⚠️ 13. Common Misconceptions

* ❌ IaC = scripting
  ✔️ IaC manages infrastructure + state

* ❌ Only for cloud
  ✔️ Works for on-premise too

* ❌ Only automation
  ✔️ Includes consistency, versioning, lifecycle management

---

## 🎯 14. Interview Questions

### ❓ What is IaC?

Infrastructure as Code is the process of managing and provisioning infrastructure using code instead of manual processes.

---

### ❓ What is idempotency?

Idempotency ensures repeated execution produces the same result without duplication.

---

### ❓ Declarative vs Imperative?

Declarative defines the desired state, while imperative defines step-by-step procedures.

---

## ✅ Summary

* IaC replaces manual infrastructure setup
* Uses code to define infrastructure
* Ensures automation, consistency, scalability
* Supports declarative (Terraform) and imperative approaches

---
---

# 2. 🚀 Terraform — Introduction (Notes)

---

## 🧠 1. What is Terraform?

### ✅ Definition:

Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp that allows you to define, provision, and manage infrastructure using declarative configuration files.

---

## 🧩 Simple Understanding

Terraform converts **code → infrastructure**

Instead of manually creating:

* Servers
* Networks
* Databases

👉 You write code, and Terraform creates everything automatically.

---

## 🏢 2. Developed By

* Company: HashiCorp
* First Release: 2014

---

## ⚙️ 3. Key Features of Terraform

### 🌍 Multi-Cloud Support

Supports:

* AWS
* Azure
* GCP
* Kubernetes
* On-premise infrastructure

👉 One tool to manage multiple platforms

---

### 🧠 Declarative Nature

* Define **what you want**
* Terraform decides **how to create it**

---

### 🔄 Idempotency

* Running code multiple times does not create duplicates
* Ensures consistent infrastructure

---

### 📦 State Management

* Maintains a state file
* Tracks existing infrastructure
* Prevents duplication

---

### 🔌 Provider-Based Architecture

Uses providers to interact with platforms

Examples:

* AWS provider
* Azure provider
* GCP provider

---

## 🧩 4. Real-World Analogy

Terraform acts like a **remote control**:

* You give commands (write code)
* System executes actions (creates infrastructure)

---

## 🌍 5. Use Cases

### 🟢 Cloud Infrastructure Setup

* Create virtual machines
* Setup networking
* Configure load balancers

---

### 🟢 Multi-Environment Setup

* Dev
* Testing
* Production

👉 Same code, different environments

---

### 🟢 Auto Scaling Infrastructure

* Dynamically scale resources

---

### 🟢 Disaster Recovery

* Recreate infrastructure quickly using code

---

### 🟢 CI/CD Integration

* Used in pipelines for automated deployment

---

## ⚖️ 6. Terraform vs Other Tools

---

### 🔥 Terraform vs Ansible

| Feature  | Terraform      | Ansible        |
| -------- | -------------- | -------------- |
| Type     | Provisioning   | Configuration  |
| Approach | Declarative    | Imperative     |
| Focus    | Infrastructure | Software setup |

👉 Terraform creates infrastructure
👉 Ansible configures infrastructure

---

### 🔥 Terraform vs Puppet

| Feature  | Terraform                   | Puppet                   |
| -------- | --------------------------- | ------------------------ |
| Use      | Infrastructure provisioning | Configuration management |
| Language | HCL                         | DSL                      |
| Focus    | Cloud infrastructure        | System configuration     |

---

## 🧠 7. Key Concepts

### 🔹 Provider

* Plugin used to interact with cloud platforms

---

### 🔹 Resource

* Infrastructure components (VM, database, etc.)

---

### 🔹 Configuration File

* `.tf` files defining infrastructure

---

### 🔹 State

* Tracks current infrastructure status

---

## 🔄 8. Terraform Workflow (Conceptual)

1. Write configuration
2. Terraform reads configuration
3. Compares desired vs current state
4. Creates or updates infrastructure

---

## 🧠 9. Why Companies Use Terraform

* 🚀 Faster infrastructure provisioning
* 🔄 Reliable and consistent setup
* 📈 Scalable systems
* 🔐 Improved security
* 👥 Team collaboration via version control

---

## ⚠️ 10. Common Misconceptions

* ❌ Terraform installs software
  ✔️ It provisions infrastructure

* ❌ Terraform replaces Ansible
  ✔️ They complement each other

* ❌ Terraform is only for AWS
  ✔️ It supports multiple cloud platforms

---

## 🎯 11. Interview Questions

### ❓ What is Terraform?

Terraform is an open-source IaC tool used to provision and manage infrastructure using declarative configuration files.

---

### ❓ Why Terraform?

It enables automation, consistency, scalability, and multi-cloud infrastructure management.

---

### ❓ Terraform vs Ansible?

Terraform is used for infrastructure provisioning, while Ansible is used for configuration management.

---

## ✅ Summary

* Terraform is an IaC tool by HashiCorp
* Uses declarative approach
* Supports multi-cloud environments
* Maintains state for infrastructure tracking
* Works with tools like Ansible

---
