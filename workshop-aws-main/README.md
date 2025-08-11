# AWS Serverless Workshop

[![AWS](https://img.shields.io/badge/AWS-Serverless-orange.svg)](https://aws.amazon.com/serverless/)
[![Hugo](https://img.shields.io/badge/Hugo-Static%20Site-blue.svg)](https://gohugo.io/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Learn to build serverless file notification systems using AWS event-driven architecture.

## 🏗️ Architecture

**Basic System:**
```
S3 Upload → Lambda → SNS → Email
```

**Advanced System:**
```
S3 Upload → Lambda → DynamoDB + SQS + SNS → Email
           ↓
    API Gateway + Web Interface + CloudWatch
```

## 🚀 What You'll Build

- Serverless file upload system with email notifications
- Event-driven architecture using S3, Lambda, SNS
- Advanced features: DynamoDB, SQS, API Gateway, CloudWatch
- Web interface for file management

## 🛠️ Technologies

- **S3**: File storage with event triggers
- **Lambda**: Serverless compute
- **SNS**: Email notifications
- **DynamoDB**: Metadata storage
- **SQS**: Message queuing
- **API Gateway**: REST API
- **CloudWatch**: Monitoring

## 📋 Prerequisites

- AWS Account (Free Tier)
- Email address for notifications
- Basic AWS knowledge

## 💰 Cost

- **Free Tier**: $0
- **Beyond limits**: < $1 USD

## 📚 Workshop Structure

1. **[Introduction](content/1-Introduce/)** - Architecture concepts
2. **[Prerequisites](content/2-Prerequiste/)** - Setup requirements
3. **[Basic System](content/3-setting-create-s3/)** - S3 + Lambda + SNS
4. **[Advanced System](content/4-setting-up-kinesis/)** - Full architecture
5. **[Monitoring](content/5-logging-with-cloudwatch/)** - CloudWatch setup
6. **[Cleanup](content/6-cleanup/)** - Resource removal

## 🚀 Quick Start

1. **Clone repository:**
   ```bash
   git clone https://github.com/HoangKhanh29/workshop-aws.git
   cd workshop-aws
   ```

2. **Install Hugo:**
   ```bash
   # Windows
   choco install hugo
   
   # macOS
   brew install hugo
   
   # Linux
   sudo apt install hugo
   ```

3. **Run locally:**
   ```bash
   hugo server -D
   ```

4. **Open:** http://localhost:1313

## 🌐 Languages

- 🇺🇸 English
- 🇻🇳 Vietnamese

## 🤝 Contributing

Contributions welcome! Please check [CONTRIBUTING.md](CONTRIBUTING.md).

## 📄 License

MIT License - see [LICENSE](LICENSE) file.

## 📞 Support

- 🐛 [Issues](https://github.com/HoangKhanh29/workshop-aws/issues)
- 💬 [Discussions](https://github.com/HoangKhanh29/workshop-aws/discussions)

---

⭐ **Star this repository** if helpful!