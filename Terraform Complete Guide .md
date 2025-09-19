# 🧩 Core Tools & Workflow

## 🔑 Tools We Use

| Terraform | AWS EC2 | AWS S3 | GitHub Actions |
|-----------|---------|--------|----------------|
## 🖼️ Core Tools We Use

| Terraform | AWS EC2 | AWS S3 | GitHub Actions |
|-----------|---------|--------|----------------|
| <img src="https://www.datocms-assets.com/2885/1620155116-brandhcterraformverticalcolor.svg" alt="Terraform" width="64"><br>**Terraform**<br><small>Infrastructure as Code (IaC)</small> | <img src="https://commons.wikimedia.org/wiki/Special:FilePath/AWS_Simple_Icons_Compute_Amazon_EC2_Instances.svg" alt="EC2" width="64"><br>**EC2**<br><small>Virtual servers (compute)</small> | <img src="https://commons.wikimedia.org/wiki/Special:FilePath/AWS_Simple_Icons_Storage_Amazon_S3.svg" alt="S3" width="64"><br>**S3**<br><small>Object storage</small> | <img src="https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png" alt="GitHub Actions" width="64"><br>**GitHub Actions**<br><small>CI/CD automation</small> |


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

