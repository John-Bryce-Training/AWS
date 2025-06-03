<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/8/89/John_bryce_logo.jpg" alt="Logo" width="259" height="107">
</p>  

| Last update | 26/03/2025  |
|-------------|-------------|

# Lab 02 - Getting Started with AWS IAM  
AWS IAM (Identity and Access Management) is a foundational service in AWS that allows you to manage users, groups, and permissions for secure access control.
It helps ensure that only the right people have the right access to the right resources.     
In this lab, you will learn how to create, configure, and manage IAM users and groups using the AWS Management Console.
###  Estimated time: 50 minutes
## Overview
**Task 1:** Create an IAM user with limited permissions
  
**Task 2:** Create a group and assign permissions to it
  
**Task 3:** Add the user to the group
 
**Task 4:** Sign in as the IAM user 
 
**Task 5:** Observe permission restrictions in action  

## Task 1: Create an IAM User

### In this task, you’ll create a new IAM user in your AWS account. IAM users are identities that represent people (like you or your teammates) who need to access AWS.

1. Log in to the AWS Management Console - https://eu-north-1.signin.aws.amazon.com/ using your AWS credentials.

3. In the top search bar, type `IAM` and click on **IAM**.

4. You’ll be taken to the IAM Dashboard. On the left menu, click **Users**.

5. Click the **Create user** button.

6. Under **User name**, type: `lab-student`.

7. Select the checkbox labeled **"Provide user access to the AWS Management Console – optional"**.

8. Uner **Console password** choose **Custom password** and type: `LabStudent123!`.

![My Image](media/Lab02/01.png)

9. Uncheck the **Users must create a new password at next sign-in - Recommended** and than select **Next**. This is the name of the new user.

10. Under **Permissions options**, check the box for **Add user to group** and than click **Next**.

12. On the review screen, confirm the details, then click **Create user**.

## Task 2: Create a Group and Attach Permissions  

### IAM groups let you manage permissions for multiple users at once. Instead of assigning policies to each user individually, you can assign them to a group, and then add users to that group.

1. From the IAM Dashboard, click **User groups** on the left menu.

2. Click the orange **Create group** button.

3. For the **User group name**, type: `EC2ReadOnlyGroup`. This group will have read-only access to AWS services.

4. On the **Attach permissions policies** screen, use the search bar to find `AmazonEC2ReadOnlyAccess`.

5. Check the box next to **AmazonEC2ReadOnlyAccess** — This policy allows viewing (but not changing) EC2-related settings and resources.

![My Image](media/Lab02/02.png)

6. Click **Next** (skip tags).

7. Click **Create user group**.

## Task 3: Add the User to the Group  

### Now we will add the user lab-student to the group we just created. This will give them the read-only EC2 permissions.  

1. Go to the **Users** section from the left menu.

2. Click on the username `lab-student`.

3. On the user's summary page, go to the **Groups** tab.

4. Click the **Add user to groups** button.

5. Check the box next to `AmazonEC2ReadOnlyAccess`.

6. Click **Add user to group(s)**.

## Task 4: Sign In as the IAM User

### In this step, you’ll sign in to the AWS Console as the IAM user you created and see what it looks like.

1. Return to the **IAM Dashboard** as the root user.

2. On the home screen, look for **Sign-in URL for IAM users in this account** under **AWS Account** box.

3. Click the **Copy link** button and paste the URL into a new browser tab or window.

>**Note:** This URL is unique to your AWS account. It takes you to the IAM login screen.

4. Sign in using the credentials:
   - **IAM username**: `lab-student`
   - **Password**: `LabStudent123!`

5. You will now be logged in as the IAM user.

## Task 5: Test Permission Restrictions

### Now we will see how the IAM policy actually works. Since `lab-student` has **read-only** permissions, they can see services but **not make any changes**.

1. While logged in as `lab-student`, open the AWS Console and search for **EC2**.

2. Click on the **EC2** service to open the dashboard.

3. Try clicking the **Launch Instance** button.

4. You should receive an error message saying you are not authorized.

## ✅ End of Lab

#### 🎉 Congratulations! You’ve completed the AWS IAM Lab.

You now know how to:
- Create IAM users and set passwords
- Create groups and attach permission policies
- Add users to groups
- Use the IAM sign-in portal
- Test real-world access control scenarios

### IAM is one of the most critical parts of AWS for managing access securely. Great job!
