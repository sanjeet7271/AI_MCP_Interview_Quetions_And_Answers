# Deployment Strategies — SDET Interview Notes

## What is a Deployment Strategy?

A **deployment strategy** defines how a new version of an application is released and moved into an environment such as QA, staging, or production.

For an SDET, the focus is on:

- Smoke testing
- Regression testing
- API/UI validation
- Performance validation
- Monitoring logs and metrics
- Rollback validation

---

# Common Deployment Strategies

| Strategy | Simple Meaning | SDET Focus |
|---|---|---|
| **1. Big Bang** | Deploy everything at once | Full regression testing |
| **2. Rolling Deployment** | Deploy gradually across servers/instances | Validate each batch |
| **3. Blue-Green** | Two environments: current and new | Test new environment, then switch traffic |
| **4. Canary** | Release to a small percentage of users first | Monitor errors and performance |
| **5. A/B Deployment** | Different users receive different versions | Compare behavior/results |
| **6. Recreate** | Stop old version → deploy new version | Validate after restart |
| **7. Shadow Deployment** | New version receives copied traffic without affecting users | Compare results safely |

---

# 1. Big Bang Deployment

The entire application is deployed at once.

```text
Old Version
     ↓
Stop / Replace
     ↓
New Version
     ↓
Production
```

### SDET Focus

- Complete regression testing
- Smoke testing
- API testing
- UI validation
- Rollback testing

### Risk

A problem can affect all users because the new version is released at once.

---

# 2. Blue-Green Deployment

Two production-like environments are maintained:

- **Blue** → Current production version
- **Green** → New version

```text
              Load Balancer
                    |
          ┌─────────┴─────────┐
          ↓                   ↓
       BLUE                 GREEN
    Current Version       New Version
          |                   |
       Users              Testing
                              ↓
                       Validation Passed
                              ↓
                       Switch Traffic
```

### SDET Example

Run:

```text
Smoke Tests
     ↓
API Tests
     ↓
UI Tests
     ↓
Regression Tests
     ↓
Validation
     ↓
Switch Traffic
```

If Green fails validation, traffic can remain on Blue.

---

# 3. Canary Deployment

The new version is initially released to a small percentage of users.

```text
Users
  |
  ↓
Load Balancer
  |
  ├── 95% → Old Version
  |
  └── 5%  → New Version
              ↓
          Monitor Tests
          Error Rate
          Performance
              ↓
       Gradually Increase
       5% → 25% → 50% → 100%
```

### SDET Focus

Monitor:

- Functional failures
- API errors
- Response time
- CPU/memory
- Application logs
- Error rate

---

# 4. Rolling Deployment

The new version is deployed to servers gradually.

```text
Servers:  S1  S2  S3  S4

Step 1:   NEW OLD OLD OLD
Step 2:   NEW NEW OLD OLD
Step 3:   NEW NEW NEW OLD
Step 4:   NEW NEW NEW NEW
```

### SDET Focus

After each batch:

```text
Deploy
  ↓
Smoke Test
  ↓
Health Check
  ↓
Monitor Logs
  ↓
Continue / Rollback
```

### Benefit

It reduces downtime and deployment risk compared with deploying everything at once.

---

# 5. A/B Deployment

Two versions are made available to different groups of users.

```text
                Users
                  |
             Load Balancer
              /          \
             ↓            ↓
        Version A      Version B
             |            |
         Group A       Group B
```

### SDET Focus

Compare:

- Functional behavior
- API responses
- User flows
- Performance
- Error rates

---

# 6. Recreate Deployment

The old version is stopped before the new version is deployed.

```text
Old Version
     ↓
Stop
     ↓
Deploy New Version
     ↓
Start Application
     ↓
Smoke Testing
```

### Disadvantage

There can be downtime while the old version is stopped and the new version starts.

---

# 7. Shadow Deployment

The new version receives a copy of real traffic, but its responses are not returned to users.

```text
                  Users
                    |
               Production
                    |
              ┌─────┴─────┐
              ↓           ↓
          Old Version   New Version
              ↓           ↓
          User Response  Compare
                        Results
```

### SDET Focus

Compare:

- Response behavior
- Performance
- Errors
- Business logic
- Database impact

The new version can be tested with realistic traffic without directly affecting users.

---

# Deployment Strategy Comparison

| Strategy | Traffic Approach | Downtime | Risk | Main Purpose |
|---|---|---:|---:|---|
| **Big Bang** | 100% new version | Possible | Higher | Simple full deployment |
| **Rolling** | Gradual server batches | Low/None | Medium | Gradual rollout |
| **Blue-Green** | Switch between environments | Very low | Lower | Fast switch/rollback |
| **Canary** | Small % → 100% | Low/None | Lower | Gradual production validation |
| **A/B** | Split by user/group | Low/None | Medium | Compare versions |
| **Recreate** | Stop → replace | Yes | Medium | Simple replacement |
| **Shadow** | Duplicate traffic | None | Low for users | Validate new version safely |

---

# Deployment vs Release

This is an important interview question.

> **Deployment = Putting the code into an environment.**

> **Release = Making the functionality available to users.**

### Example

Code can be deployed to production but hidden behind a **feature flag**.

```text
Code
 ↓
Deploy to Production
 ↓
Feature Flag = OFF
 ↓
Users don't see the feature
```

Later:

```text
Feature Flag = ON
 ↓
Feature becomes available
 ↓
Release
```

---

# SDET Responsibilities During Deployment

As an SDET, I would typically perform:

1. **Pre-deployment validation**
2. Smoke testing
3. API testing
4. UI testing
5. Regression testing
6. Database validation
7. Log validation
8. Health-check validation
9. Performance monitoring
10. Post-deployment validation
11. Rollback validation

---

# Interview-Ready Answer

> **"Common deployment strategies include Big Bang, Rolling, Blue-Green, Canary, A/B, Recreate, and Shadow deployment. As an SDET, I focus on smoke testing, regression testing, API/UI validation, performance validation, monitoring logs and metrics, and rollback validation depending on the deployment strategy."**

## One-Line Definitions

```text
Big Bang   → Deploy everything at once.

Rolling    → Deploy the new version gradually across servers.

Blue-Green → Maintain two environments and switch traffic
             from the old environment to the new one.

Canary     → Release the new version to a small percentage
             of users and gradually increase traffic.

A/B        → Different user groups receive different versions.

Recreate   → Stop the old version and deploy the new version.

Shadow     → Send a copy of real traffic to the new version
             without affecting users.
```
