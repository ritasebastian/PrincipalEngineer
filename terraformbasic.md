

## 🧱 **Terraform Basics**

| Command | Purpose |
|--------|---------|
| `terraform init` | Initialize working directory |
| `terraform plan` | Show changes before applying |
| `terraform apply` | Apply infrastructure changes |
| `terraform destroy` | Delete all managed infrastructure |
| `terraform fmt` | Format code |
| `terraform validate` | Check config syntax |
| `terraform output` | Show outputs from state file |
| `terraform taint` | Force resource to be destroyed and recreated |
| `terraform state list` | List resources in state file |

---

## 📁 **Project Structure**

```
main.tf       → Main resources  
variables.tf  → Input variables  
outputs.tf    → Output values  
provider.tf   → Cloud provider config  
terraform.tfvars → Variable values  
```

---

## 🔌 **Provider Example (AWS)**

```hcl
provider "aws" {
  region = "us-east-1"
}
```

---

## 💡 **Resource Example (EC2)**

```hcl
resource "aws_instance" "my_ec2" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "example-instance"
  }
}
```

---

## 📦 **Variable Example**

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

Use it like:
```hcl
instance_type = var.instance_type
```

---

## 🧪 **Output Example**

```hcl
output "instance_ip" {
  value = aws_instance.my_ec2.public_ip
}
```

---

## 🧾 **Data Source Example**

```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]
  filter {
    name   = "name"
    values = ["ubuntu/images/*"]
  }
}
```

---

## 🔐 **Backend Example (S3 + DynamoDB)**

```hcl
terraform {
  backend "s3" {
    bucket         = "my-tf-state"
    key            = "prod/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

---

## 🛡 **State Locking & Remote State**

| Feature | Tool |
|--------|------|
| Locking | DynamoDB table |
| Remote state storage | S3, GCS, Azure blob, Terraform Cloud |

---

## 🧠 **Modules Example**

```hcl
module "vpc" {
  source = "terraform-aws-modules/vpc/aws"
  name   = "my-vpc"
  cidr   = "10.0.0.0/16"
}
```

---

## 🔄 **Looping & Conditions**

**for_each**:
```hcl
resource "aws_s3_bucket" "buckets" {
  for_each = toset(["dev", "prod"])
  bucket   = "myapp-${each.key}"
}
```

**count**:
```hcl
resource "aws_instance" "web" {
  count = 3
}
```

---

## 🔗 **Useful Functions**

| Function | Purpose |
|---------|---------|
| `join()`, `split()` | String manipulation |
| `lookup()`, `map()` | Maps |
| `file()` | Read file content |
| `element()` | Pick index from list |
| `length()` | Get list size |
| `merge()` | Merge maps |

---

## 🔍 **Debugging Tips**

- Run `TF_LOG=DEBUG terraform apply` to see debug logs
- Use `terraform console` to interactively test expressions

---

## 🧾 Terraform Cloud/Enterprise

| Feature | Description |
|--------|-------------|
| Workspaces | Separate environments |
| Version control integration | GitHub, GitLab |
| Remote runs | Secure state management & collaboration |
| Sentinel | Policy-as-code support |

---

