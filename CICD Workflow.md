# cheat-sheet-for-Jen.-gitlab-github-action-circleCI-Azure-devops
This is for those who thought they instantly learn all the things what is needed in CI/CD piplines and described abuot how the yml and different different files workflow and designed like guy understand easy inside work.

   //---------------------------------------------------------------------------------------------------------------------------------------------------------//

# 🚀 CI/CD Tools Cheat Sheet

A one-stop **visual guide** to understand Jenkins, GitHub Actions, CircleCI, and Azure DevOps.

# 🚀 CI/CD Tools Comparison Cheat Sheet

## 🔧 Overview

| Jenkins | GitHub Actions | CircleCI | Azure DevOps |
|---------|----------------|----------|--------------|
| ![Jenkins](https://www.jenkins.io/images/logos/jenkins/jenkins.png) <br> Open-source automation server | ![GitHub Actions](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png) <br> Integrated CI/CD service by GitHub | ![CircleCI](https://circleci.com/favicon.ico) <br> Cloud-based CI/CD platform | ![Azure DevOps](https://learn.microsoft.com/en-us/media/logos/logo-ms-social.png) <br> Microsoft's CI/CD service |

---

## 📜 Pipeline Configurations

| Jenkins | GitHub Actions | CircleCI | Azure DevOps |
|---------|----------------|----------|--------------|
| ```groovy<br>pipeline {<br>  stages { }<br>}<br>``` | ```yaml<br>name: CI<br>on:<br>  push:<br>    branches:<br>      - main<br>jobs:<br>  build:<br>    runs-on: ubuntu-latest<br>    steps:<br>      - run: npm install<br>``` | ```yaml<br>version: 2.1<br>jobs:<br>  build:<br>    steps:<br>      - checkout<br>      - run: npm install<br>      - run: npm test<br>``` | ```yaml<br>trigger:<br>  - main<br>pool:<br>  vmImage: 'ubuntu-latest'<br>steps:<br>  - script: npm install<br>  - script: npm test<br>``` |

---

## 🔄 Workflow Examples (ASCII Visuals)

### 🟢 Jenkins


[ Code Commit ]
│
▼
[ Build ]
│
▼
[ Test ]
│
▼
[ Deploy ]
│
▼
[ AWS ]

---

### 🔵 GitHub Actions

[ Code Commit / Push ]
│
▼
[ Workflow Trigger ]
│
▼
[ Run Tests ]
│
▼
[ Deploy ]
│
▼
[ AWS ]


---

### 🟠 CircleCI

[ Node.js App ]
│
▼
[ Build ]
│
▼
[ Test ]
│
▼
[ Deploy ]
│
▼
[ AWS ]


---

### 🟣 Azure DevOps

[ Node.js App ]
│
▼
[ Build ]
│
▼
[ Docker Image ]
│
▼
[ Deploy ]
│
▼
[ AWS ]


---

## ✅ Summary Table

| Tool            | Trigger                     | Config File               | Where Jobs Run               | Pipeline Type                     |
|-----------------|-----------------------------|---------------------------|------------------------------|-----------------------------------|
| Jenkins         | Webhook / Poll SCM          | `Jenkinsfile` (Groovy)    | Jenkins agents (self-hosted) | Stages (Build, Test, Deploy)      |
| GitHub Actions  | Push, PR, schedule, manual  | `.github/workflows/*.yml` | GitHub-hosted runners        | Jobs + Steps (YAML)               |
| CircleCI        | Push to GitHub/Bitbucket    | `.circleci/config.yml`    | Docker/VM environments       | Jobs + Workflows                  |
| Azure DevOps    | Push, PR, schedule, manual  | `azure-pipelines.yml`     | Microsoft/Self-hosted agents | Build Pipeline + Release Pipeline |

---

✅ This cheat sheet now has **configs, workflows, ASCII diagrams, and a summary table** for instant understanding.

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


# 🚀 CI/CD Tools Comparison Cheat Sheet
