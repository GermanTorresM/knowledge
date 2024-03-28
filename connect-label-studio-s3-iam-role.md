# How To Connect Label Studio to S3 via IAM Role


Crear policy

Sign in to the AWS Management Console and open the IAM console at https://console.aws.amazon.com/iam/.

In the navigation pane on the left, choose Policies.

Choose Create policy.

In the Policy editor section, choose the JSON option.

Type or paste a JSON policy document. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::<your_bucket_name>",
                "arn:aws:s3:::<your_bucket_name>/*"
            ]
        }
    ]
}
```

Resolve any security warnings, errors, or general warnings generated during policy validation, and then choose Next.

On the Review and create page, type a Policy Name and a Description (optional) for the policy that you are creating. Review Permissions defined in this policy to see the permissions that are granted by your policy.

(Optional) Add metadata to the policy by attaching tags as key-value pairs.

Name: SourcePolicy
Description: Label Studio Source Files

Choose Create policy to save your new policy.


Otra Policiy

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject"
            ],
            "Resource": [
                "arn:aws:s3:::<your_bucket_name>",
                "arn:aws:s3:::<your_bucket_name>/*"
            ]
        }
    ]
}
```

Name: TargetPolicy
Description: Label Studio Target Bucket


Create ROle

Custom Trust Policy

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal":{
                "AWS": [
                    "arn:aws:iam::4900990:user/rw_bucket"
                ]
            },
            "Action": "sts:AssumeRole",
            "Condition":{
                "StringEquals": {
                    "sts:xternalId": [
                        "<YOUR-ORG-ExternalId>"
                    ]
                }
            }
        }
    ]
}
```

Next

Select Policies

Next

Name: LSEByteRole

Create Role




