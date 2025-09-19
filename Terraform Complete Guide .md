# 📸 Terraform in Action (Screenshots)

Even if you don’t read code, just **look at these screenshots** 👇

---

## 🔍 Terraform Plan (Preview)
This shows what AWS resources **will be created**.

![Terraform Plan Screenshot](./assets/terraform-plan.png)

---

## 🚀 Terraform Apply (Execution)
This is Terraform **building the infra** on AWS.

![Terraform Apply Screenshot](./assets/terraform-apply.png)

---

## 📤 Terraform Output (Results)
At the end, Terraform gives us **useful values** like Public IP & S3 ARN.

![Terraform Output Screenshot](./assets/terraform-output.png)

---

# 📂 Where to Put Screenshots?

- Make a folder in your repo:  
assets/
├── terraform-plan.png
├── terraform-apply.png
└── terraform-output.png

yaml
Copy code

- Then commit images along with your README.

---

# 🎯 Example Outputs You’ll See

```bash
Apply complete! Resources: 2 added, 0 changed, 0 destroyed.

Outputs:

ec2_public_ip = "18.210.55.23"
s3_bucket_arn = "arn:aws:s3:::my-terraform-demo-bucket-123"
