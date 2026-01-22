# 📚 AWS CLI Commands Guide

<p align="center">
  <img src="https://img.shields.io/badge/AWS-CLI%20v2-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white" alt="AWS CLI v2"/>
  <img src="https://img.shields.io/badge/Version-January%202026-232F3E?style=for-the-badge" alt="Version"/>
  <img src="https://img.shields.io/badge/Language-Spanish-red?style=for-the-badge" alt="Spanish"/>
  <img src="https://img.shields.io/github/license/your-username/aws-cli-guide?style=for-the-badge" alt="License"/>
</p>

<p align="center">
  <b>A comprehensive guide to essential AWS CLI commands for debugging, monitoring, and administration.</b>
</p>

<p align="center">
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-services-covered">Services</a> •
  <a href="#-download">Download</a> •
  <a href="#-contributing">Contributing</a> •
  <a href="./README_ES.md">🇪🇸 Español</a>
</p>

---

## 🎯 About

This guide compiles the most important AWS CLI commands organized by service. While Infrastructure as Code (IaC) tools like Terraform or CloudFormation are typically used to provision and configure AWS services, these commands are essential for:

- 🔍 **Debugging** - Troubleshoot issues in real-time
- 📊 **Monitoring** - Check resource status and health
- 🧪 **Testing** - Validate configurations and permissions
- 🛠️ **Administration** - Quick operational tasks

## 🚀 Quick Start

### Prerequisites

1. **Install AWS CLI v2**
   ```bash
   # macOS
   brew install awscli
   
   # Linux
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   unzip awscliv2.zip
   sudo ./aws/install
   
   # Windows
   msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
   ```

2. **Configure credentials**
   ```bash
   aws configure
   ```

3. **Verify your identity**
   ```bash
   aws sts get-caller-identity
   ```

## 📋 Services Covered

| Category | Services |
|----------|----------|
| **Configuration** | AWS Configure, STS |
| **Compute** | EC2, Security Groups, Auto Scaling, Lambda |
| **Containers** | ECS, ECR |
| **Storage** | S3, EBS |
| **Database** | RDS, DynamoDB |
| **Networking** | VPC, ELB, Route 53, CloudFront |
| **Security** | IAM, Secrets Manager, CloudTrail |
| **Messaging** | SNS, SQS, EventBridge, API Gateway |
| **Monitoring** | CloudWatch, Systems Manager (SSM) |
| **IaC** | CloudFormation |
| **AI/ML** | Bedrock |
| **Cost** | Cost Explorer |

## 📥 Download

| Format | Description | Link |
|--------|-------------|------|
| 📄 **PDF** | Full formatted document | [Download](./docs/Guia_AWS_CLI_Commands.pdf) |
| 📖 **Markdown** | Read online | [View](./docs/AWS_CLI_Guide.md) |

## 💡 Most Used Commands

### Verify Identity
```bash
aws sts get-caller-identity
```

### List EC2 Instances
```bash
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]" --output table
```

### List S3 Buckets
```bash
aws s3 ls
```

### View CloudWatch Logs in Real-Time
```bash
aws logs tail /aws/lambda/my-function --follow
```

### Connect to EC2 via Session Manager
```bash
aws ssm start-session --target i-0123456789abcdef0
```

## 🛠️ Useful Tips

### Global Options
| Option | Description |
|--------|-------------|
| `--debug` | Enable debug mode for troubleshooting |
| `--profile name` | Use a specific credentials profile |
| `--region us-east-1` | Specify AWS region |
| `--output json\|table\|text\|yaml` | Change output format |
| `--query` | Filter results with JMESPath |
| `--dry-run` | Check permissions without executing (EC2) |

### Complementary Tools
- **jq** - Command-line JSON processor
- **aws-vault** - Secure credential management
- **awslogs** - AWS CloudWatch logs viewer

## 📁 Repository Structure

```
aws-cli-guide/
├── README.md           # This file (English)
├── README_ES.md        # Spanish version
├── LICENSE             # MIT License
├── CONTRIBUTING.md     # Contribution guidelines
└── docs/
    ├── Guia_AWS_CLI_Commands.docx    # Full guide (DOCX)
    └── AWS_CLI_Guide.md              # Full guide (Markdown)
```

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) for details on how to submit pull requests.

### Ways to Contribute
- 🐛 Report bugs or errors in commands
- 💡 Suggest new commands or services
- 🌐 Help translate to other languages
- 📝 Improve documentation

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.

## 👤 Author

**Francisco Javier Escobar García**

- LinkedIn: [Connect with me](https://linkedin.com/in/franciscojeg/)
- GitHub: [@franciscojeg](https://github.com/franciscojeg)

## ⭐ Show Your Support

If this guide helped you, please consider giving it a ⭐ on GitHub!

---

<p align="center">
  <b>Official AWS CLI Reference:</b> <a href="https://docs.aws.amazon.com/cli/latest/reference/">docs.aws.amazon.com/cli</a>
</p>
