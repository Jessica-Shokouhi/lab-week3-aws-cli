# **lab-week3-aws-cli**

The lab includes three scripts that provision AWS infrastructure using the AWS CLI.
---

# **Group Members**

- Jessica
- Cole 
- Kyle 
---


---

## **Documentation Used**

All scripts were completed using the AWS CLI Command Reference:  
[https://awscli.amazonaws.com/v2/documentation/api/latest/index.html](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)

---

# **Script 1 — import-key**

**Goal:**  
Import an existing public key into AWS and name it **bcitkey**.

**Relevant AWS CLI documentation:**  
- Import key pair:  
  `https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/import-key-pair.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fimport-key-pair.html")

---

# **Script 2 — create-bucket**

**Goal:**  
Create an S3 bucket using the AWS CLI.

**Important notes:**  
- Bucket names must be globally unique  
- Must specify `--create-bucket-configuration LocationConstraint=us-west-2`  
- Bucket can be deleted with:  
  ```
  aws s3api delete-bucket --bucket <your-bucket-name> --region us-west-2
  ```

# **Script 3 — create-vpc & create-ec2**

**Goal:**  
Provision a VPC, subnet, security group, and EC2 instance using the AWS CLI.

### **Requirements:**
- Use the AMI provided by the `debian_ami` variable  
- Use the security group created earlier (`security_group_id`)  
- Use the key pair imported in Script 1 (`bcitkey`)  
- Write the EC2 public IP to a file named **instance_data**  
- Confirm SSH access using:  
  ```
  ssh -i ~/.ssh/bcitkey admin@<public-ip>
  ```

**Relevant AWS CLI documentation:**  
- Create VPC:  
  `https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-vpc.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fcreate-vpc.html")  
- Create subnet:  
  `https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-subnet.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fcreate-subnet.html")  
- Create security group:  
  `https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-security-group.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fcreate-security-group.html")  
- Authorize security group ingress:  
  `https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/authorize-security-group-ingress.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fauthorize-security-group-ingress.html")  
- Run instances:  
  `https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/run-instances.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Frun-instances.html")  
- Describe instance metadata:  
  `https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-instances.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fdescribe-instances.html")

---

# **Verification**

After provisioning:

<img width="2194" height="1052" alt="image" src="https://github.com/user-attachments/assets/4a7c702d-2031-427d-9cb2-810e2d0c86a3" />


---
