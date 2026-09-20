
````md
# CI/CD — SDET Interview Notes
<img width="598" height="293" alt="image" src="https://github.com/user-attachments/assets/361d7dbb-4a61-46a6-a7b9-875d3d82ac4f" />
<img width="536" height="380" alt="image" src="https://github.com/user-attachments/assets/4c52c21b-ef72-4ca2-a0ac-681df5d59305" />
<img width="569" height="355" alt="image" src="https://github.com/user-attachments/assets/35d5a41e-eefc-49b0-b35b-0bc31ec6439a" />


## 1. Continuous Integration (CI)

### Definition

> Continuous Integration means developers frequently merge their code into a shared repository, and an automated pipeline builds and tests the code.

### CI Diagram

```text
Developer
   |
   | Code Change
   ↓
Git / GitHub
   |
   | Webhook
   ↓
Jenkins
   |
   ├── Checkout Code
   ↓
   ├── Build
   ↓
   ├── Unit Tests
   ↓
   ├── API Tests
   ↓
   ├── Automation Tests
   ↓
   └── Generate Report
            |
            ↓
        Test Result
````

### SDET Role in CI

As an SDET, I would typically handle:

* Automation test execution
* API/UI testing
* Regression testing
* Test data management
* Test reports
* Failure analysis
* Quality gates

---

# 2. Continuous Delivery

### Definition

> Continuous Delivery means keeping the application in a deployable state by automatically building, testing, and preparing validated code for release.

### Continuous Delivery Diagram

```text
Developer
    ↓
Git
    ↓
Jenkins
    ↓
Build
    ↓
Unit Tests
    ↓
SDET Automation
    ↓
Quality Gate
    ↓
Deploy to QA / Staging
    ↓
Smoke + Regression
    ↓
Production Ready
    ↓
Manual Release Approval
    ↓
Production
```

### Key Point

The software is always ready to be deployed, but production release may require manual approval.

---

# 3. Continuous Deployment

### Definition

> Continuous Deployment automatically deploys every change that successfully passes the required automated tests and quality gates into production.

### Continuous Deployment Diagram

```text
Developer
    ↓
Git
    ↓
Webhook
    ↓
Jenkins
    ↓
Build
    ↓
Unit Tests
    ↓
API/UI Automation
    ↓
Quality Gate
    ↓
QA / Staging
    ↓
Automated Validation
    ↓
Production
    ↓
Monitoring
```

### Key Point

There is generally no manual production approval in the deployment path.

---

# 4. CI vs Continuous Delivery vs Continuous Deployment

| Concept                    | Main Purpose                            | Production Deployment        |
| -------------------------- | --------------------------------------- | ---------------------------- |
| **Continuous Integration** | Build + test code frequently            | ❌ Not necessarily            |
| **Continuous Delivery**    | Keep software production-ready          | 🟡 Usually requires approval |
| **Continuous Deployment**  | Automatically release validated changes | ✅ Automatic                  |

---

# 5. Easy Way to Remember

```text
CI
 ↓
"Is the code working?"

Continuous Delivery
 ↓
"Is the application ready to release?"

Continuous Deployment
 ↓
"Automatically release it."
```

---

# 6. Complete CI/CD Pipeline — SDET Perspective

```text
                 DEVELOPMENT
                     |
                     ↓
              Developer writes code
                     |
                     ↓
                 Git Push
                     |
                     ↓
                  Webhook
                     |
                     ↓
                  Jenkins
                     |
        ┌────────────┴────────────┐
        ↓                         ↓
      BUILD                    QUALITY
        |                         |
        ↓                         ↓
   Compile Code             Unit Tests
        |                   API Tests
        ↓                   UI Tests
   Package App              Regression
        |                   Code Quality
        └────────────┬────────────┘
                     ↓
                Quality Gate
                     |
              ┌──────┴──────┐
              ↓             ↓
            FAIL           PASS
              ↓             ↓
          Fix Code       Deploy QA
                            |
                            ↓
                     Smoke Testing
                            |
                            ↓
                    Regression Testing
                            |
                            ↓
                     Deploy Staging
                            |
                            ↓
                    Final Validation
                            |
                    ┌───────┴───────┐
                    ↓               ↓
              Continuous       Continuous
               Delivery        Deployment
                    ↓               ↓
             Manual Approval    Automatic
                    ↓               ↓
                    └───────┬───────┘
                            ↓
                       Production
                            |
                            ↓
                      Monitoring
```

---

# 7. Interview-Ready Answer

> **"Continuous Integration is the practice of frequently integrating code into a shared repository and automatically building and testing it. Continuous Delivery extends CI by automatically preparing validated software for deployment, usually with a manual production approval. Continuous Deployment goes one step further by automatically deploying successfully validated changes to production. As an SDET, I contribute mainly through automated UI/API testing, regression testing, quality gates, test reporting, and failure analysis."**

```
```
