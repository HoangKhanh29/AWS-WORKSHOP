# AWS Serverless File Notification System Workshop

[![AWS](https://img.shields.io/badge/AWS-Serverless-orange.svg)](https://aws.amazon.com/serverless/)
[![Hugo](https://img.shields.io/badge/Hugo-Static%20Site-blue.svg)](https://gohugo.io/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A comprehensive workshop for building a **Serverless File Notification System** using AWS event-driven architecture. Learn to create a system that automatically sends email notifications when files are uploaded to S3.

## 🏗️ Architecture Overview

### Option 1: Basic System
```
User Upload → S3 Bucket → S3 Event → Lambda Function → SNS Topic → Email Notification
```

### Option 2: Advanced System
```
User Upload → S3 Bucket → S3 Event → Lambda Function → DynamoDB (metadata)
                                                   → SQS Queue → Processing Lambda
                                                   → SNS Topic → Email Notification
API Gateway ← Web Interface ← CloudWatch Dashboard ← Monitoring
```

## 🚀 What You'll Build

- **Serverless file upload system** with automatic notifications
- **Event-driven architecture** using AWS managed services
- **Real-time email notifications** via SNS
- **Metadata storage** in DynamoDB (Option 2)
- **Web interface** for file uploads (Option 2)
- **Monitoring dashboard** with CloudWatch (Option 2)

## 🛠️ Technologies Used

- **AWS S3** - File storage and event source
- **AWS Lambda** - Serverless compute
- **Amazon SNS** - Email notifications
- **Amazon DynamoDB** - NoSQL database (Option 2)
- **Amazon SQS** - Message queuing (Option 2)
- **API Gateway** - REST API (Option 2)
- **CloudWatch** - Monitoring and logging (Option 2)

## 📋 Prerequisites

- **AWS Account** (Free Tier eligible)
- **Valid email address** for notifications
- **Basic knowledge** of AWS services
- **Modern web browser**

## 💰 Cost Estimation

This workshop is designed to run within **AWS Free Tier**:
- **Estimated cost**: $0 if within Free Tier limits
- **Maximum cost**: < $1 USD if exceeding limits

## 🎯 Learning Objectives

After completing this workshop, you will:
- ✅ Understand **serverless architecture** principles
- ✅ Master **event-driven design** patterns
- ✅ Build **production-ready** serverless applications
- ✅ Implement **monitoring and logging** best practices
- ✅ Create **scalable and cost-effective** solutions

## 📚 Workshop Structure

### 1. [Introduction](content/1-Introduce/)
- Serverless architecture concepts
- Event-driven design principles
- AWS services overview

### 2. [Prerequisites](content/2-Prerequiste/)
- AWS account setup
- Environment preparation
- Required permissions

### 3. [Option 1: Basic System](content/3-Option_1/)
- [3.1 Create S3 Bucket](content/3-Option_1/3.1-Create-S3-Bucket/)
- [3.2 Create SNS Topic](content/3-Option_1/3.2-Create-SNS-Topic/)
- [3.3 Create Lambda Function](content/3-Option_1/3.3-Create-Lambda-Function/)

### 4. [Option 2: Advanced System](content/4.Option_2/)
- [4.1 Create DynamoDB Table](content/4.Option_2/4.1-DynamoDB-Table/)
- [4.2 Create SQS Queue](content/4.Option_2/4.2-SQS-Queue/)
- [4.3 Enhanced Lambda Function](content/4.Option_2/4.3-Enhanced-Lambda-Function-with-DynamoDB/)
- [4.4 Create API Gateway](content/4.Option_2/4.4-API-Gateway/)
- [4.5 Build Web Interface](content/4.Option_2/4.5-Web-Interface/)
- [4.6 Setup CloudWatch Dashboard](content/4.Option_2/4.6-CloudWatch-Dashboard/)

### 5. [Test System](content/5-Test-System/)
- End-to-end testing
- Troubleshooting guide

### 6. [Resource Cleanup](content/6-cleanup/)
- Complete cleanup checklist
- Cost verification

## 🌐 Languages

This workshop is available in:
- 🇺🇸 **English** (`_index.md` files)
- 🇻🇳 **Vietnamese** (`_index.vi.md` files)

## 🚀 Quick Start

### Option 1: View Online (Recommended)
1. Visit the deployed workshop site: [Workshop URL]
2. Follow the step-by-step instructions
3. Complete hands-on exercises

### Option 2: Run Locally
1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/aws-serverless-workshop.git
   cd aws-serverless-workshop
   ```

2. **Install Hugo**:
   ```bash
   # macOS
   brew install hugo
   
   # Windows
   choco install hugo
   
   # Linux
   sudo apt install hugo
   ```

3. **Run the workshop site**:
   ```bash
   hugo server -D
   ```

4. **Open in browser**: http://localhost:1313

## 📖 How to Use This Workshop

### For Beginners:
1. Start with **Prerequisites** section
2. Complete **Option 1** (Basic System)
3. Test your implementation
4. Clean up resources

### For Advanced Users:
1. Review **Introduction** for context
2. Complete **Option 2** (Advanced System)
3. Explore additional features
4. Customize for your use case

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Ways to Contribute:
- 🐛 Report bugs or issues
- 💡 Suggest improvements
- 📝 Add translations
- 🔧 Submit code fixes
- 📚 Improve documentation

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **AWS Documentation** for comprehensive service guides
- **Hugo Community** for the excellent static site generator
- **Contributors** who helped improve this workshop

## 📞 Support

- 📧 **Email**: [your-email@domain.com]
- 🐛 **Issues**: [GitHub Issues](https://github.com/yourusername/aws-serverless-workshop/issues)
- 💬 **Discussions**: [GitHub Discussions](https://github.com/yourusername/aws-serverless-workshop/discussions)

## 🔗 Related Resources

- [AWS Serverless Documentation](https://aws.amazon.com/serverless/)
- [AWS Lambda Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)

---

⭐ **Star this repository** if you found it helpful!

🔄 **Share with others** who might benefit from learning serverless architecture!

📚 **Check out our other AWS workshops** for more learning opportunities!