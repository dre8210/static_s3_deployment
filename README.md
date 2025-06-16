# Static Website Deployment to Amazon S3 using GitHub Actions

This project demonstrates how to automatically deploy a static website to Amazon S3 using GitHub Actions for continuous deployment.

## Project Overview

This repository contains a static website that is automatically deployed to an Amazon S3 bucket whenever changes are pushed to the main branch. The deployment is handled by a GitHub Actions workflow that syncs the website files to an S3 bucket configured for static website hosting.

## Features

- **Automated Deployment**: Changes pushed to the main branch are automatically deployed to S3
- **Efficient File Syncing**: Only changed files are uploaded, with unnecessary files excluded
- **Static Website Hosting**: Leverages Amazon S3's static website hosting capabilities

## Prerequisites

To use this project, you'll need:

1. An AWS account
2. An S3 bucket configured for static website hosting
3. AWS IAM credentials with permissions to write to the S3 bucket
4. A GitHub repository with this code

## Setup Instructions

### 1. Create an S3 Bucket for Static Website Hosting

1. Log in to the AWS Management Console
2. Navigate to S3 and create a new bucket
3. Enable "Static website hosting" under bucket properties
4. Set the index document to `index.html`
5. Configure the bucket policy to allow public read access:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::<your-bucket-name>/*"
    }
  ]
}
```

### 2. Create AWS IAM Credentials

1. Create an IAM user with programmatic access
2. Attach a policy with permissions to write to your S3 bucket
3. Save the access key ID and secret access key

### 3. Configure GitHub Repository Secrets

Add the following secrets to your GitHub repository:

- `AWS_ACCESS_KEY_ID`: Your IAM user access key
- `AWS_SECRET_ACCESS_KEY`: Your IAM user secret key
- `AWS_REGION`: The AWS region where your S3 bucket is located (e.g., `us-east-1`)
- `S3_BUCKET_NAME`: The name of your S3 bucket

### 4. GitHub Actions Workflow

The workflow is already configured in `.github/workflows/s3.yml` and will:

1. Checkout the code
2. Configure AWS credentials
3. Sync files to the S3 bucket, excluding unnecessary files

## How It Works

1. When you push changes to the main branch, the GitHub Actions workflow is triggered
2. The workflow authenticates with AWS using your stored credentials
3. It syncs your website files to the S3 bucket, excluding files like `.git`, `Dockerfile`, and `.txt` files
4. Your updated website is immediately available at your S3 website URL

## Customization

- Modify the `s3.yml` workflow to change which files are excluded from deployment
- Add additional steps like running tests or building assets before deployment
- Configure CloudFront distribution for CDN capabilities (not included in this basic setup)

## Website URL

After deployment, your website will be available at:
(http://16-06-2025-s3bucket.s3-website.us-east-2.amazonaws.com/)

## License

[Include your license information here]

## Contributing

[Include contribution guidelines if applicable]
