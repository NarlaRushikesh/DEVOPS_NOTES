# Terraform Setup with AWS (Hands-on Notes)

## 📌 Objective

Set up Terraform and AWS CLI to enable infrastructure provisioning using Terraform.

---

# 🧩 Step 1: Install Terraform

## 1. Download Terraform

* Go to: https://developer.hashicorp.com/terraform/downloads
* Download: **Windows AMD64**

## 2. Extract

* Extract the `.zip` file
* You will get:

```
terraform.exe
```

## 3. Move File

* Place `terraform.exe` in:

```
D:\devops\terraform
```

## 4. Add to PATH

* Open:

  * "Edit the system environment variables"
* Click:

  * Environment Variables → System Variables → Path → Edit → New
* Add:

```
D:\devops\terraform
```

## 5. Verify Installation

Open PowerShell:

```
terraform version
```

✅ Expected:

```
Terraform v1.x.x
```

---

# 🧩 Step 2: Install AWS CLI

## 1. Download

* https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
* Install AWS CLI v2

## 2. Verify

```
aws --version
```

✅ Expected:

```
aws-cli/2.x.x
```

---

# 🧩 Step 3: Create IAM User (AWS)

## 1. Go to AWS Console

* Service: IAM → Users → Create User

## 2. User Details

* User name:

```
terraform-user
```

* ❌ Do NOT enable:

```
AWS Management Console access
```

## 3. Permissions

* Select:

```
Attach policies directly
```

* Choose:

```
AdministratorAccess
```

## 4. Create User

---

# 🔑 Step 4: Generate Access Keys

## 1. Open User

* Go to:

```
IAM → Users → terraform-user
```

## 2. Security Credentials Tab

* Click:

```
Create Access Key
```

## 3. Select Use Case

```
CLI (Command Line Interface)
```

## 4. Save Credentials

You will get:

```
Access Key ID
Secret Access Key
```

⚠️ IMPORTANT:

* Save immediately
* Secret key will not be shown again

---

# 🧩 Step 5: Configure AWS CLI

Run:

```
aws configure
```

Enter:

```
AWS Access Key ID: <your-access-key>
AWS Secret Access Key: <your-secret-key>
Default region name: ap-south-1
Default output format: json
```

---

# 🌍 Region Selection

Recommended:

```
ap-south-1  (Mumbai)
```

Reason:

* Closest region (India)
* Lower latency
* Cost-efficient

---

# 🧩 Step 6: Verify AWS Configuration

## 1. Check Config

```
aws configure list
```

## 2. Test AWS Connection

```
aws ec2 describe-instances
```

✅ If no error → Setup successful

---

# 🧪 Step 7: Verify Terraform + AWS

## 1. Create File

Create `main.tf`:

```
provider "aws" {
  region = "ap-south-1"
}
```

## 2. Initialize Terraform

```
terraform init
```

✅ Expected:

* Provider plugins installed
* No errors

---

# 🎯 Final Outcome

You have successfully:

* Installed Terraform
* Installed AWS CLI
* Created IAM user
* Generated access keys
* Configured AWS CLI
* Connected Terraform with AWS

---

# 🚨 Security Best Practices

* Never share:

  * Access Key
  * Secret Key
* Rotate keys regularly
* Delete exposed keys immediately
* Use IAM roles in production

---

# 🚀 Next Step

Proceed to:
👉 Provision EC2 instance using Terraform
-----------------------------------------
