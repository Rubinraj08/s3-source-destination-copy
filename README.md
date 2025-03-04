# 🚀 AWS S3-Lambda Auto File Copy  

A **serverless AWS solution** that automatically copies files from one S3 bucket to another using **AWS Lambda** and **IAM policies**.  

---

## 🎯 **Project Overview**  

🔹 **Source Bucket**: Stores uploaded files.  
🔹 **Destination Bucket**: Receives copied files.  
🔹 **AWS Lambda**: Triggers on new file uploads and copies them.  
🔹 **IAM Policy**: Grants Lambda permissions to access S3.  

---

## 🛠️ **Tech Stack**  

- **AWS S3** (Simple Storage Service)  
- **AWS Lambda** (Python 3.x)  
- **IAM Role & Policy**  
- **Event-Driven Architecture**  

---

## 📌 **Step-by-Step Setup**  

### **1️⃣ Create S3 Buckets**  

1️⃣ **Go to the AWS S3 Console**  
2️⃣ Click `Create bucket`  
3️⃣ Enter a **unique** bucket name:  
   - **Source Bucket**: `source-bucket-yourname`  
   - **Destination Bucket**: `destination-bucket-yourname`  
4️⃣ Leave other settings as default and click `Create`  
5️⃣ Repeat for the **destination bucket**  

---

### **2️⃣ Create a Lambda Function**  

1️⃣ Open **AWS Lambda Console**  
2️⃣ Click `Create function` → Select `Author from scratch`  
3️⃣ Enter Function Name: **S3CopyFunction**  
4️⃣ Choose **Python 3.x** as the runtime  
5️⃣ Click `Create function`  

---

### **3️⃣ Add Environment Variable**  

1️⃣ In Lambda, go to `Configuration` → `Environment variables`  
2️⃣ Click `Edit`, then `Add environment variable`  
3️⃣ Enter:  
   - **Key**: `DEST_BUCKET`  
   - **Value**: `destination-bucket-yourname`  
4️⃣ Click `Save`  

---

### **4️⃣ Update IAM Permissions**  

1️⃣ In Lambda, go to `Configuration` → `Permissions`  
2️⃣ Click on the **IAM role name** to open IAM console  
3️⃣ Click `Add permissions` → `Attach policies`  
4️⃣ Click `Create inline policy`, then use this policy:  

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:PutObject"],
      "Resource": [
        "arn:aws:s3:::source-bucket-yourname/*",
        "arn:aws:s3:::destination-bucket-yourname/*"
      ]
    }
  ]
}
