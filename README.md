### **# 🚀 Scalable Online Notes Application on AWS**



**A scalable and highly available Online Notes Application deployed on AWS using multiple cloud services.**



**The application allows users to:**



**- 📝 Create and store notes**

**- ☁️ Upload files to Amazon S3**

**- 🗄️ Store note data in Amazon RDS MySQL**

**- ⚡ Trigger AWS Lambda when files are uploaded**

**- 📊 Store upload/log events in DynamoDB**

**- 📧 Send notifications using Amazon SNS**

**- ⚖️ Distribute traffic using an Application Load Balancer**

**- 📈 Automatically scale EC2 instances using Auto Scaling**

**- 🌐 Access the application through a custom domain using Route 53**



**---**



### **# 🏗️ Architecture**



**!\[AWS Architecture](screenshots/architecture.png)**



**## Architecture Flow**



&#x20;                        **👤 User**

&#x20;                          **│**

&#x20;                          **▼**

&#x20;                   **🌐 Amazon Route 53**

&#x20;                          **│**

&#x20;                          **▼**

&#x20;                **⚖️ Application Load Balancer**

&#x20;                          **│**

&#x20;                          **▼**

&#x20;                **📈 Auto Scaling Group**

&#x20;                     **Min: 2**

&#x20;                     **Desired: 2**

&#x20;                     **Max: 4**

&#x20;                   **/           \\**

&#x20;                  **▼             ▼**

&#x20;           **🖥️ EC2 Instance   🖥️ EC2 Instance**

&#x20;             **Node.js App       Node.js App**

&#x20;                  **│               │**

&#x20;                  **└───────┬───────┘**

&#x20;                          **│**

&#x20;               **┌──────────┴──────────┐**

&#x20;               **▼                     ▼**

&#x20;        **🗄️ Amazon RDS           ☁️ Amazon S3**

&#x20;          **MySQL Database          File Storage**

&#x20;                                     **│**

&#x20;                                     **▼**

&#x20;                               **⚡ AWS Lambda**

&#x20;                                 **/        \\**

&#x20;                                **▼          ▼**

&#x20;                       **📊 DynamoDB       📧 Amazon SNS**

&#x20;                        **Upload Logs       Email Alert**



### **☁️ AWS Services Used**

### 

**| AWS Service               | Purpose                                     |**

**| ------------------------- | ------------------------------------------- |**

**| Amazon VPC                | Custom network infrastructure               |**

**| Amazon EC2                | Hosts the Node.js application               |**

**| Application Load Balancer | Distributes traffic across EC2 instances    |**

**| Auto Scaling Group        | Automatically manages application instances |**

**| Amazon RDS MySQL          | Stores notes and application data           |**

**| Amazon S3                 | Stores uploaded files                       |**

**| AWS Lambda                | Processes S3 upload events                  |**

**| Amazon DynamoDB           | Stores application/upload logs              |**

**| Amazon SNS                | Sends email notifications                   |**

**| Amazon Route 53           | Routes custom domain traffic to ALB         |**

**| AWS IAM                   | Manages permissions between AWS services    |**



### **🌐 Network Architecture**



**The application is deployed inside a custom Amazon VPC.**



**Custom VPC**

**│**

**├── Public Subnet 1**

**│     └── Application Infrastructure**

**│**

**├── Public Subnet 2**

**│     └── Application Infrastructure**

**│**

**├── Private Subnet 1**

**│     └── RDS / Private Resources**

**│**

**└── Private Subnet 2**

&#x20;     **└── RDS / Private Resources**



#### **The VPC also includes:**



**Internet Gateway**

**NAT Gateway**

**Public Route Table**

**Private Route Table**

**Security Groups**

**💻 Application Features**

**📝 Create Notes**



**Users can create notes using the web application.**



&#x20;             **User**

&#x20;              **↓**

&#x20;      **Node.js / Express**

&#x20;              **↓**

&#x20;       **Amazon RDS MySQL**

&#x20;      **☁️ Upload Files**



**Users can upload supported files through the application.**



&#x20;            **User**

&#x20;             **↓**

&#x20;     **Node.js Application**

&#x20;             **↓**

&#x20;          **Amazon S3**

&#x20; **⚡ Event Driven Processing**

##### 

##### **When a file is uploaded to S3:**



&#x20;             **Amazon S3**

&#x20;                **↓** 

&#x20;       **Object Created Event**

&#x20;           **AWS Lambda**

&#x20;                **├── → Amazon DynamoDB**

&#x20;                **│       Store upload/log information**

&#x20;                **│**

&#x20;                **└── → Amazon SNS**

&#x20;                 **Send email notification**



#### **📈 High Availability and Scaling**



**The application is deployed using:**



**Application Load Balancer**

**Target Group**

**Multiple EC2 instances**

**Auto Scaling Group**



**Auto Scaling configuration:**



**Minimum Capacity: 2**

**Desired Capacity: 2**

**Maximum Capacity: 4**



##### **Traffic flow:**



* **User**

&#x20; **↓**

**Application Load Balancer**

&#x20; **↓**

**Target Group**

&#x20; **↓**

**EC2 Instances managed by Auto Scaling Group**

**🔐 Security**



**The following security practices were used:**



**RDS deployed in private subnets**

**Security Groups used to control network access**

**IAM roles used for AWS service permissions**

**Sensitive environment variables stored in .env**

**.env excluded from GitHub using .gitignore**

**SSH/private key files are not stored in the repository**

### 

### **🛠️ Tech Stack**



**Application**

**Node.js**

**Express.js**

**EJS**

**MySQL**

**Cloud \& DevOps**

**AWS EC2**

**AWS VPC**

**AWS RDS**

**AWS S3**

**AWS Lambda**

**AWS DynamoDB**

**AWS SNS**

**AWS IAM**

**Application Load Balancer**

**Auto Scaling Group**

**AWS Route 53**

**PM2**



