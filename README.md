# AWS S3 Static Website Hosting Project

A comprehensive guide to hosting a static website on Amazon S3, demonstrating cloud-based web hosting using AWS services.

## 📋 Project Overview

This project demonstrates the complete process of hosting a static website using Amazon S3, from initial bucket creation to final deployment with public accessibility. The implementation includes proper security configurations and troubleshooting common issues encountered during the hosting process.

**Author**: Sanil Gajbhiye  
**Duration**: ~45 minutes  
**Region**: Asia Pacific (Mumbai)

## 🏗️ Architecture

```
Internet Users
      ↓
S3 Bucket Endpoint URL
      ↓
Amazon S3 Bucket (Static Website Hosting Enabled)
      ↓
Website Files (index.html + assets)
```

## 🛠️ Technologies & Services Used

- **Amazon S3**: Primary hosting service for static website
- **S3 Static Website Hosting**: Feature to serve website content
- **Access Control Lists (ACL)**: For managing public access permissions
- **S3 Bucket Policies**: For protecting resources from deletion
- **AWS Bucket Policy Generator**: Tool for creating security policies

## 🎯 Learning Objectives

This project covers the following key AWS concepts:

1. **S3 Bucket Creation**: Understanding global naming uniqueness and regional selection
2. **Static Website Hosting**: Converting S3 bucket into a web server
3. **Access Control Lists (ACL)**: Managing public access to individual objects
4. **Bucket Policies**: Implementing security measures to protect public resources
5. **Troubleshooting**: Resolving common 403 Forbidden errors

## 📁 Project Structure

```
S3 Bucket/
├── index.html                                    # Main website file
└── NextWork - Everyone should be in a job they love_files/   # Image assets folder
    ├── image1.jpg
    ├── image2.png
    └── ...other assets
```

## 🚀 Implementation Steps

### Step 1: Create S3 Bucket
⏱️ **Duration**: 5-10 minutes

1. Navigate to AWS S3 Console
2. Click "Create bucket"
3. Enter a globally unique bucket name
4. Select **Asia Pacific (Mumbai)** region for optimal proximity
5. Configure remaining settings as needed
6. Create the bucket

> **Important**: S3 bucket names are globally unique across all AWS accounts worldwide.

### Step 2: Upload Website Files

1. Upload `index.html` file (main website blueprint)
2. Upload `NextWork - Everyone should be in a job they love_files` folder containing all image assets
3. Ensure all necessary files are properly uploaded

### Step 3: Enable Static Website Hosting

1. Select your S3 bucket
2. Navigate to **Properties** tab
3. Scroll to **Static website hosting** section
4. Click **Edit**
5. Enable **Static website hosting**
6. Set **Index document** to `index.html`
7. Save changes

**Result**: S3 generates a bucket endpoint URL for public access.

### Step 4: Resolve 403 Forbidden Error

#### Problem
Initial access to bucket endpoint URL results in "403 Forbidden" error because uploaded files remain private despite enabled static hosting.

#### Solution: Configure ACL for Public Access

1. Select `index.html` file in S3 bucket
2. Navigate to **Permissions** tab
3. Edit **Access Control List (ACL)**
4. Grant **Read** permissions to **Everyone (public access)**
5. Repeat process for `NextWork - Everyone should be in a job they love_files` folder
6. Apply public read permissions to all objects in the folder

### Step 5: Implement Bucket Policy for Resource Protection

⚠️ **Most Challenging Part**: Creating appropriate bucket policy to prevent deletion of public resources.

#### Using AWS Bucket Policy Generator

1. Access AWS Bucket Policy Generator
2. Configure policy to explicitly deny deletion operations
3. Include the following actions in deny statement:
   - `s3:DeleteObject`
   - `s3:DeleteObjectVersion`
   - `s3:PutLifecycleConfiguration`

#### Sample Bucket Policy Structure

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid":"Statement1"
            "Effect": "Deny",
            "Principal": "*",
            "Action": [
                "s3:DeleteObject",
                "s3:DeleteObjectVersion",
                "s3:PutLifecycleConfiguration"
            ],
            "Resource": [ 
                "arn:aws:s3:::nextwork-website-project-sanil"
                "arn:aws:s3:::nextwork-website-project-sanil/*"

            ]

        }
    ]
}
```

> **Note**: All three deletion-related actions are required because objects can be deleted either explicitly via DELETE API or through lifecycle configuration.

## 🔧 Troubleshooting

### Common Issue: 403 Forbidden Error

**Symptoms**: Bucket endpoint URL shows "403 Forbidden" error

**Cause**: Website files uploaded to S3 remain private despite static hosting being enabled

**Solution**:
1. Enable ACL on bucket if not already enabled
2. Make `index.html` publicly readable via ACL
3. Make all asset folders/files publicly readable via ACL
4. Ensure bucket policy allows public read access

### Understanding the Difference

- **Static Website Hosting**: Enables S3 to serve files as a website
- **File Permissions**: Separate configuration required for public access to individual files

## ✅ Success Criteria

- [x] S3 bucket created successfully
- [x] Static website hosting enabled
- [x] Website files uploaded and configured
- [x] 403 Forbidden error resolved
- [x] Public accessibility achieved via bucket endpoint URL
- [x] Bucket policy implemented for resource protection

## 🎉 Project Outcome

**Success!** The static website is now publicly accessible through the S3 bucket endpoint URL. Visitors can view the complete website including all images and content.

## 📖 Key Learnings

1. **Global Bucket Naming**: S3 bucket names must be globally unique across all AWS accounts
2. **Regional Selection**: Choosing the nearest region (Mumbai) for optimal performance
3. **Dual Configuration**: Static hosting and file permissions are separate configurations
4. **Security Implementation**: Bucket policies provide additional protection layers
5. **Troubleshooting Skills**: Understanding and resolving common AWS hosting issues

## 🔗 Useful Resources

- [AWS S3 Static Website Hosting Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)
- [AWS Bucket Policy Generator](https://awspolicygen.s3.amazonaws.com/policygen.html)
- [S3 Access Control Lists (ACL)](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html)

## 🤝 Contributing

This project serves as a learning reference for AWS S3 static website hosting. Feel free to:
- Fork the repository
- Suggest improvements
- Share your own implementation experiences
- Report any issues or corrections needed

## 📝 License

This project is created for educational purposes as part of NextWork learning program.

---

**Project Duration**: ~45 minutes  
**Difficulty Level**: Beginner to Intermediate  
**AWS Services**: S3, IAM (Bucket Policies), ACL
