# S3 Bucket Policies

Created: May 8, 2019 6:11 PM
Updated: May 8, 2019 6:20 PM

**Force Encryption Policy**

Enforced two conditions to deny any request without encryption header and deny incorrect encryption header value.

```
{
“Id”: “Policy197393696393”,
“Version” “2012-10-17
“Statement”: [
“Sid”: “Stmt197376396333”,
“Action”: [
“s

“Effect”: “Deny”,
“Resource”: “<arn::aws…>”,
“Condition”: {
“StringNotEquals”: {
“S3:x-amz-server-side-encryption”: “AES256”

“Principle”: “*”

{
“Sid”: “Stmt197375396333”,
“Action”: [
“s3:PutObject”
],
“Effect”: “Deny”,
“Resource”: “<arn::aws…>”,
“Condition”: {
“Null”: {
“S3:x-amz-server-side-encryption”: “true”
}
},
“Principle”: “*”
}
}
```