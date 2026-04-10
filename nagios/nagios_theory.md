
# 1. Continuous Monitoring Concepts

## Monitoring
Monitoring is the process of observing a system’s health, performance, and availability.

Example:
- Checking CPU usage
- Monitoring website uptime

---

## Continuous Monitoring
Continuous Monitoring means automatically monitoring systems in real-time (24/7).

Example:
- Alert when server goes down
- Alert when CPU > 90%

---

## Importance of Monitoring
- Detect issues early
- Reduce downtime
- Improve system reliability

---

## Benefits
- Early problem detection
- Reduced downtime
- Performance optimization
- Automation
- Security monitoring

---

## Types of Monitoring
1. Infrastructure Monitoring (CPU, RAM, Disk)
2. Application Monitoring
3. Network Monitoring
4. Security Monitoring

---

## Key Concepts
- Metric: Measurable value (CPU usage)
- Threshold: Limit set (CPU > 80%)
- Alert: Notification when threshold is crossed
- Incident: System failure or abnormal behavior

---

## Monitoring Flow
System → Data Collection → Threshold Check → Alert
-----
-----

# 2. Introduction to Nagios

## What is Nagios?
Nagios is an open-source monitoring tool used to monitor systems, networks, and infrastructure.

---

## Features
- Real-time monitoring
- Alerting system (Email, SMS)
- Plugin-based architecture
- Web interface
- Scalable

---

## Nagios Architecture

### Components
1. Nagios Core
   - Schedules checks
   - Processes results
   - Sends alerts

2. Plugins
   - Perform actual checks
   - Example: CPU, Disk, HTTP

3. Agents (NRPE)
   - Installed on remote systems
   - Enable remote monitoring

---

## Architecture Flow
Nagios Core → Plugin → System Check → Result → Alert

---

## Hosts vs Services

### Host
- A system/device (server)

### Service
- A function running on host
- Example: HTTP, CPU, Disk

---

## Soft State vs Hard State

### Soft State
- Temporary issue
- No alert yet

### Hard State
- Confirmed issue
- Alert is triggered

---

## Nagios States
- OK
- WARNING
- CRITICAL
- UNKNOWN

---

## Importance
- Reduces downtime
- Early issue detection
- Automation

----
----
