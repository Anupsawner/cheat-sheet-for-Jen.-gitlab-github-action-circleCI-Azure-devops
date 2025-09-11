# cheat-sheet-for-Jen.-gitlab-github-action-circleCI-Azure-devops
This is for those who thought they instantly learn all the things what is needed in CI/CD piplines and described abuot how the yml and different different files workflow and designed like guy understand easy inside work.

   //---------------------------------------------------------------------------------------------------------------------------------------------------------//

# 🚀 CI/CD Tools Cheat Sheet

A one-stop **visual guide** to understand Jenkins, GitHub Actions, CircleCI, and Azure DevOps.

---

## 📌 1. Jenkins

### 🔹 What is Jenkins?
- Open-source **automation server**.
- Mainly for **Continuous Integration (CI)** and **Continuous Delivery (CD)**.
- Highly flexible with plugins.

### 🔹 Workflow
```
[ Developer ]
     │ Commit
     ▼
[ Git Repo ]
     │ Webhook
     ▼
[ Jenkins ] ──► [ Jenkinsfile Pipeline ] ──► [ Build → Test → Deploy ]
```

### 🔹 Pipeline Example
```groovy
pipeline {
  agent any
  stages {
    stage('Build') { steps { echo 'Building...' } }
    stage('Test') { steps { echo 'Testing...' } }
    stage('Deploy') { steps { echo 'Deploying...' } }
  }
}
```

📝 **Notes:** Best for self-hosted & customizable workflows.

---

## 📌 2. GitHub Actions

### 🔹 What is it?
- **Built-in CI/CD** inside GitHub.
- Uses **YAML workflows** in `.github/workflows/`.

### 🔹 Workflow
```
[ Push / PR ]
     │ Event Trigger
     ▼
[ GitHub Actions ] ──► [ Runner (Linux/Windows/macOS) ]
     │
     ▼
[ Build → Test → Deploy ]
```

### 🔹 Pipeline Example
```yaml
name: CI Pipeline
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '16'
      - run: npm install
      - run: npm test
```

📝 **Notes:** Best for GitHub projects, easiest to start.

---

## 📌 3. CircleCI

### 🔹 What is it?
- Cloud-based **CI/CD** tool.
- Optimized for **Dockerized builds**.

### 🔹 Workflow
```
[ Developer ]
     │ Commit
     ▼
[ GitHub/Bitbucket Repo ]
     │
     ▼
[ CircleCI ] ──► [ .circleci/config.yml ] ──► [ Jobs → Workflows ]
```

### 🔹 Pipeline Example
```yaml
version: 2.1
jobs:
  build:
    docker:
      - image: circleci/node:16
    steps:
      - checkout
      - run: npm install
      - run: npm test
workflows:
  version: 2
  ci-workflow:
    jobs:
      - build
```

📝 **Notes:** Great for Docker/Kubernetes CI/CD.

---

## 📌 4. Azure DevOps

### 🔹 What is it?
- Microsoft’s **end-to-end DevOps platform**.
- Offers **Repos, Pipelines, Boards, Artifacts, Test Plans**.

### 🔹 Workflow
```
[ Developer ]
     │ Commit
     ▼
[ Azure Repos / GitHub ]
     │ Trigger
     ▼
[ Azure Pipeline (YAML/Classic) ] ──► [ Build + Test + Deploy ]
     ▼
[ Release Pipelines ]
```

### 🔹 Pipeline Example
```yaml
trigger:
  - main
pool:
  vmImage: 'ubuntu-latest'
steps:
  - task: NodeTool@0
    inputs:
      versionSpec: '16.x'
  - script: npm install
    displayName: 'Install dependencies'
  - script: npm test
    displayName: 'Run tests'
```

📝 **Notes:** Best for enterprises, integrates with Microsoft stack.

---

# 📊 Visual Comparison

| Feature       | Jenkins             | GitHub Actions       | CircleCI            | Azure DevOps             |
|---------------|---------------------|----------------------|---------------------|--------------------------|
| Hosting       | Self-hosted         | GitHub Cloud         | Cloud / Self-hosted | Cloud + On-premises      |
| Config Format | Groovy (Jenkinsfile)| YAML                 | YAML                | YAML / Classic GUI       |
| Ease of Use   | ⚡ Medium          | ⚡⚡ Very Easy      |⚡⚡ Easy            | ⚡ Medium               |
| Best For      | Custom setups       | GitHub projects      | Dockerized builds   | Enterprise DevOps        |

---

# 📌 Visual Workflow Summary

```
   Jenkins            GitHub Actions       CircleCI           Azure DevOps

  [ Commit ]          [ Commit ]           [ Commit ]         [ Commit ]
       │                  │                     │                 │
       ▼                  ▼                     ▼                 ▼
  Jenkinsfile         Workflow YAML        Config YAML     azure-pipelines.yml
       │                  │                     │                 │
       ▼                  ▼                     ▼                 ▼
  Build → Test →     Build → Test →        Build → Test →   Build → Test →
  Deploy (Custom)    Deploy (GitHub)       Deploy (Docker)  Deploy + Release
```

---

# 🌍 Real-World Web App Deployment Example

Let’s say you have a **Node.js web app**. Here’s how each tool handles CI/CD:

### ✅ Jenkins
```
1. Developer pushes code to GitHub.
2. Jenkins triggers via webhook.
3. Jenkinsfile runs: npm install → npm test → docker build → docker push.
4. Deploys container to AWS EC2 / Kubernetes.
```

### ✅ GitHub Actions
```
1. Push to `main` triggers workflow.
2. GitHub Actions runner installs Node.js.
3. Run tests + build Docker image.
4. Deploy to GitHub Pages / AWS / Azure.
```

### ✅ CircleCI
```
1. Push to repo with `.circleci/config.yml`.
2. CircleCI spins up Docker container.
3. npm install → npm test → docker build.
4. Deploys to Heroku / AWS ECS / GCP.
```

### ✅ Azure DevOps
```
1. Code in Azure Repos or GitHub.
2. Azure Pipeline builds + tests.
3. Creates Docker image → pushes to Azure Container Registry.
4. Release Pipeline deploys to Azure App Service or AKS.
```

---

# 🧠 Quick Notes
- **Jenkins** → Most flexible, but requires setup.
- **GitHub Actions** → Best for GitHub repos.
- **CircleCI** → Strong Docker & cloud CI/CD.
- **Azure DevOps** → Full enterprise solution.

---

✅ This sheet is designed for **instant understanding + real-world context** 📘
# 🚀 CI/CD Tools Cheat Sheet

![CI/CD Tools Comparison](./assets/cicd-tools.png)
