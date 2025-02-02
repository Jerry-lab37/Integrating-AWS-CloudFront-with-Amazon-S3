# **Integrating AWS CloudFront with Amazon S3 for Optimized Content Delivery**  

## **Purpose**  
This guide provides a step-by-step approach to integrating **AWS CloudFront** with an **Amazon S3 bucket** for efficient content delivery. This setup enhances performance, security, and reduces latency by caching static assets at AWS edge locations worldwide.

---

## **Step 1: Create an S3 Bucket**  
1. Go to **AWS Console → S3**  
2. Click **Create Bucket**  
3. Set **Bucket Name** (e.g., `my-static-site`)  
4. Choose **Region**  
5. **Uncheck** "Block all public access" (CloudFront will manage access)  
6. Click **Create Bucket**  

---

## **Step 2: Upload Content to S3**  
1. Open the **S3 bucket**  
2. Click **Upload**  
3. Add `index.html` and `.jpg` files (samples provided below)  
4. Click **Upload**  

---

## **Step 3: Modify Bucket Policy (Public Read for CloudFront)**  
1. Go to **Permissions → Bucket Policy**  
2. Add the following policy (replace `BUCKET_NAME` with your actual bucket name):  

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::BUCKET_NAME/*"
    }
  ]
}
```
3.Click Save

##**Step 4: Create a CloudFront Distribution**
Go to AWS Console → CloudFront
Click Create Distribution
Under Origin, configure:
Origin Domain Name → Select your S3 bucket
Origin Access → Choose Origin Access Control (OAC) and Create new OAC
Click Create and Save policy changes
Configure Default Behavior:
Viewer Protocol Policy → Redirect HTTP to HTTPS
Allowed HTTP Methods → GET, HEAD
Configure Distribution Settings:
Price Class → Default
Alternate Domain Name (CNAME) → Add a custom domain (optional)
SSL Certificate → Use AWS default SSL or upload your own
Click Create Distribution
Wait for CloudFront Status to become Deployed

Step 5: Test the Setup
Copy the CloudFront Distribution URL
Open a browser and enter:

https://<CloudFront-Domain-Name>/index.html

3.Your static website or image should now load via CloudFront
Sample Files for Testing
Download Sample .jpg File
Download Sample Image

Sample index.html for S3
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CloudFront with S3</title>
</head>
<body>
    <h1>Welcome to CloudFront with S3</h1>
    <img src="https://<CloudFront-Domain-Name>/image.jpg" alt="Sample Image">
</body>
</html>

Note: Replace <CloudFront-Domain-Name> with your actual CloudFront distribution domain name.

Conclusion
Congratulations! 🎉 You have successfully integrated AWS CloudFront with Amazon S3 to optimize content delivery.

Key Benefits:
✅ Faster Performance – Content is cached at global edge locations
✅ Increased Security – Direct S3 access is restricted
✅ Lower Latency – Users access content from nearby AWS edge servers

This setup ensures a scalable, cost-effective, and secure content delivery solution using AWS. 🚀
