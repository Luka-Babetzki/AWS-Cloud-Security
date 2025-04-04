# Cloud Security with AWS IAM
## Objective

The goal of this project was to implement AWS Identity and Access Management (IAM) to enhance cloud security. IAM allows for the secure control of access to AWS resources by managing authentication and authorisation within an AWS account.

### Skills Learned

- Understanding and implementing AWS IAM policies
- Using JSON to define granular access control rules
- Managing user permissions through IAM users and groups
- Utilising tags in EC2 instances for access management
- Testing and validating IAM policies in real-world scenarios

### Tools Used

- AWS IAM for identity and access management
- AWS EC2 for instance management
- AWS Management Console for resource visualisation
- JSON for defining IAM policies

## Steps

### 1. Tagging EC2 Instances

I used tags to efficiently identify and manage AWS resources.

- **Tag Key:** `Env`
- **Values:** `production`, `development`
- **Purpose:** Differentiate environments within the project.

![EC2 Instances](https://imgur.com/74OrbTi.png)

*Ref 1: ...*

![Overview](https://imgur.com/QcH1HWY.png)

*Ref 2: ...*


### 2. IAM Policy Creation

I created an IAM policy using JSON to manage access permissions:

- **Allows** EC2 actions on "development" resources
- **Permits** describe actions
- **Denies** tag creation/deletion

#### JSON Policy Structure:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ec2:*",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "ec2:ResourceTag/Env": "development"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:Describe*"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Deny",
            "Action": [
                "ec2:CreateTags",
                "ec2:DeleteTags"
            ],
            "Resource": "*"
        }
    ]
}
```
*Ref 3: ...*


![JSON Policy](https://imgur.com/gQd9B3r.png)

*Ref 4: ...*

### 3. Account Alias

Created an account alias for simplified AWS Management Console access.

- **New console sign-in URL:** https://nextwork-alias-lukababetzki.signin.aws.amazon.com/console

![Alias](https://imgur.com/1U9oLZm.png)

*Ref 5: ...*

### 4. IAM Users and User Groups

- Created IAM users representing human users and applications.
- Set up user groups for streamlined permission management.
- Attached the policy to a user group, allowing all members to inherit the permissions.

![User Creation](https://imgur.com/8jGIIgg.png)

*Ref 6: ...*
### 5. Testing IAM Policies

#### **Production Instance Test:**

- **Result:** Failed to stop
- **Error:** "You are not authorized to perform this operation."
- **Reason:** IAM policy restrictions.

![Denied](https://imgur.com/fObDxhz.png)

*Ref 7: ...*

#### **Development Instance Test:**

- **Result:** Successfully stopped
- **Reason:** IAM policy allowed changes to development resources.

![Success](https://imgur.com/WSLVumF.png)

*Ref 8: ...*


## Lessons Learned

- AWS IAM provides robust security mechanisms for resource access control.
- JSON policies allow granular permission control.
- Grouping users simplifies permissions management.
- Proper tagging enhances policy effectiveness.
- Testing policies is crucial to verify intended behaviour.

---

### Acknowledgements

Thank you to the amazing NextWork community for their guidance and support throughout this project.
