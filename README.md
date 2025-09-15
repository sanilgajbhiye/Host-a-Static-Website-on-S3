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

![S3 Bucket Creation Success]
(<img width="1918" height="910" alt="S3 bucket " src="https://github.com/user-attachments/assets/71a72078-8dc4-4b0d-9360-7376efa8b057" />)
*Successfully created S3 bucket 'nextwork-website-project-sanil' in Asia Pacific (Mumbai) region*

> **Important**: S3 bucket names are globally unique across all AWS accounts worldwide.

### Step 2: Upload Website Files

1. Upload `index.html` file (main website blueprint)
2. Upload `NextWork - Everyone should be in a job they love_files` folder containing all image assets
3. Ensure all necessary files are properly uploaded

![S3 Bucket Objects]
(<img width="1918" height="906" alt="FIles and folders in S3" src="https://github.com/user-attachments/assets/84b3304f-df7f-4184-bc2e-1e356ae6401e" />)
*S3 bucket showing uploaded files: index.html (58.8 KB) and NextWork assets folder*

### Step 3: Enable Static Website Hosting

1. Select your S3 bucket
2. Navigate to **Properties** tab
3. Scroll to **Static website hosting** section
4. Click **Edit**
5. Enable **Static website hosting**
6. Set **Index document** to `index.html`
7. Save changes

![Static Website Hosting Configuration]
(<img width="1918" height="903" alt="Static website setting" src="https://github.com/user-attachments/assets/c99bb41d-a713-410b-8f8c-6153e3723db5" />)
*Static website hosting configuration showing 'Enable' selected and index.html configured as the index document*

**Result**: S3 generates a bucket endpoint URL for public access.

### Step 4: Resolve 403 Forbidden Error

#### Problem
Initial access to bucket endpoint URL results in "403 Forbidden" error because uploaded files remain private despite enabled static hosting.

![403 Forbidden Error]
(<img width="1918" height="230" alt="URL access error" src="https://github.com/user-attachments/assets/215d68fc-ec57-410b-bc8d-42f030c333cb" />)
*403 Forbidden error encountered when trying to access the website before configuring public permissions*

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

![Bucket Policy Configuration]
(<img width="1918" height="907" alt="bucket policy " src="https://github.com/user-attachments/assets/1abbb02d-fdd0-40b4-89d4-efa51b511344" />)
*Bucket policy JSON configuration showing deny statement for deletion actions*

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Deny",
            "Principal": "*",
            "Action": [
                "s3:DeleteObject",
                "s3:DeleteObjectVersion", 
                "s3:PutLifecycleConfiguration"
            ],
            "Resource": [
                "arn:aws:s3:::nextwork-website-project-sanil",
                "arn:aws:s3:::nextwork-website-project-sanil/*"
            ]
        }
    ]
}
```

#### Bucket Policy Effectiveness Test

![Bucket Policy Protection Test]
(<img width="1918" height="903" alt="Access denied to delete objects " src="https://github.com/user-attachments/assets/eec765b8-5d41-4781-9edf-ba354a4c5835" />)
*Demonstration of bucket policy effectiveness - 45 objects (2.7 MB) failed to delete due to "Access denied" errors, proving the policy is working correctly*

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

## 📸 Project Screenshots

All screenshots demonstrate the complete implementation process:

1. **Bucket Creation Success** - Shows successful creation of 'nextwork-website-project-sanil' bucket in Asia Pacific (Mumbai) region
2. **File Upload Structure** - Displays uploaded index.html (58.8 KB) and NextWork assets folder
3. **Static Website Hosting Configuration** - Shows enabled static hosting with index.html as the index document
4. **403 Forbidden Error** - Demonstrates the initial access error before public permissions were configured
5. **Bucket Policy Implementation** - Shows JSON configuration for preventing resource deletion
6. **Policy Effectiveness Test** - Proves policy works by showing 45 objects failed to delete with "Access denied" errors
7. **Final Website Result** - Complete NextWork landing page successfully hosted and accessible

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

## 🎉 Final Result

**Success!** The static website is now publicly accessible through the S3 bucket endpoint URL. Visitors can view the complete NextWork website including all images and interactive elements.
<img width="1918" height="907" alt="working website" src="https://github.com/user-attachments/assets/c0efa897-264c-416e-a62f-1df0ef56b9d7" />
