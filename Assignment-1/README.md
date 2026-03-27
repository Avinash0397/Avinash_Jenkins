![Screenshot 2025-05-03 115207](https://github.com/user-attachments/assets/f52d426e-e2a3-4a00-bbfc-6e462f6dff8c)
#  Jenkins Git & Web Automation Pipeline

##  Overview

This project demonstrates two Jenkins automation tasks:

- **Part 1**: Git branch operations using Jenkins with notifications.
- **Part 2**: Parameterized file creation and automatic web publishing using chained Jenkins jobs.

---

##  Part 1: Git Branch Management via Jenkins Job

###  Objective

Create a Jenkins pipeline job that performs the following Git operations:

![image](https://github.com/user-attachments/assets/1b7d53d0-02b6-4ecf-9bde-9e3ebd0833f6)


1. Create a branch
2. List all branches
3. Merge one branch into another
4. Rebase one branch onto another
5. Delete a branch

![image](https://github.com/user-attachments/assets/8cca08e1-cbfc-48c0-8b1a-1713d9f6d76d)


###  Notifications

- If **any step fails**, send a **Slack and Email notification** with:
  - Job name
  - Failed step name
  - Error message or reason
- If **all steps succeed**, optionally send a success notification.

```

Started by user Hifza Khan
Running as SYSTEM
Building in workspace /var/lib/jenkins/workspace/Assignment-1
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/Assignment-1/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/khanhifza/demo_jenkins.git # timeout=10
Fetching upstream changes from https://github.com/khanhifza/demo_jenkins.git
 > git --version # timeout=10
 > git --version # 'git version 2.43.0'
 > git fetch --tags --force --progress -- https://github.com/khanhifza/demo_jenkins.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision 5a5bad251a79442f3d87c4e2b7a899e71a396028 (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 5a5bad251a79442f3d87c4e2b7a899e71a396028 # timeout=10
Commit message: "Update file.txt"
 > git rev-list --no-walk 5a5bad251a79442f3d87c4e2b7a899e71a396028 # timeout=10
No emails were triggered.
[Assignment-1] $ /bin/bash /tmp/jenkins5573607191354693150.sh
Creating new branch: feature-branch
Switched to a new branch 'feature-branch'
Listing all branches:
* feature-branch
  main
  remotes/origin/main
Switching to main for merge
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
Merging feature-branch into main
Already up to date.
Rebasing feature-branch onto main
Switched to branch 'feature-branch'
Current branch feature-branch is up to date.
Deleting branch feature-branch
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
Deleted branch feature-branch (was 5a5bad2).
Email was triggered for: Always
Sending email for trigger: Always
Sending email to: shreekadam2222htb@gmail.com
[Slack Notifications] found #7 as previous completed, non-aborted build
[Slack Notifications] will send OnSuccessNotification because build matches and user preferences allow it
Finished: SUCCESS


```
---

### Jenkins Configuration

- Use **Pipeline script** (declarative or scripted).
- Integrate:
  - **Slack Notification Plugin**
 
    ![image](https://github.com/user-attachments/assets/cedc4d5a-32fb-4253-8771-7f243c19131a)
--- 

  - **Email Extension Plugin**
 
  ![image](https://github.com/user-attachments/assets/ffda616a-69e7-450b-b204-a4f244707a01)

- Wrap each Git operation in `try-catch` or `catchError` blocks for controlled error handling.

---

##  Part 2: Parameterized Job & Web Publishing

![image](https://github.com/user-attachments/assets/d2b435c1-b2e2-4b81-b2c7-0a38dbf6ee8f)


###  Job 1: Create File with Ninja Name

####  Objective

- Accept a **String parameter**: `<Ninja Name>`
![image](https://github.com/user-attachments/assets/57b3718a-a6a7-44b9-9b3d-937be1c577cf)

- Create a file `ninja.txt`
- Add content:
<Ninja Name> from DevOps Ninja

![image](https://github.com/user-attachments/assets/3b8e47fa-1a49-4708-9811-6aa7e0ecc113)

![image](https://github.com/user-attachments/assets/4fdafb35-e544-4912-a050-bb17e51fb661)




###  Job 2: Publish File to Web Server

![image](https://github.com/user-attachments/assets/d2b435c1-b2e2-4b81-b2c7-0a38dbf6ee8f)


####  Objective

- Trigger **automatically** after Job 1 completes successfully
- Read content from `ninja.txt`
- Publish it using a **web server** (e.g., Python HTTP server, Apache, Nginx)

  ![image](https://github.com/user-attachments/assets/4ae84830-3480-48d9-b246-d9024d41b33b)

  ![image](https://github.com/user-attachments/assets/888b6fe5-09ef-4b7a-a141-8677a7c1363b)



###  Triggering & Notifications

- Use `Build Triggers` → "Build after other projects are built"
- Or trigger via pipeline chaining
- On **failure** of any step: send Slack and Email notification
- On **success** of all steps: send Slack and Email success message

---

##  Prerequisites

- Jenkins instance with:
- Git Plugin
- Pipeline Plugin
- Slack Notification Plugin
- Email Extension Plugin
- Configured Git credentials
- Configured SMTP server for email
- Slack Webhook URL (Slack app setup)
- A simple web server (e.g., using `python3 -m http.server`)

---


