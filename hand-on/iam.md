# IAM

## Create IAM groups

Use these AWS CLI commands to create the required IAM groups:

```bash
aws iam create-group --group-name Developers-Group
aws iam create-group --group-name DevOps-Group
aws iam create-group --group-name DataAnalytics-Group
aws iam create-group --group-name Management-Group
```


## Create IAM users
```bash
# Development Team
echo "Creating Development Team users..."
aws iam create-user --user-name john.developer --path /developers/
aws iam create-login-profile --user-name john.developer --password "TempPassword123!" --password-reset-required
aws iam add-user-to-group --user-name john.developer --group-name Developers-Group

# Or attach policies directly if not using group
# aws iam attach-user-policy --user-name john.developer --policy-arn arn:aws:iam::aws:policy/AmazonEC2ReadOnlyAccess
# aws iam attach-user-policy --user-name john.developer --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess


# DevOps Team
echo "Creating DevOps Team users..."
aws iam create-user --user-name mike.devops --path /devops/
aws iam create-login-profile --user-name mike.devops --password "TempPassword123!" --password-reset-required
aws iam add-user-to-group --user-name mike.devops --group-name DevOps-Group

# Analytics Team
echo "Creating Analytics Team user..."
aws iam create-user --user-name alex.analyst --path /analytics/
aws iam create-login-profile --user-name alex.analyst --password "TempPassword123!" --password-reset-required
aws iam add-user-to-group --user-name alex.analyst --group-name DataAnalytics-Group

# Management Team
echo "Creating Management Team user..."
aws iam create-user --user-name ceo.manager --path /management/
aws iam create-login-profile --user-name ceo.manager --password "TempPassword123!" --password-reset-required
aws iam add-user-to-group --user-name ceo.manager --group-name Management-Group
```

## Roles

### Create trust policy file
echo '{
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Principal": {"AWS": "arn:aws:iam::YOUR-ACCOUNT-ID:root"},
        "Action": "sts:AssumeRole"
    }]
}' > trust-policy.json

### Create role
aws iam create-role --role-name DeveloperRole --assume-role-policy-document file://trust-policy.json

### Attach permissions
aws iam attach-role-policy --role-name DeveloperRole --policy-arn arn:aws:iam::aws:policy/AmazonEC2ReadOnlyAccess
aws iam attach-role-policy --role-name DeveloperRole --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess

### Give group permission to assume role:
echo '{
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": "sts:AssumeRole",
        "Resource": "arn:aws:iam::YOUR-ACCOUNT-ID:role/DeveloperRole"
    }]
}' > assume-role-policy.json

aws iam put-group-policy --group-name Developers-Group --policy-name AssumeRole --policy-document file://assume-role-policy.json



## Create DeveloperPolicy

Create a policy document file named `DeveloperPolicy.json` with this content:

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Action": [
				"ec2:RunInstances",
				"ec2:TerminateInstances",
				"ec2:DescribeInstances",
				"ec2:StartInstances",
				"ec2:StopInstances"
			],
			"Resource": "*",
			"Condition": {
				"StringEquals": {
					"ec2:InstanceType": ["t2.micro", "t2.small", "t3.micro"]
				}
			}
		},
		{
			"Effect": "Allow",
			"Action": [
				"s3:GetObject",
				"s3:PutObject",
				"s3:DeleteObject"
			],
			"Resource": "arn:aws:s3:::dev-*/*"
		}
	]
}
```

Create the IAM policy with AWS CLI:

```bash
aws iam create-policy --policy-name DeveloperPolicy --policy-document file://DeveloperPolicy.json
```



