# AWS S3 Static Website Hosting

This project shows how to use Amazon S3 to host a static website. It guides you through the process of creating an S3 bucket, uploading the files for your website, configuring the bucket to host static websites, and evaluating the accessibility of the website.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [Setup Instructions](#setup-instructions)
    - [Prepare Your Website Files](#prepare-your-website-files)
    - [Create an S3 Bucket](#create-an-s3-bucket)
    - [Upload Website Files](#upload-website-files)
    - [Configure S3 Bucket for Static Website Hosting](#configure-s3-bucket-for-static-website-hosting)
    - [Set Permissions for Public Access](#set-permissions-for-public-access)
    - [Test the Static Website](#test-the-static-website)
4. [Optional: Custom Domain Setup](#optional-custom-domain-setup)
5. [Technologies Used](#technologies-used)
6. [Cleanup](#cleanup)

## Project Overview

In this project, a static website is hosted on an Amazon S3 bucket. It entails setting up a bucket for hosting static websites, uploading website files, and constructing the bucket. The project also outlines how to test the website and configure permissions to make it publicly available.

## Prerequisites

Before you begin, ensure the following:

- An AWS account.
- Basic knowledge of AWS S3 and static website hosting.
- Static website files ready to be uploaded (e.g., HTML, CSS, JavaScript).

## Setup Instructions

### **Prepare Your Website Files**

1. Organize your static website files, which should include:
    - `index.html` (the main landing page)
    - Other HTML files, CSS stylesheets, JavaScript, and any media files like images or videos.
   
2. Ensure that the main entry point of the website is named `index.html`.

### **Create an S3 Bucket**

1. Log in to the **AWS Management Console**.
2. Navigate to the **S3** service.
3. Click **Create bucket** and configure:
    - **Bucket Name**: Choose a globally unique name (e.g., `antique-cafe`).
    - **Region**: Select a region close to your target audience.
    - **Block Public Access settings**: Uncheck *"Block all public access"* to allow public access to your files.
    - **Bucket Versioning**: Leave it disabled (optional).
4. Click **Create Bucket**.

### **Upload Website Files**

1. Open your newly created bucket.
2. Click **Upload** > **Add files**.
3. Select all your static website files (e.g., `index.html`, CSS, JS files).
4. Click **Upload** to complete the process.

### **Configure S3 Bucket for Static Website Hosting**

1. In the bucket, go to the **Properties** tab.
2. Scroll to **Static website hosting** and click **Edit**.
3. Select **Enable**.
4. Specify the following:
    - **Index document**: `index.html`
    - **Error document**: `error.html` (optional if you have an error page).
5. Save changes.

### **Set Permissions for Public Access**

1. Go to the **Permissions** tab.
2. Scroll to **Bucket policy** and add the following policy to allow public access:

    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": "*",
          "Action": "s3:GetObject",
          "Resource": "arn:aws:s3:::antique-cafe/*"
        }
      ]
    }
    ```

3. Replace `antique-cafe` with your bucket's name.
4. Save the policy.

### **Test the Static Website**

1. Return to the **Properties** tab.
2. Locate the **Static website hosting** section.
3. Copy the **Website endpoint URL** (e.g., `http://antique-cafe.s3-website-us-east-1.amazonaws.com`).
4. Open the URL in your browser to verify that the website is live.

## Technologies Used

- **AWS S3**: For hosting the static website.
- **AWS Management Console**: For managing the S3 bucket and configuring settings.
- **DNS**: For setting up a custom domain (optional).

## Cleanup

To avoid unnecessary charges and clean up the resources you've created, follow these steps to delete everything:

### 1. Delete Website Files from S3
1. Navigate to the **S3** service in the AWS Management Console.
2. Open the S3 bucket you created for the website.
3. Select all files (such as `index.html`, CSS, JS files, etc.).
4. Click **Actions** > **Delete** and confirm the deletion.

### 2. Delete the S3 Bucket
1. After deleting all files, go to the **Properties** tab of the S3 bucket.
2. Scroll down to **Bucket settings** and click **Delete bucket**.
3. Type the bucket name to confirm the deletion and click **Confirm**.

### 3. Remove the Bucket Policy (Optional)
If you created a custom bucket policy, you can delete it:
1. Go to the **Permissions** tab.
2. Scroll down to **Bucket policy** and delete the policy.
3. Click **Save changes**.

### 5. Delete AWS Resources
Ensure no other resources (like EC2 instances or Route 53 hosted zones) are associated with this project to avoid unnecessary costs. You can delete any extra resources via the AWS Management Console.

---