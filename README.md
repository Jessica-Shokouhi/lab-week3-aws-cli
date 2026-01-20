---

# **lab-week3-aws-cli — AWS CLI Infrastructure Provisioning**

## **Group Members**
-Jessica 
-Cole
-Kyle

## **AWS Region**
us-west-2

---

# **Part 1 — SSH Key Import**

### **Key Used**
`bcitkey`

### **Public Key Import Command**
```
aws ec2 import-key-pair \
  --key-name "bcitkey" \
  --public-key-material fileb://~/.ssh/bcitkey.pub \
  --region us-west-2
```

### **Documentation Used**
Import Key Pair  
`https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/import-key-pair.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fimport-key-pair.html")

### **Notes**
- The key was generated locally using `ssh-keygen`
- Only the **public key** is uploaded to AWS  
- The key is required for Script 3 to SSH into the EC2 instance

---

# **Part 2 — S3 Bucket Creation**

### **Bucket Creation Command**
(Executed inside the script `create-bucket`)
```
aws s3api create-bucket \
  --bucket <your-unique-bucket-name> \
  --region us-west-2 \
  --create-bucket-configuration LocationConstraint=us-west-2
```

### **Documentation Used**
Create Bucket  
`https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/create-bucket.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fs3api%2Fcreate-bucket.html")

### **Notes**
- Bucket names must be globally unique  
- The `LocationConstraint` is required for any region other than `us-east-1`  
- Bucket deletion command:
```
aws s3api delete-bucket --bucket <your-bucket-name> --region us-west-2
```

---

# **Part 3 — VPC + EC2 Provisioning**

Scripts used:
- `create-vpc`
- `create-ec2`

### **What Script 3 Does**
- Creates a VPC  
- Creates a subnet  
- Creates a security group  
- Adds SSH (22) and HTTP (80) ingress rules  
- Launches a Debian EC2 instance  
- Uses the key pair imported in Part 1  
- Writes the public IP to a file named `instance_data`

### **AMI Used**
Debian AMI provided in the starter files via the `debian_ami` variable.

### **Instance Type**
`t3.micro`  
(Free-tier eligible in us-west-2)

### **SSH Command Used to Test**
```
ssh -i ~/.ssh/bcitkey admin@<public-ip>
```

### **Documentation Used**
Create VPC  
`https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-vpc.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fcreate-vpc.html")

Create Subnet  
`https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-subnet.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fcreate-subnet.html")

Create Security Group  
`https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-security-group.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fcreate-security-group.html")

Authorize Ingress  
`https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/authorize-security-group-ingress.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fauthorize-security-group-ingress.html")

Run Instances  
`https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/run-instances.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Frun-instances.html")

Describe Instances  
`https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-instances.html` [(awscli.amazonaws.com in Bing)](https://www.bing.com/search?q="https%3A%2F%2Fawscli.amazonaws.com%2Fv2%2Fdocumentation%2Fapi%2Flatest%2Freference%2Fec2%2Fdescribe-instances.html")

---

# **Testing the Infrastructure**

After running all scripts:

### **1. Run provisioning scripts**
```
./import-key
./create-bucket
./create-vpc
./create-ec2
```

### **2. Verify EC2 public IP**
```
cat instance_data
```

### **3. SSH into the instance**
```
ssh -i ~/.ssh/bcitkey admin@<public-ip>
```

### **4. Confirm instance is reachable**
Inside EC2:
```
uname -a
```

---

# **Repository Link**
Public GitHub repo URL:  
<your‑repo‑link‑here>

---


