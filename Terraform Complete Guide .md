# 🧩 Core Tools & Workflow

## 🔑 Tools We Use

| Terraform | AWS EC2 | AWS S3 | GitHub Actions |
|-----------|---------|--------|----------------|
| ![Terraform](https://www.datocms-assets.com/2885/1620155116-brandhcterraformverticalcolor.svg) <br> **Infrastructure as Code (IaC)** – Automates AWS infra with reusable modules | ![EC2](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v14.0/dist/Compute/Amazon-EC2_64.svg) <br> **Elastic Compute Cloud** – Virtual servers to host applications | ![S3](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v14.0/dist/Storage/Amazon-Simple-Storage-Service-S3_Bucket_64.svg) <br> **Simple Storage Service** – Object storage for files, state, and backups | ![GitHub Actions](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png) <br> **CI/CD Engine** – Automates Terraform runs on every commit |

---

## ⚙️ Step-by-Step Flow

| Step | Tool | What Happens |
|------|------|--------------|
| 1️⃣ | ![GitHub](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png) **GitHub Repo** | Stores Terraform code & tracks changes |
| 2️⃣ | ![GitHub Actions](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png) **GitHub Actions** | Runs Terraform plan/apply automatically |
| 3️⃣ | ![Terraform](https://www.datocms-assets.com/2885/1620155116-brandhcterraformverticalcolor.svg) **Terraform** | Talks to AWS Provider (API) |
| 4️⃣ | ![EC2](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v14.0/dist/Compute/Amazon-EC2_64.svg) **EC2 Instance** | Creates VM with Public IP |
| 5️⃣ | ![S3](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v14.0/dist/Storage/Amazon-Simple-Storage-Service-S3_Bucket_64.svg) **S3 Bucket** | Creates bucket for storage & Terraform state |

---

## 🏗️ Visual Workflow (Diagram)

```mermaid
flowchart LR
    A["👨‍💻 Developer pushes code <br> to GitHub"] --> B["⚙️ GitHub Actions <br> runs Terraform"]
    B --> C["🛠️ Terraform <br> uses AWS Provider"]
    C --> D["🖥️ AWS EC2 <br> Virtual Server"]
    C --> E["📦 AWS S3 <br> Storage Bucket"]

    D --> F["🌍 Public IP Output"]
    E --> G["🔑 Bucket ARN Output"]

