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
---
# 3. 🚀 Terraform Architecture — Notes

---

## 🧠 1. What is Terraform Architecture?

Terraform architecture describes how Terraform internally works to provision and manage infrastructure.

It defines:

* Core components
* Their roles
* Interaction between components
* Execution flow

---

## 🧩 2. High-Level Components

Terraform architecture consists of:

* Terraform CLI
* Configuration Files
* Providers
* Resources
* State
* Execution Plan

---

## ⚙️ 3. Core Components (Detailed)

---

### 🔹 3.1 Terraform CLI

Command Line Interface used to interact with Terraform.

#### Responsibilities:

* Reads configuration files
* Executes commands
* Communicates with providers
* Manages state

---

### 🔹 3.2 Configuration Files

* Written in HCL (HashiCorp Configuration Language)
* File extension: `.tf`

#### Contains:

* Providers
* Resources
* Variables
* Outputs

---

### 🔹 3.3 Providers (Very Important)

#### Definition:

A provider is a plugin that enables Terraform to interact with external APIs such as AWS, Azure, or GCP.

#### Key Points:

* Acts as a bridge between Terraform and cloud platforms
* Terraform does not directly create resources
* Providers handle API communication

---

### 🔹 3.4 Resources

Resources represent actual infrastructure components.

#### Examples:

* Virtual machines
* Databases
* Networks
* Storage systems

#### Key Idea:

> Resource = What you want to create

---

### 🔹 3.5 State (Critical Concept)

#### Definition:

State is a file that tracks the current infrastructure managed by Terraform.

#### Purpose:

* Tracks existing resources
* Maps configuration to real infrastructure
* Prevents duplication
* Enables updates and deletions

#### Key Insight:

Without state, Terraform cannot determine:

* What exists
* What needs to change

---

### 🔹 3.6 Execution Plan

#### Definition:

Execution plan shows what Terraform will do before applying changes.

#### Includes:

* Resources to create
* Resources to update
* Resources to delete

---

## 🔄 4. Internal Working Flow

---

### Step 1: Write Configuration

Define infrastructure in `.tf` files

---

### Step 2: Initialize Terraform

* Downloads required providers
* Prepares environment

---

### Step 3: Create Execution Plan

* Compares desired state with current state

---

### Step 4: Apply Changes

* Calls provider APIs
* Creates/updates infrastructure

---

### Step 5: Update State

* Saves updated infrastructure details

---

## 🧠 5. Resource Graph

#### Definition:

Terraform builds a dependency graph of resources before execution.

#### Purpose:

* Determines execution order
* Handles dependencies automatically

#### Example:

* VPC → Subnet → Server
  Terraform ensures correct order automatically

---

## 🔗 6. Component Interaction

### Flow:

User → CLI → Provider → Cloud → State

---

## 🧠 7. Key Characteristics

### ✅ Plugin-Based Architecture

* Providers act as plugins
* Easily extendable

---

### ✅ Declarative Model

* Focus on desired state

---

### ✅ State-Driven Execution

* Uses state to manage infrastructure

---

### ✅ Dependency Management

* Automatically resolves execution order

---

## ⚠️ 8. Common Mistakes

* ❌ Terraform directly creates resources
  ✔️ Providers create resources

* ❌ State is optional
  ✔️ State is essential

* ❌ Execution order is random
  ✔️ Controlled via dependency graph

---

## 🎯 9. Interview Questions

### ❓ What are Terraform components?

Terraform CLI, Providers, Resources, State, Configuration files

---

### ❓ What is a provider?

A plugin that enables interaction with cloud platforms.

---

### ❓ What is state?

A file that tracks current infrastructure.

---

### ❓ What is execution plan?

A preview of infrastructure changes before applying them.

---

## ✅ Summary

* Terraform architecture includes CLI, Providers, Resources, State, and Configuration files
* Providers act as a bridge to cloud platforms
* State tracks infrastructure
* Resource graph handles dependencies
* Execution plan previews changes

---
---


# 4. 🚀 Terraform Workflow — Notes

---

## 🧠 1. What is Terraform Workflow?

### ✅ Definition:

Terraform workflow is the sequence of steps used to provision, update, and manage infrastructure.

---

## 🔄 2. Core Workflow Steps

```
init → plan → apply → destroy
```

Each step plays a specific role in infrastructure management.

---

## ⚙️ 3. Step-by-Step Explanation

---

### 🔹 3.1 terraform init

#### 📌 Purpose:

Initialize the Terraform working directory

#### 🧠 What Happens:

* Downloads required providers
* Sets up backend (state storage)
* Prepares environment

#### 🎯 Key Idea:

Prepares Terraform to execute configuration

#### ⚠️ Notes:

* Must be run before other commands
* Run again if configuration changes significantly

---

### 🔹 3.2 terraform plan

#### 📌 Purpose:

Preview changes before applying

#### 🧠 What Happens:

* Reads configuration files
* Reads state file
* Compares:

  * Desired state (configuration)
  * Current state (existing infrastructure)

#### 📊 Output:

* Resources to create
* Resources to update
* Resources to delete

#### 🎯 Key Idea:

Dry run (no actual changes)

---

### 🔹 3.3 terraform apply

#### 📌 Purpose:

Apply changes to infrastructure

#### 🧠 What Happens:

* Executes the plan
* Calls provider APIs
* Creates/updates/deletes resources
* Updates state file

#### 🎯 Key Idea:

Transforms plan into real infrastructure

#### ⚠️ Notes:

* Makes actual changes
* May require user confirmation

---

### 🔹 3.4 terraform destroy

#### 📌 Purpose:

Delete all managed infrastructure

#### 🧠 What Happens:

* Reads state file
* Identifies resources
* Deletes them via providers

#### 🎯 Key Idea:

Clean up infrastructure completely

#### ⚠️ Notes:

* Use carefully (can remove all resources)

---

## 🔁 4. Workflow Flow

1. Write configuration
2. Run `init`
3. Run `plan`
4. Run `apply`
5. State is updated
6. Use `destroy` if needed

---

## 🧠 5. Key Concepts

---

### 🔹 Desired vs Current State

* Desired → defined in configuration
* Current → stored in state

---

### 🔹 Execution Plan

* Generated during `plan`
* Used in `apply`

---

### 🔹 Idempotency

* Running multiple times does not create duplicates

---

## 🧩 6. Real-World Analogy (Building a House)

| Step    | Terraform   | Real World       |
| ------- | ----------- | ---------------- |
| init    | Setup tools | Gather materials |
| plan    | Blueprint   | Design plan      |
| apply   | Build       | Construction     |
| destroy | Remove      | Demolition       |

---

## 🧠 7. Characteristics

* Predictable (plan shows changes)
* Safe (preview before execution)
* Repeatable (consistent results)
* Controlled (approval before apply)

---

## ⚠️ 8. Common Mistakes

* ❌ Skipping `plan`
  ✔️ Always review changes

* ❌ Running `destroy` carelessly
  ✔️ Can delete all resources

* ❌ Not running `init`
  ✔️ Required before execution

---

## 🎯 9. Interview Questions

### ❓ What is Terraform workflow?

Sequence of steps (init, plan, apply, destroy) to manage infrastructure.

---

### ❓ What does terraform init do?

Initializes directory and downloads providers.

---

### ❓ Difference between plan and apply?

* plan → preview changes
* apply → execute changes

---

### ❓ What does destroy do?

Deletes all Terraform-managed infrastructure.

---

## ✅ Summary

* Terraform workflow: init → plan → apply → destroy
* init prepares environment
* plan previews changes
* apply executes changes
* destroy removes infrastructure
* Ensures safe, predictable, and consistent deployments

---
---

# 5. 🚀 Terraform Configuration Language (HCL) — Notes

---

## 🧠 1. What is HCL?

### ✅ Definition:

HCL (HashiCorp Configuration Language) is the language used by Terraform to define infrastructure in a human-readable and declarative format.

---

## 🧩 Key Idea

* HCL is simple and readable
* It follows a **declarative approach**

👉 You define:

> What infrastructure you want

👉 Not:

> How to create it step-by-step

---

## ⚙️ 2. Terraform Configuration Structure

* Terraform uses `.tf` files
* Configuration is written using **blocks**

---

## 🧱 3. Main Building Blocks

---

### 🔹 3.1 Provider Block

#### 📌 Purpose:

Defines the platform where infrastructure will be created

#### 🧠 Concept:

* Acts as a bridge between Terraform and cloud platforms

#### Examples:

* AWS provider
* Azure provider

---

### 🔹 3.2 Resource Block (Most Important)

#### 📌 Purpose:

Defines infrastructure components

#### 🧠 Concept:

> Resource = actual infrastructure

#### Examples:

* Virtual machines
* Databases
* Networks

---

### 🔹 3.3 Variable Block

#### 📌 Purpose:

Makes configuration dynamic and reusable

#### 🧠 Concept:

* Avoid hardcoding values
* Improves flexibility

---

### 🔹 3.4 Output Block

#### 📌 Purpose:

Displays useful information after execution

#### Examples:

* Server IP address
* Application URL

---

## 🧩 4. General HCL Structure

```
block_type "label1" "label2" {
  key = value
}
```

---

### 🧩 Resource Structure

```
resource "type" "name" {
  attribute = value
}
```

---

## 🧠 5. Important Concepts

---

### 🔹 Declarative Syntax

* Define desired state
* Terraform handles execution

---

### 🔹 Arguments

* Key-value pairs inside blocks

Example:

```
instance_type = "t2.micro"
```

---

### 🔹 Expressions

* Used for dynamic values

---

### 🔹 References

* One resource can refer to another

---

## 🔗 6. Dependency Handling

---

### 🔹 Automatic Dependencies

* Terraform detects relationships automatically
* Determines execution order

#### Example:

* Network → Server
* Network created first

---

## 🧠 7. File Organization

Typical Terraform files:

* `main.tf` → main configuration
* `variables.tf` → variable definitions
* `outputs.tf` → output values

---

## ⚠️ 8. Common Mistakes

* ❌ Hardcoding values
  ✔️ Use variables

* ❌ Ignoring outputs
  ✔️ Useful for debugging

* ❌ Writing imperative logic
  ✔️ Terraform is declarative

---

## 🎯 9. Interview Questions

### ❓ What is HCL?

HCL is the language used by Terraform to define infrastructure in a declarative format.

---

### ❓ What are main blocks in Terraform?

* Provider
* Resource
* Variable
* Output

---

### ❓ What is a resource?

A resource represents an infrastructure component such as a VM, database, or network.

---

### ❓ Why use variables?

To make configurations reusable and dynamic.

---

## ✅ Summary

* HCL is Terraform’s configuration language

* Uses `.tf` files

* Core blocks:

  * Provider
  * Resource
  * Variable
  * Output

* Declarative approach

* Supports reusability and dependency handling

---


