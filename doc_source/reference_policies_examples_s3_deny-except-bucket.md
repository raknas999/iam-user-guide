# Amazon S3: Limits Managing to a Specific S3 Bucket<a name="reference_policies_examples_s3_deny-except-bucket"></a>

This example shows how you might create a policy that limits managing an S3 bucket by allowing all S3 actions on the specific bucket, but explicitly denying access to every AWS service except Amazon S3\. This policy also denies access to actions that can't be performed on an S3 bucket, such as `s3:ListAllMyBuckets` or `s3:GetObject`\. To use this policy, replace the red text in the example policy with your own information\.

If this policy is used in combination with other policies \(such as the [AmazonS3FullAccess](https://aws-iam-console-beta-dev2.integ.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AmazonS3FullAccess) or [AmazonEC2FullAccess](https://aws-iam-console-beta-dev2.integ.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AmazonEC2FullAccess) AWS managed policies\) that allow actions denied by this policy, then access is denied\. This is because an explicit deny statement takes precedence over allow statements\. For more information, see [[ERROR] BAD/MISSING LINK TEXT](reference_policies_evaluation-logic.md#policy-eval-denyallow)\.

**Warning**  
`NotAction` and `NotResource` are advanced policy elements that must be used with care\. This policy denies access to every AWS service except Amazon S3\. If you attach this policy to a user, any other policies that grant permissions to other services are ignored and access is denied\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::<BUCKET-NAME>",
        "arn:aws:s3:::<BUCKET-NAME>/*"
      ]
    },
    {
      "Effect": "Deny",
      "NotAction": "s3:*",
      "NotResource": [
        "arn:aws:s3:::<BUCKET-NAME>",
        "arn:aws:s3:::<BUCKET-NAME>/*"
      ]
    }
  ]
}
```