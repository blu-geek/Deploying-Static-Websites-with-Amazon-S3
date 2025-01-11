# Deploying-Static-Websites-with-Amazon-S3

As a Solutions Developer working with Valtara that needs to store and share large amounts of data, such as user-generated content like photos or videos. You are tasked with creating an S3 bucket to securely store these files, configure access policies so that users can upload and download their data, and then host a static website directly from the S3 bucket to display this content to the public.

<img width="707" alt="Screenshot 2025-01-11 at 13 26 59" src="https://github.com/user-attachments/assets/f0e17bcb-1914-41cd-a9af-5fc47fbb6a62" />

<img width="784" alt="Screenshot 2025-01-11 at 13 30 22" src="https://github.com/user-attachments/assets/061c8a59-af24-4ebf-8d24-ef22197523d7" />

# Summarized Architecture Flow: Hosting a Static Website on AWS

1. Client Request & DNS Lookup:
The client requests the website, triggering a DNS query.
Route 53 resolves the query and points to the CloudFront distribution.
2. SSL/TLS Encryption:
AWS Certificate Manager provisions an SSL/TLS certificate for HTTPS communication.
CloudFront fetches the certificate to enable secure, encrypted connections.
3. Content Delivery via CloudFront:
The request reaches CloudFront, which either serves cached content or fetches original files from the S3 bucket.
HTTPS communication is enforced using the SSL certificate.
4. Secure S3 Bucket Access:
CloudFront OAC (Origin Access Control) ensures the S3 bucket is private, accessible only to CloudFront.
This setup secures static assets (HTML, CSS, JS, images) stored in the S3 bucket.
5. Redirects with CloudFront Function:
The CloudFront Function performs HTTP redirects (e.g., from www to the root domain), enhancing user experience and SEO.
6. Content Served to Client:
Static web files stored in the private S3 bucket are delivered to the client through the CloudFront distribution.


# Activity Guide: Create an S3 Bucket, Upload Files,Configure Access and Host a Static Website

1. Set Up Prerequisites
AWS Account:
Ensure you have an active AWS account (Free Tier or Paid).
Download Required Files:
Download your the required files (index.html or error.html)  and unzip them if more for use in later steps

2. Create an S3 Bucket (Amazon S3)
- Access S3 Console:
Log in to the AWS Management Console, search for S3, and click Create Bucket.
- Name the Bucket:
Provide a unique bucket name and select a region close to your location for optimal performance.
- Configure Options:
Leave public access settings enabled by default and click Create Bucket.
Upload downloaded files to S3 bucket
- Manual Access (Optional):
Go to Permissions in the S3 Console, disable Block Public Access, and confirm changes.
Select the file, click Make Public via ACL, and confirm.
- Using Bucket Policy:
Navigate to Bucket Policy in the S3 Console and generate a policy using the Policy Generator:
Set Action to GetObject.
Add * in the Principal field.
Include the bucket ARN with /* appended.
Save the policy to enable automated public access for all objects.

4. Host a Static Website (Amazon S3)
Enable Website Hosting:
Under Properties, scroll to Static Website Hosting, click Edit, and enable it.
Specify index.html for the homepage and error.html for error handling.
Upload Website Files:
Upload index.html and error.html to the S3 bucket.
Test the Website:
Access the Bucket Website URL under Static Website Hosting and confirm the website is live.

5. Enable Versioning
Turn on Versioning:
Go to Properties, click Edit under Bucket Versioning, and enable it.
Upload New Versions:
Re-upload files (e.g., index.html) to create multiple versions.
Restore Versions:
Use Show Versions to view and restore older file versions.

6. Delete the S3 Bucket
Step 1: Empty the Bucket:
Disable versioning under Properties and confirm deletion of all versions.
Step 2: Delete the Bucket:
Return to the S3 Console, select the bucket, and click Delete.

7. Troubleshooting Common Issues
404 Not Found:
Ensure the object is public or the URL is correct.
Access Denied:
Verify permissions at the bucket or object level.
Incorrect Static Website Configuration:
Ensure index.html and error.html match the configurations.

