# A Step-by-Step Guide to Writing VPC Flow Logs to an S3 Bucket


## Prerequisites

Before you begin, ensure you have the following:

1. An active AWS account
2. A configured VPC with one or more subnets
3. An S3 bucket to store the VPC flow logs


## Step 1: Create an IAM Policy for VPC Flow Logs

To write VPC flow logs to an S3 bucket, you must create an IAM policy granting the necessary permissions.

1. Navigate to the AWS Management Console [https://aws.amazon.com/console/] and open the IAM service [https://console.aws.amazon.com/iam/].
2. Click **Policies** in the left navigation pane, then click the **Create policy** button.
3. Select the **JSON** tab and paste the following policy, replacing **your-bucket-name** with the name of your S3 bucket:

```
{
    "Version": "2023-04-05",
    "Statement": [
        {
            "Action": [
                "s3:PutObject",
                "s3:GetBucketAcl"
            ],
            "Effect": "Allow",
            "Resource": [
                "arn:aws:s3:::your-bucket-name/*"
            ]
        }
    ]
}
```

4. Click **Review policy** give your policy a name and description, and click **Create policy**.


## Step 2: Create an IAM Role for VPC Flow Logs

Next, create an IAM role that uses the policy you created in Step 1.

1. In the IAM service, click **Roles** in the left navigation pane and click **Create role**.
2. Select **VPC Flow Logs** as the service using this role, and click **Next: Permissions**.
3. Search for the policy you created in Step 1, select it, and click **Next: Tags**.
4. (Optional) Add any tags you’d like, and click **Next: Review**.
5. Provide a name and description for the role, then click **Create role**.
6. (Optional) For Trusted entity type, choose Custom trust policy. For Custom trust policy, replace **Principal: {}**, with the following, then select **Next**.

```
"Principal": {
   "Service": "vpc-flow-logs.amazonaws.com"
},
```

7. On the **Add Permissions page**, select the checkbox for the policy you created earlier in this procedure, then choose Next.
8. Now enter a name for your role and provide an optional description.
9. Finally, choose **Create role**.


## Step 3: Configure VPC Flow Logs to Write to S3 Bucket

Now that you have the necessary IAM role, you can configure VPC flow logs to write to your S3 bucket.

1. Open the VPC service in the AWS Management Console.
2. In the left navigation pane, click on **Your VPCs**.
3. Select the VPC you want to create flow logs for, then click on the **Actions** button and choose **Create flow log**.
4. In the **Filter** section, choose the type of traffic you want to capture (All, Accept, or Reject).
5. In the **Destination** section, choose **Send to an S3 bucket**.
6. Provide the ARN of your S3 bucket in the format **arn:aws:s3:::your-bucket-name**.
7. For the **IAM Role**, select the role you created in Step 2.
8. Click **Create flow log**.


## Step 4: View Your VPC Flow Log Records

With everything properly configured, you can now view your flow log records inside the s3 service. Remember, loading all of the logs into your S3 bucket may take up to ten minutes, so be patient.

1. Open the Amazon S3 console at https://console.aws.amazon.com/s3/.
2. Find the name of the bucket to open its corresponding details page.
3. Navigate to the folder with the log files. An example of what that path would look like is:

```
prefix/AWSLogs/account_id/vpcflowlogs/region/year/month/day/
```

4. Select the checkbox next to the file name and choose **Download**.