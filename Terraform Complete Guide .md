# 🚀 Terraform AWS Project – EC2 + S3 Modules

![Terraform](https://img.shields.io/badge/IaC-Terraform-7B42BC?logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/Cloud-AWS-FF9900?logo=amazonaws&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/CI/CD-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)
![Status](https://img.shields.io/badge/Status-Production--Ready-brightgreen)

> 🎯 This repo is for **visual learners** who want to master **Terraform on AWS**.  
> If you don’t like boring study 📖 → Don’t worry, this guide is **100% visual & practical** 😎  

---

## 🖼️ Big Picture (What Happens Here)

Terraform → Talks to AWS → Builds **EC2 Instance** 🖥️ + **S3 Bucket** 📦

+-------------------+
| Terraform CLI | 🛠️
+-------------------+
|
v
+-------------------+
| AWS Provider | ☁️
+-------------------+
| |
v v
+------+ +--------+
| EC2 | | S3 |
| 🖥️ | | 📦 |
+------+ +--------+


✅ At the end → Terraform gives you  
- 🌍 **EC2 Public IP**  
- 🔑 **S3 Bucket ARN**  

---

## 🌍 Project Structure

```bash
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
├── provider.tf
├── versions.tf
├── terraform.tfvars
│
├── modules/
│   ├── ec2/        # EC2 module
│   └── s3/         # S3 module
│
├── env/
│   ├── dev.tfvars
│   ├── staging.tfvars
│   └── prod.tfvars
│
└── .terraform/     # Terraform’s memory

🏗️ Architecture Diagram
graph TD
    A[Terraform CLI 🛠️] --> B[AWS Provider ☁️]
    B --> C[EC2 Instance 🖥️]
    B --> D[S3 Bucket 📦]
    C --> E[Public IP 🌍]
    D --> F[Bucket ARN 🔑]

🧩 Modules = Lego Blocks

🧱 EC2 Module → Builds instance

🧱 S3 Module → Builds bucket

🧩 Together → Full infra setup
