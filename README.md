# DevOps Ninja Jenkins Assignments - README

Welcome to the **DevOps Ninja Jenkins Assignments** repository. This project demonstrates hands-on Jenkins CI/CD automation skills across multiple real-world scenarios, including pipeline creation, job configuration, authorization, node management, and failure notifications.

---

## Assignments Overview

### **Assignment 1: Git Branch Operations + Parameterized Job Chaining**

#### Part 1: Git Branching Automation
- Jenkins Freestyle job that performs:
  - Create a branch
  - List all branches
  - Merge branches
  - Rebase branches
  - Delete a branch
- Slack and Email notifications on **any step failure**.

#### Part 2: Parameterized & Chained Jobs
- Job 1: Takes `<Ninja Name>` as input, creates a file, writes:
  > "`<Ninja Name> from DevOps Ninja`"
- Job 2: Automatically triggers after Job 1 and **serves the file content on a web server**.
- Notifications on success or failure using Slack and Email.

---

###  **Assignment 2: User Authentication & Authorization in Jenkins**

#### Jenkins Roles Setup
- **Teams**: Developer, Testing, DevOps, Admin
- **Jobs**: 3 per team, total 9 dummy jobs
- **Views**: Each team sees relevant jobs only
- **Users & Permissions**:
  - Developer: access to dev jobs
  - Tester: dev + test jobs
  - DevOps: all jobs
  - Admin: full access

#### Authorization Strategy:
- Implemented using **Role-Based Strategy Plugin**.
- Evaluated alternatives:
  - Legacy mode
  - Project-based
  - Matrix-based

#### Bonus:
- Enabled **SSO (Single Sign-On) with Google** for admin login.

---

###  **Assignment 3: CI Checks for Polyglot Repositories**

#### Repositories Used:
- **Python**: [attendance-api](https://github.com/OT-MICROSERVICES/attendance-api)
- **GoLang**: [employee-api](https://github.com/OT-MICROSERVICES/employee-api)
- **Java**: [spring3hibernate](https://github.com/opstree/spring3hibernate.git)

#### Jenkins Setup:
- Freestyle jobs per language.
- Generic & advanced CI checks:
  - Unit testing
  - Dependency scans
  - Credential scanning
  - Code coverage
- Reports stored and artifacts archived.
- Slack & Email alerts on failures.

---

###  **Assignment 4: Agent Configuration & Load Distribution**

#### Node Configurations:
| OS        | Launch Method             | Max Jobs | Assigned To               |
|-----------|---------------------------|----------|----------------------------|
| Ubuntu    | Command on Master         | 5        | Assignment 1 - Part 1      |
| RHEL      | Launch agent via SSH      | 2        | Assignment 1 - Part 2      |


#### Time-Based Execution:
- Jobs between **9 AM – 6 PM** run on configured nodes.
- Outside those hours, jobs run on **Master** node.

---

### **Assignment 5: Declarative Pipeline for Java Project**

#### Features:
- **Declarative Pipeline** with following stages:
  - Code checkout
  - Parallel:
    - Code Stability
    - Code Quality (SonarQube)
    - Code Coverage (Jacoco)
  - Manual approval for artifact publishing
  - Artifact upload
  - Slack & Email notifications

#### Advanced Features:
- **Skippable stages** via pipeline parameters
- **Approval gate** before publishing artifacts
- Artifact storage using Jenkins built-in archive
- Optional: Repeat the same using **Scripted Pipeline**

---

##  Technologies Used

- Jenkins
- Git & GitHub
- Slack & Email Plugins
- SonarQube
- Jacoco
- Maven / Gradle
- Ubuntu, CentOS, RHEL Nodes
- Shell Scripting
- Google SSO

---



