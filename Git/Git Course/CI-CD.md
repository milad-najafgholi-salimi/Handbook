**CI/CD is the automation of:**

1. **checking your code every time it changes** (CI)
    
2. **delivering it safely to users** (CD)
    

So humans write code → machines test, build, and ship it.

---
## CI — Continuous Integration

### What CI means

Every time you:
```
git push
```
CI automatically:

- builds your code
    
- runs tests
    
- checks formatting / lint
    
- fails fast if something’s broken
    

### Why CI exists

Before CI:

> “Works on my machine”

After CI:

> “If CI is green, it’s probably safe.”

---
Typical CI pipeline
```
push → build → test → lint → report
```
Example:

- Python code pushed
    
- CI spins up a clean machine
    
- installs dependencies
    
- runs `pytest`
    
- runs `ruff` or `flake8`
    
- reports success or failure

---
## CD — Continuous Delivery / Deployment

### Two meanings (important!)

### 1️⃣ Continuous **Delivery**

- Code is always **ready** to deploy
    
- Deployment is manual (click a button)
    

### 2️⃣ Continuous **Deployment**

- Code is deployed **automatically**
    
- No human approval
    

Most teams start with **Delivery**, not Deployment.

---
### Typical CD pipeline
```
CI passed → build artifact → deploy
```
Deployment could mean:

- upload to server
    
- push Docker image
    
- publish package
    
- update cloud service
    

---

## CI/CD together (full flow)
```
commit
  ↓
push
  ↓
CI (tests, lint, build)
  ↓
CD (deploy / release)
```
If CI fails → CD never runs.  
Safety first.

---
## Why CI/CD is a big deal

### Without CI/CD

- manual testing
    
- fear of deploying
    
- bugs sneak in
    
- releases are stressful
    

### With CI/CD

- fast feedback
    
- consistent quality
    
- confidence to change things
    
- smaller, safer releases
    

This is **how modern software scales**.

---

## Common CI/CD tools

### CI tools

- **GitHub Actions** (most popular now)
    
- GitLab CI
    
- CircleCI
    
- Jenkins (old but powerful)
    

### CD tools

- GitHub Actions
    
- ArgoCD
    
- Spinnaker
    
- Terraform (infra side)
    

Often: **same tool does both**.

---
## Example: simple CI for Python (GitHub Actions)
```
name: CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.11"
      - run: pip install -r requirements.txt
      - run: pytest
```
This runs on **every push**.  
No excuses, no “forgot to test”.

---
## CI/CD concepts you should know

### 🔹 Pipeline

A series of automated steps.

### 🔹 Job

One unit of work (e.g., “run tests”).

### 🔹 Stage

A group of jobs (e.g., “test stage”).

### 🔹 Artifact

Output of the pipeline (build, package, image).

### 🔹 Environment

Where code runs (dev / staging / prod).

---
## CI/CD best practices (real-world)

- Pipelines must be **fast**
    
- Tests must be **deterministic**
    
- Secrets never in repo
    
- Fail early
    
- Same pipeline for everyone

---
## CI/CD for your _personal AI companion project_

You don’t need fancy stuff. But CI helps a lot.

### What CI should do for you

- run tests
    
- check formatting
    
- prevent broken commits
    

### What CD _could_ do later

- package app
    
- deploy local service
    
- build Docker image
    

Even solo projects benefit from CI.

