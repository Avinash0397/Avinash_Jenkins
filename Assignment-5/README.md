#  Assignment 5: Declarative Jenkins CI Pipeline for Java Project

##  Objective

Build a robust **Declarative Jenkins Pipeline** for a Java-based project that includes:
- Code checkout
- Parallel checks (Stability, Quality, Coverage)
- Conditional stage execution
- Approval before publishing
- Notifications on success/failure

---

##  Pipeline Structure

###  Stages Overview:
1. **Code Checkout**
2. **Parallel Stages**
   - Code Stability (e.g., Unit Testing)
   - Code Quality (e.g., SonarQube)
   - Code Coverage (e.g., Jacoco)
3. **Generate Reports**
4. **Approval Gate (Manual Input)**
5. **Artifact Publishing**
6. **Notifications (Slack + Email)**

![image](https://github.com/user-attachments/assets/8bc1212a-21a8-43f8-8ec8-e69e4de025f5)

![image](https://github.com/user-attachments/assets/c03de41f-87aa-4f22-a48d-e4f0cd3aa78b)


---

## Tools Required

- Jenkins (2.300+)
- Maven or Gradle
- SonarQube plugin
- Jacoco plugin
- Email and Slack plugins
- GitHub repo with Java code

---

## Sample Directory Structure
![image](https://github.com/user-attachments/assets/c03de41f-87aa-4f22-a48d-e4f0cd3aa78b)

![image](https://github.com/user-attachments/assets/ce98a19c-66a2-47b0-81e2-261fe4329e9c)


