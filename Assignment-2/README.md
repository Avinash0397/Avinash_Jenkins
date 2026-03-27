#  Jenkins Role-Based Authorization & SSO Integration

## Assignment 2: User Authentication & Authorization

This project demonstrates secure Jenkins setup with:

- Role-based access control (RBAC)
- View-based job segregation
- SSO (Single Sign-On) integration for Admin via Google

---

##  Part 1: Jenkins Role-Based Authorization

###  Jenkins Job Structure

Create **9 Jenkins jobs** to simulate workflows for 3 different teams:

####  Developer Team Jobs

- `dev-1`
- `dev-2`
- `dev-3`

####  Testing Team Jobs

- `test-1`
- `test-2`
- `test-3`

####  DevOps Team Jobs

- `devops-1`
- `devops-2`
- `devops-3`

> 🔹 Each job prints its own name and build number.

![Screenshot 2025-05-12 173144](https://github.com/user-attachments/assets/ac0e8aff-db26-4fbf-b94e-a84506887e0f)

---

###  User Access & Role Definitions

| Role        | Users            | Permissions                                                                 |
|-------------|------------------|------------------------------------------------------------------------------|
| Developer   | developer-1, developer-2 | - Can see only `dev-*` jobs<br>- Can build, see workspace, configure        |
| Testing     | testing-1, testing-2     | - Can see `test-*` jobs<br>- Can build, see workspace, configure<br>- Can view `dev-*` jobs |
| DevOps      | devops-1, devops-2       | - Can see `devops-*` jobs<br>- Can build, see workspace, configure<br>- Can view `dev-*` and `test-*` jobs |
| Admin       | admin-1                 | - Full access across Jenkins                                                |

---

![Screenshot 2025-05-12 173022](https://github.com/user-attachments/assets/436ec48a-933c-4be4-8b53-81d2fac46e25)
### 👀 Views Setup

Create Jenkins views to logically group jobs:

- `Developer View`: shows only `dev-*` jobs
- `Testing View`: shows only `test-*` jobs
- `DevOps View`: shows only `devops-*` jobs

---

### 🔒 Recommended Authorization Strategy

Use the **Role-Based Strategy Plugin** for fine-grained control.

#### ✅ Steps:

1. Go to **Manage Jenkins > Configure Global Security**
2. Under **Authorization**, select **Role-Based Strategy**
3. Go to **Manage Jenkins > Manage and Assign Roles > Manage Roles**
4. Create these roles:
   - `developer`
   - `testing`
   - `devops`
   - `admin`
5. Assign specific **job permissions** (Job: Build, Configure, Read, Workspace) to each role
6. Go to **Assign Roles** and map users to their respective roles
7. Use **job name patterns** like `dev-*`, `test-*`, `devops-*` for role visibility

![Screenshot (529)](https://github.com/user-attachments/assets/c8b5efec-4c45-4a13-bff3-75ba06e9d949)


![Screenshot 2025-05-12 173022](https://github.com/user-attachments/assets/1d5786fc-3afa-4a69-a0f5-b0c8e74a08c6)

---


### 🔄 Comparison of Authorization Strategies

| Strategy       | Description                                                                 | Use Case Suitability |
|----------------|-----------------------------------------------------------------------------|-----------------------|
| **Legacy Mode** | All users get full control.                                                  |  Not secure         |
| **Project-Based** | Authorization defined per project.                                          |  Limited control     |
| **Matrix-Based** | Granular control over user permissions.                                      |  Suitable but verbose |
| **Role-Based**   | Best practice for team-based access control with scalable permission sets. | Recommended         |


![Screenshot 2025-05-12 173033](https://github.com/user-attachments/assets/4f907712-c0d9-463b-b4cc-0fc675f305cb)


---

## 📌 Part 2: Enable SSO with Google for Admin User

### 🎯 Objective

Enable **SSO login for `admin-1`** using their Google account.

---

### 🛠️ Tools Required

- Jenkins
- `Google Login Plugin` (SSO)
- Google Developer Console

---

### 🔧 Setup Steps

1. Install **Google Login Plugin** in Jenkins
2. Go to **https://console.developers.google.com/**
3. Create a new project and navigate to:
   - **APIs & Services > Credentials**
4. Create **OAuth 2.0 Client ID**
   - Application Type: **Web Application**
   - Add **Authorized Redirect URI**:
     ```
     http://<your-jenkins-url>/securityRealm/finishLogin
     ```

     ![image](https://github.com/user-attachments/assets/bc554a9c-eb14-495a-a702-4887006f3155)

5. Copy **Client ID** and **Client Secret**
6. In Jenkins:
   - Go to **Manage Jenkins > Configure Global Security**
   - Select **Google Apps Authentication**
   - Paste Client ID and Secret
   - Restrict login to domain or user if needed
     
![image](https://github.com/user-attachments/assets/7f764e9b-8dfa-49b4-bbb1-62b021ecbd7f)

---

