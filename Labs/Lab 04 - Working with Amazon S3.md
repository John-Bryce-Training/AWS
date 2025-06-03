<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/8/89/John_bryce_logo.jpg" alt="Logo" width="259" height="107">
</p>  

| Last update | 26/03/2025  |
|-------------|-------------|

# Lab 04 - Getting Started with Amazon S3  
Amazon S3 (Simple Storage Service) is a foundational object storage service in AWS that allows you to store and retrieve any amount of data, at any time, from anywhere on the web.  
It is designed for durability, availability, and scalability, and is commonly used for backup, data archiving, hosting static websites, and more.  
In this lab, you will learn how to create and configure an S3 bucket, upload and manage files, set permissions, and enable static website hosting.

## Estimated time: 45 minutes
## Overview
**Task 1:** Create an S3 bucket 
 
**Task 2:** Upload and manage files 
 
**Task 3:** Set permissions and test access 
 
**Task 4:** Enable static website hosting
  
**Task 5:** Enable versioning and test file overwrite recovery  

## Task 1: Create an S3 Bucket

#### In this task, you’ll create a new S3 bucket to store files. Buckets in S3 are like folders where you organize your files in the cloud.

1. Go to the [AWS Management Console](https://console.aws.amazon.com/) and sign in with your credentials.

2. In the top search bar, type `S3` and select the **S3** service.

3. Click the **Create bucket** button.

4. Configure the bucket with the following settings:
   - **Bucket name**: Must be globally unique (e.g., `jb-lab-s3-demo-[yourname]`)
   - Leave **Block all public access** checked for now.

5. Scroll to the bottom and click **Create bucket**.

## Task 2: Upload and Manage Files

#### In this task, you’ll upload a file to your S3 bucket and explore how objects are stored and viewed.

1. From the S3 Dashboard, click on the name of the bucket you created.

2. Click the **Upload** button.

3. Use **Add files** to choose a file from your computer (e.g., `.txt`, `.jpg`, `.pdf`).

4. Click **Upload** at the bottom of the page. Leave all other options at their default.

5. When the upload is complete, click on the file name to open its object details.

## Task 3: Set Permissions and Test Access

#### By default, files in S3 are private. In this task, you’ll update permissions so a file is publicly accessible by URL.

1. Inside your bucket, click on the name of the file you uploaded.

2. Click on the **Permissions** tab.

3. Scroll down to the **Access control list (ACL)** section and click **Edit**.

4. Under **Everyone (public access)**, check the box for **Read**.

5. Confirm and click **Save changes**.

6. Go to the **Properties** tab and copy the **Object URL**.

7. Open a new browser tab and paste the URL. If the file opens in the browser, your public access settings are working.

## Task 4: Enable Static Website Hosting

#### Amazon S3 can host static websites (like HTML pages) without the need for a traditional web server.

1. Go back to your bucket and click on the **Properties** tab.

2. Scroll down to the **Static website hosting** section and click **Edit**.

3. Set the following:
   - Enable the feature
   - **Index document**: `index.html`
   - (Optional) **Error document**: `error.html`

4. Click **Save changes**.

5. Now go to the **Objects** tab and click **Upload**.

6. Upload `index.html` file (you can download it from Lab 04 folder at the repository) and click **Upload** to finish.

7. Make these files public by following the same steps from Task 3.

8. Clicl **Close** and go back to **Properties** and copy the **Bucket website endpoint** at the end of the page.

9. Open the endpoint URL in a browser — you should see your website!

## Task 5: Enable Versioning and Test File Recovery

#### S3 Versioning allows you to preserve, retrieve, and restore every version of every object stored in a bucket.

1. Go to the **Properties** tab of your bucket.

2. Scroll down to **Bucket Versioning** and click **Edit**.

3. Select **Enable** and click **Save changes**.

4. Upload a file called `example.txt`.

5. Then, upload another file with the same name (`example.txt`) but different content. This creates a new version.

6. Click on the file name, then click on the **Versions** tab.

7. You’ll see both versions listed — with timestamps and unique version IDs.

8. You can select a version to download or restore it.

## ✅ End of Lab

#### 🎉 Congratulations! You’ve completed the Amazon S3 Lab.

Amazon S3 is a powerful and flexible tool that’s widely used in the cloud world. Well done!
