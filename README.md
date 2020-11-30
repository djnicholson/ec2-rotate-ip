# ec2-rotate-ip

This is a script that can be run periodically to change the public-facing IP on one or more EC2 instances.

## Pre-requisites

Ensure the following pre-requisites before running the script.

### Instances

For any instance that should have its public IP rotated:

1. Associate an Elastic IP with that instance.
2. Create a tag on the Elastic IP:
   - **rotate=1** _(key="rotate", value="1")_

### Environment

You will need Node.js installed and your environment configured with credentials to use the AWS Node.js SDK.

#### Required AWS permissions:

- `ec2:ReleaseAddress`
- `ec2:DescribeAddresses`
- `ec2:CreateTags`
- `ec2:AssociateAddress`
- `ec2:AllocateAddress`

#### Example IAM policy:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "ec2:ReleaseAddress",
                "ec2:DescribeAddresses",
                "ec2:CreateTags",
                "ec2:AssociateAddress",
                "ec2:AllocateAddress"
            ],
            "Resource": "*"
        }
    ]
}
```

#### Environment configuration instructions:

https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-credentials-node.html

## Instructions

Run the following command whenever you want to rotate IPs:

```
npx ec2-rotate-ip
```
