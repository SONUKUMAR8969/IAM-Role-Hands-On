# AWS IAM Role Management with S3 List Bucket Permissions for EC2

This guide will walk you through creating an IAM role that grants EC2 instances the permission to list S3 buckets. We will verify the functionality by checking the EC2 instance's ability to list S3 buckets before and after attaching the role.

## Steps

### 1. Create IAM Role

1. **Navigate to IAM Roles**
   - Sign in to the AWS Management Console and open the IAM console at https://console.aws.amazon.com/iam/.
   - In the navigation pane, choose **Roles**.
   - Click on **Create role**.

   ![Create IAM Role](https://github.com/user-attachments/assets/90184a4f-70a0-47af-ae6e-7297d542e2a1)

2. **Select AWS Service**
   - Under **Select trusted entity**, choose **AWS service**.
  
![Create IAM Role](https://github.com/user-attachments/assets/9b02be78-f9c2-4e35-8dba-f2c3df13eafb)

   - Select **EC2** from the list of services.
   - Click **Next**.

   ![Select AWS Service](https://github.com/user-attachments/assets/a2186daf-c1cb-47fb-879f-2d9d298bd3a2)

### 2. Attach Permissions Policy

1. **Attach Permissions**
   - In the **Attach permissions policies** section, search for `AmazonS3ReadOnlyAccess`.
   - Select the `AmazonS3ReadOnlyAccess` policy.
   - Click **Next**.

   ![Attach Permissions Policy](https://github.com/user-attachments/assets/70739c19-4060-443f-80bb-52d403ef5803)

### 3. Configure Role

1. **Name and Configure Role**
   - Enter `S3ListBucketRole` for the **Role name**.
   - Optionally, add a description and tags.
   - Click **Create role**.

   ![Configure Role](https://github.com/user-attachments/assets/58b24cc2-af92-4c26-9f7b-d0812733a3af)

### 4. Attach Role to EC2 Instance

1. **Checking if we can access s3 inside this instance**

   ![Configure Role](https://github.com/user-attachments/assets/9a00e9b3-d6ad-46b9-a4ba-9d873536c1af)

   we cannot access s3 as we have not configured role to this EC2.

2. **Modify IAM Role for EC2 Instance**
   - Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
   - In the navigation pane, choose **Instances**.
   - Select the instance you want to attach the role to.
   - Click on **Actions**, then **Security**, and then **Modify IAM role**.  

   ![Attach Role to EC2 Instance](https://github.com/user-attachments/assets/aaaaecad-3030-43e2-af5b-5cc5b06e4c9a)

   - Choose `S3ListBucketRole` from the **IAM role** list.
   - Click **Update IAM role**.

   ![Attach Role to EC2 Instance](https://github.com/user-attachments/assets/40ee3009-c85c-4e32-a253-2f179ffc5eec)

### 5. Verification

1. **Connect to EC2 Instance**
   - Connect to the EC2 instance using SSH or Session Manager.
   - Run the following command to attempt to list S3 buckets:
     

   ```bash
   aws s3 ls

![Attach Role to EC2 Instance](https://github.com/user-attachments/assets/c9f85674-a590-414c-8920-72282842b9ce)
