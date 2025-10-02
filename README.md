# assignment-2.15-Secret-Management-on-AWS

1. What is needed to authorize your EC2 to retrieve secrets from the AWS Secret Manager?

   To allow an EC2 instance to fetch secrets from AWS Secrets Manager, three things are required:
    IAM Role: Create a role for the EC2 instance to assume (instance profile).
    IAM Policy: Attach a specific policy that grants "secretsmanager:GetSecretValue" on the specific secret.
    Instance Profile: Associate the IAM role (via its profile) with the running EC2 instance.


2. Derive the IAM policy (i.e. JSON)?
   - Using the secret name prod/cart-service/credentials, derive a sensible ARN as the specific resource for access
_________________________________________________________________________________________________
   json


      {

      "Version": "2012-10-17",
   
      "Statement": [
   
      {
   
      "Effect": "Allow",
      
      "Action": [
      
         "secretsmanager:GetSecretValue",
         
         "secretsmanager:DescribeSecret"
         
      ],
      
      "Resource": "arn:aws:secretsmanager:ap-southeast-1:123456789012:secret:prod/cart-service/credentials-*"
      
      } 
   
      ]  
   
      }
__________________________________________________________________________________________________

*Specific Resource ARN

For the secret named prod/cart-service/credentials, the precise Amazon Resource Name (ARN) should be used to restrict access only to the specific secret.

A sensible and robust ARN for the policy resource is:

arn:aws:secretsmanager:region:account-id:secret:secret-name-<6_random_chars>

This format is required because AWS Secrets Manager automatically adds a unique random 6-character suffix to the secret name in the ARN. 
Using the wildcard (∗) after the hyphen ensures the policy works correctly, regardless of the random suffix.
