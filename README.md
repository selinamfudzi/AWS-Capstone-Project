

```markdown

# 🌐 AWS Serverless Translation Pipeline
 
A fully automated, serverless infrastructure built with Terraform that translates text using AWS Translate. The system is triggered by uploading a JSON file to an S3 bucket and delivers the translated result to another S3 bucket.
 
## 📋 Project Overview
 
This project demonstrates a real-world Infrastructure-as-Code (IaC) solution on AWS, integrating:

- **AWS Translate** for neural machine translation

- **Amazon S3** for secure, durable object storage

- **AWS Lambda** for serverless compute

- **Terraform** for infrastructure provisioning and management
 
## 🏗️ Architecture
 
```

[User] --> [Uploads JSON to S3 Request Bucket] --> [S3 Event Notification]

    |

    V

[AWS Lambda Triggered] --> [Calls AWS Translate API]

    |

    V

[Writes Result to S3 Response Bucket] --> [User Retrieves Output]

```
 
## ⚙️ Prerequisites
 
Before deploying this infrastructure, ensure you have:
 
1.  **AWS Account** with appropriate permissions

2.  **AWS CLI** configured with credentials

    ```bash

    aws configure

    ```

3.  **Terraform** installed ([Download here](https://www.terraform.io/downloads))

4.  **Git** installed
 
## 🚀 Deployment
 
### 1. Clone the Repository

```bash

git clone https://github.com/your-username/aws-translation-project.git

cd aws-translation-project

```
 
### 2. Initialize Terraform

```bash

terraform init

```
 
### 3. Review Execution Plan

```bash

terraform plan

```
 
### 4. Deploy Infrastructure

```bash

terraform apply

```

Type `yes` when prompted to confirm.
 
## 📁 Project Structure
 
```

aws-translation-project/

├── main.tf                 # Primary Terraform configuration

├── variables.tf            # Terraform variables

├── providers.tf            # AWS provider configuration

├── outputs.tf              # Terraform outputs

├── lambda_function.py      # Python Lambda function code

├── lambda_function.zip     # Packaged Lambda deployment

├── sample_request.json     # Example input file

└── README.md              # This file

```
 
## 📤 How to Use
 
1.  **Create a JSON file** following this format:

    ```json

    {

      "source_language": "es",

      "target_language": "en",

      "text": "Texto que desea traducir aquí."

    }

    ```
 
2.  **Upload the file** to your S3 request bucket:

    ```bash

    aws s3 cp your-file.json s3://[REQUEST_BUCKET_NAME]/

    ```
 
3.  **Check the response bucket** for results:

    ```bash

    aws s3 ls s3://[RESPONSE_BUCKET_NAME]/results/

    ```
 
4.  **Download and view** the translated output:

    ```bash

    aws s3 cp s3://[RESPONSE_BUCKET_NAME]/results/your-file.json .

    ```
 
## 🛠️ Terraform Outputs
 
After successful deployment, Terraform will output:
 
- `request_bucket_name`: Name of the input S3 bucket

- `response_bucket_name`: Name of the output S3 bucket

- `lambda_function_name`: Name of the Lambda function

- `lambda_role_arn`: ARN of the IAM execution role
 
## 💰 Cost Optimization & Free Tier
 
This architecture is designed to operate within AWS Free Tier limits:

- **AWS Lambda**: 1 million free requests/month

- **Amazon S3**: 5 GB standard storage/month

- **AWS Translate**: 2 million characters/month (first 12 months)

- **S3 Lifecycle Policies**: Automatically delete files after 30 days
 
## 🧪 Testing
 
Use the provided `sample_request.json` file to test the pipeline:
 
```bash

aws s3 cp sample_request.json s3://$(terraform output -raw request_bucket_name)/

```
 
## 🧹 Cleanup
 
To destroy all resources and avoid ongoing charges:
 
```bash

terraform destroy

```
 
**Warning**: This will permanently delete all S3 buckets and their contents.
 
## 🤝 Contributing
 
1. Fork the project

2. Create a feature branch (`git checkout -b feature/amazing-feature`)

3. Commit changes (`git commit -m 'Add amazing feature'`)

4. Push to branch (`git push origin feature/amazing-feature`)

5. Open a Pull Request
 
## 📄 License
 
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
 
## 🆘 Troubleshooting
 
**Common Issues:**
 
1.  **Lambda not triggering**: Check S3 bucket permissions and Lambda execution role

2.  **Translation errors**: Verify the JSON format and language codes

3.  **Access denied**: Ensure IAM roles have appropriate permissions
 
**Check CloudWatch Logs:**

```bash

aws logs describe-log-groups --query 'logGroups[?contains(logGroupName, `translation-function`)].logGroupName' --output text

```
 
## 📞 Support
 
If you encounter any problems:

1. Check the [Troubleshooting](#-troubleshooting) section

2. Review AWS CloudWatch logs for errors

3. Open an issue on GitHub with detailed information
 
---
 
**Note**: Always monitor your AWS usage and set up billing alerts to avoid unexpected charges.

```
 
## How to Use This README:
 
1. **Create a new file** in your project folder called `README.md`

2. **Copy and paste** the entire content above into this file

3. **Customize** the sections with your specific information (especially the GitHub URL)

4. **Save** the file and commit it to your repository:
 
```bash

git add README.md

git commit -m "Add comprehensive README documentation"

git push origin main

```
 
This professional README will help anyone understand your project, how to deploy it, and how to use it effectively!
Terraform | HashiCorp Developer
Explore Terraform product documentation, tutorials, and examples.
 
