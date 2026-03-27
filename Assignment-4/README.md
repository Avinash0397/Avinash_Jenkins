# Assignment 4: Jenkins Node Configuration and Load Distribution

## Objective

Set up Jenkins agents (nodes) on various Linux systems and configure job execution distribution with time-based and job-specific constraints.

---

## Prerequisites

- Jenkins Master installed and accessible
- SSH access and Java installed on agent machines (RHEL, CentOS)
- Proper hostname resolution between master and nodes
- Necessary ports (e.g., 22 for SSH) are open between Jenkins master and nodes

---

## 🧾 Node Configuration Summary

| Node Type | OS     | Method                         | Max Jobs | Assigned To           |
|-----------|--------|--------------------------------|----------|------------------------|
| Node 1    | Ubuntu | Execution via Command on Master| 5        | Assignment 1: Part 1   |
| Node 2    | RHEL   | Launch via SSH                 | 2        | Assignment 1: Part 2   |

![image](https://github.com/user-attachments/assets/9385fd5e-8eba-4bc2-aaec-4b98f724ad59)


---

## 🔧 Steps to Configure Nodes

### Node 1: Ubuntu (Execution via command on the master)

1. **On Ubuntu Node:**
   - Ensure Java is installed:  
     ```bash
     sudo apt update && sudo apt install openjdk-11-jdk -y
     ```
2. **On Jenkins Master:**
   - Go to `Manage Jenkins → Manage Nodes → New Node`
   - Name: `ubuntu-node`
   - Type: Permanent Agent
   - Launch method: **Launch agent by connecting it to the master**
   - Work Directory: `/home/jenkins`
   - Number of Executors: **5**
   - Usage: Only build jobs with label expressions → `assignment1-part1`
   - Label: `assignment1-part1 ubuntu`
   - Save

3. On the Ubuntu node, execute the command shown under the "Command to run agent" section to connect the node.

![image](https://github.com/user-attachments/assets/0b37b4e6-1c82-4184-9278-bce043a97889)


---

### Node 2: RHEL (Launch via SSH)

1. **On RHEL Node:**
   - Ensure Java is installed:
     ```bash
     sudo yum install java-11-openjdk -y
     ```
   - Create Jenkins user and set SSH key

2. **On Jenkins Master:**
   - Add RHEL SSH credentials (username + private key)
   - Go to `Manage Jenkins → Manage Nodes → New Node`
   - Name: `rhel-node`
   - Type: Permanent Agent
   - Launch Method: **Launch agents via SSH**
   - Host: `<RHEL_IP>`
   - Credentials: Use the one created
   - Number of Executors: **2**
   - Label: `assignment1-part2 rhel`
   - Usage: Only build jobs with label expressions
   - Save

---


##  Time-Based Job Execution

### Goal:
If job runs **between 9:00 AM and 6:00 PM**, execute on **agent node** (ubuntu, rhel, or centos).
If outside this time, execute on **master node**.

###  Approach:
1. In each Jenkins job, add a **pre-build step** with the following Shell script:
```bash
#!/bin/bash

HOUR=$(date +"%H")
if [ "$HOUR" -ge 9 ] && [ "$HOUR" -lt 18 ]; then
    echo "Executing during working hours, forcing agent node..."
    echo "AGENT_LABEL=true" > .env
else
    echo "Outside working hours, using master..."
    echo "AGENT_LABEL=false" > .env
fi
