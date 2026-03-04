# Packer AWS Golden AMI Automation

Automated Amazon Machine Image (AMI) creation using HashiCorp Packer with the amazon-ebs builder for consistent and repeatable EC2 deployments.

---

## 🚀 What this project does

This template:

1. Launches a temporary EC2 instance
2. Installs required software (nginx / redis via provisioners)
3. Creates an AMI snapshot
4. Terminates the temporary instance

Result → **Reusable Golden AMI**

---

## 🧠 Why Packer

* Faster instance boot time
* No manual configuration
* Prevents configuration drift
* Consistent environments
* Ideal for Auto Scaling Groups

---

## ⚙️ Core Concepts

| Concept              | Purpose                           |
| -------------------- | --------------------------------- |
| Builder (amazon-ebs) | Creates AMI from EC2              |
| Provisioner          | Installs software (shell/ansible) |
| source block         | Defines base image + infra        |
| build block          | Defines actions on the instance   |
| Golden Image         | Pre-baked ready-to-use AMI        |

---

## 📦 Workflow

```bash
packer init .
packer fmt .
packer validate .
packer build .
```

---

## 🔐 AWS Authentication

Recommended:

```bash
aws configure
```

Provide:

* Access key
* Secret key
* Region
* json output

---

## 📝 Minimal Template Structure

```hcl
source "amazon-ebs" "ubuntu" {
  region        = "us-west-2"
  instance_type = "t3.micro"
  ssh_username  = "ubuntu"
  ami_name      = "my-ami-{{timestamp}}"
}

build {
  sources = ["source.amazon-ebs.ubuntu"]

  provisioner "shell" {
    inline = ["sudo apt update"]
  }
}
```

---

## 🎯 Interview Summary

**What does Packer do?**

> Creates a temporary VM, provisions software, snapshots it into an AMI, and deletes the VM to produce a reusable machine image.

**Packer vs Terraform**

* Packer → builds images
* Terraform → provisions infrastructure

---

## ✅ Hands-on Achievements

* Wrote HCL templates
* Installed required plugins
* Validated configuration
* Configured AWS credentials
* Built custom AMIs
* Installed nginx/redis using provisioners
* Cleaned up AMIs & snapshots to avoid cost

---

## 🛠 Tech Stack

* Packer
* AWS EC2 / AMI / EBS
* Shell Provisioners
* Git
