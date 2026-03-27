#  Assignment 3: Continuous Integration (CI) with Jenkins Freestyle Jobs

##  Objective

Implement CI checks for three microservice repositories using Jenkins Freestyle jobs. Store CI reports, manage artifacts, and send notifications on failures.

---

##  Repositories for CI Checks

| Language | Repository URL |
|----------|----------------|
| Python   | [attendance-api](https://github.com/OT-MICROSERVICES/attendance-api) |
| GoLang   | [employee-api](https://github.com/OT-MICROSERVICES/employee-api) |
| Java     | [spring3hibernate](https://github.com/opstree/spring3hibernate.git) |

---

##  Jenkins Job Structure

Create **3 Freestyle Jobs**:

1. `ci-python-attendance`
2. `ci-golang-employee`   
3. `ci-java-spring3hibernate`

   ![image](https://github.com/user-attachments/assets/85d8df26-22eb-45d7-95de-1612753e836c)


---

##  Configuration Steps (Common)

### 1. **Source Code Management**
- Select **Git**
- Add the corresponding repository URL
- Set branches to build (e.g., `*/main` or `*/master`)

![image](https://github.com/user-attachments/assets/4645644f-ff5a-48a3-8d87-44053fe48dd1)


### 2. **Build Triggers**
- Poll SCM or trigger via webhook

### 3. **Build Environment**
- Enable `Delete workspace before build starts`
- Inject necessary environment variables

![image](https://github.com/user-attachments/assets/88f73467-d12f-41d0-82bd-0ce9296c89f5)

---

## CI Checks to Implement

###  Generic Checks
- **Credential Scanning**: Use tools like `truffleHog`, `gitleaks`, or `detect-secrets`
- **Code Linting**:
  - Python: `flake8`, `black`
  - GoLang: `golint`, `go vet`
  - Java: `Checkstyle`, `PMD`

###  Unit Testing
- Python: `pytest`
- GoLang: `go test`
- Java: `JUnit` via Maven/Gradle

###  Code Coverage
- Python: `coverage.py`
- GoLang: `go test -cover`
- Java: `JaCoCo` or `Cobertura`

### Dependency Scanning
- Python: `safety`, `bandit`
- GoLang: `go list -m all`, `govulncheck`
- Java:`OWASP Dependency Check` , `SonarQube` 

---


![image](https://github.com/user-attachments/assets/8d73c66e-7f97-46d1-b261-84a8fb50ae2d)

![image](https://github.com/user-attachments/assets/6eea65fe-0e7b-4a4d-90c0-47024acd3e51)

