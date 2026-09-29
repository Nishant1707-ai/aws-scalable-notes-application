# 🚀 Scalable Online Notes Application on AWS

A full-stack Online Notes Application deployed on AWS with a scalable and highly available cloud architecture.

The application allows users to create notes and upload attachments. Notes are stored in Amazon RDS MySQL, while uploaded files are stored in Amazon S3. AWS Lambda processes S3 upload events and records activity in DynamoDB while sending notifications through Amazon SNS.

The application is hosted on Amazon EC2 and exposed through an Application Load Balancer with Auto Scaling. Amazon Route 53 is used for custom domain routing.

---

## 🏗️ Architecture

![AWS Architecture](screenshots/architecture.png)

### Architecture Flow

```text
                         👤 User
                           │
                           ▼
                    🌐 Route 53
                           │
                           ▼
                ⚖️ Application Load Balancer
                           │
                           ▼
                 📈 Auto Scaling Group
                       ┌───┴───┐
                       ▼       ▼
                    EC2 #1   EC2 #2
                       │       │
                       └───┬───┘
                           │
                     Node.js App
                    /           \
                   ▼             ▼
             RDS MySQL          S3
            Notes Database   File Storage
                                 │
                                 ▼
                              Lambda
                             /      \
                            ▼        ▼
                       DynamoDB     SNS
                       Log Data    Email
☁️ AWS Services Used
Service	Purpose
Amazon VPC	Custom networking with public and private subnets
Amazon EC2	Hosts the Node.js application
Application Load Balancer	Distributes HTTP traffic across EC2 instances
Auto Scaling Group	Maintains and scales application instances
Amazon RDS MySQL	Stores application notes
Amazon S3	Stores uploaded files
AWS Lambda	Processes S3 upload events
Amazon DynamoDB	Stores application/upload event logs
Amazon SNS	Sends upload notifications
Amazon Route 53	Provides custom domain routing
AWS IAM	Controls permissions between AWS services
NAT Gateway	Provides outbound internet access for private resources
Internet Gateway	Provides internet connectivity for the VPC
🌐 Network Architecture

The application uses a custom VPC with:

2 Public Subnets
2 Private Subnets
Internet Gateway
NAT Gateway
Public Route Table
Private Route Table
Security Groups
Network Flow
                         Internet
                            │
                            ▼
                    Internet Gateway
                            │
                     ┌──────┴──────┐
                     │   VPC       │
                     │             │
             Public Subnets    Private Subnets
                  │                  │
                  │                  └── RDS
                  │
                  └── ALB → EC2
                         │
                         └── NAT Gateway
💻 Application Features
📝 Create Notes

Users can create notes through the web interface.

User
  ↓
Node.js / Express
  ↓
Amazon RDS MySQL

The note title and description are stored in the MySQL database.

☁️ File Upload

Users can upload attachments through the application.

User
  ↓
Node.js Application
  ↓
Amazon S3

The uploaded files are stored in the configured S3 bucket.

⚡ S3 Event Processing

When an object is uploaded to S3, an Object Created event triggers the Lambda function.

Amazon S3
    │
    │ Object Created Event
    ▼
AWS Lambda
    │
    ├──────────────► DynamoDB
    │                Upload/Event Log
    │
    └──────────────► SNS
                     Email Notification
⚖️ Load Balancing & Auto Scaling

The application runs behind an Application Load Balancer.

Traffic flow:

User
  ↓
Route 53
  ↓
Application Load Balancer
  ↓
Target Group
  ↓
EC2 Instances

The Auto Scaling Group was configured with:

Minimum Capacity : 2
Desired Capacity : 2
Maximum Capacity : 4

This allows the application infrastructure to maintain multiple EC2 instances and scale according to the configured Auto Scaling policies.

🔐 Security Configuration

Security Groups were configured to control communication between the application components.

Application Load Balancer
HTTP : 80
Source: Internet
EC2 Application Instances
Application Port : 3000
Source           : ALB Security Group
RDS MySQL
MySQL : 3306
Source: EC2 Application Security Group

This allows the application to communicate with the database without exposing the database directly to the internet.

🛠️ Technology Stack
Application
Node.js
Express.js
EJS
MySQL
AWS
Amazon VPC
Amazon EC2
Application Load Balancer
Auto Scaling
Amazon RDS
Amazon S3
AWS Lambda
Amazon DynamoDB
Amazon SNS
Amazon IAM
Amazon Route 53
NAT Gateway
Internet Gateway
Server Management
Linux
npm
PM2
Git / GitHub
📂 Project Structure
aws-scalable-notes-application/
│
├── app/
│   ├── server.js
│   ├── package.json
│   ├── package-lock.json
│   │
│   └── views/
│       └── index.ejs
│
├── screenshots/
│   ├── architecture.png
│   ├── application.png
│   ├── vpc.png
│   ├── ec2.png
│   ├── alb.png
│   ├── autoscaling.png
│   ├── rds.png
│   ├── s3.png
│   ├── lambda.png
│   ├── dynamodb.png
│   ├── sns.png
│   └── route53.png
│
├── docs/
│   └── DEPLOYMENT.md
│
├── .gitignore
├── .env.example
└── README.md
⚙️ Local / EC2 Setup
1. Clone the Repository
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd aws-scalable-notes-application/app
2. Install Dependencies
npm install
3. Configure Environment Variables

Create a .env file:

PORT=3000

AWS_REGION=ap-south-1

S3_BUCKET_NAME=your-s3-bucket-name

RDS_HOST=your-rds-endpoint
RDS_USER=your-rds-user
RDS_PASSWORD=your-rds-password
RDS_DATABASE=your-database-name

Never commit .env or any credentials to GitHub.

4. Start the Application
node server.js

The application runs on:

http://localhost:3000
🔄 PM2 Process Management

PM2 was used to keep the Node.js application running on EC2.

Install PM2
sudo npm install -g pm2
Start the application
pm2 start server.js --name notes-app
Check status
pm2 status
Save the process
pm2 save
Configure startup
pm2 startup

After running pm2 startup, execute the command provided by PM2.

Then save the process list again:

pm2 save
Restart application
pm2 restart notes-app
🧪 Testing

The following application components were tested:

 Create notes
 Store notes in RDS MySQL
 Upload files
 Store uploaded files in S3
 Trigger Lambda from S3 Object Created events
 Store event information in DynamoDB
 Send SNS notification
 Connect EC2 application to private RDS
 Configure ALB
 Configure Target Group health checks
 Configure Auto Scaling Group
 Configure Route 53 custom domain
 Run Node.js application using PM2
📸 Project Screenshots
Application

VPC

EC2

Application Load Balancer

Auto Scaling

RDS

S3

Lambda

DynamoDB

SNS

Route 53

📖 Deployment Documentation

Detailed deployment commands and configuration steps are available in:

docs/DEPLOYMENT.md
🚧 Future Improvements

The following improvements can be added in future versions:

HTTPS using AWS Certificate Manager
CloudFront for content delivery
CI/CD using GitHub Actions or Jenkins
Docker containerization
Infrastructure as Code using Terraform
Application monitoring and alerting
Centralized application logging
Kubernetes deployment
🎯 What I Learned

This project provided hands-on experience with:

Designing AWS VPC networking
Working with public and private subnets
Configuring route tables, Internet Gateway and NAT Gateway
Deploying Node.js applications on EC2
Connecting EC2 applications to private RDS
Working with Amazon S3
Building event-driven workflows using S3 and Lambda
Logging events with DynamoDB
Sending notifications using SNS
Configuring IAM permissions
Configuring Application Load Balancers
Implementing EC2 Auto Scaling
Managing Node.js applications with PM2
Configuring custom DNS with Route 53
Managing a cloud project using Git and GitHub
👨‍💻 Author

Nishant

Aspiring DevOps & Cloud Engineer

⭐ If you found this project useful, consider giving the repository a star.
