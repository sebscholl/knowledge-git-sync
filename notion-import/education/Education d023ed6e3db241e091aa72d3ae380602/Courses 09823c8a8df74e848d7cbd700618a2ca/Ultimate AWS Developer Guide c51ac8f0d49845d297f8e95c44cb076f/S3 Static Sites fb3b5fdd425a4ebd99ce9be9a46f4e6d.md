# S3 Static Sites

Created: May 8, 2019 7:01 PM
Updated: May 8, 2019 7:09 PM

Ability to host static sites on S3. Enabled in bucket permissions by selecting Static Website Hosting, declaring an entry file and other options.

URL: <bucket-name>.s3-website.<AWS-region>.amazonaws.com

By default the site is protected, thus you need to add a public permissions to the bucket (in access controls AND bucket policy)

Uploaded static files (index.html) can reference files stored in s3 relatively.

**Public Policy**

```
{
"Version":"2012-10-17",
"Statement":[{
"Sid":"PublicReadGetObject",
"Effect":"Allow",
"Principal": "*",
"Action":["s3:GetObject"],
"Resource":["arn:aws:s3:::example-bucket/*"
]
}
]
}
```