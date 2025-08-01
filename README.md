# AWS Projects Portfolio

## Project 1: AWS Three-Tier Web Application Demo

**Goal**: Combine Infrastructure as Code with manual provisioning for flexible deployment of Three-Tier Application.

#### AWS Services Used

| Category                  | AWS Service                   | Purpose                                                                 |
|---------------------------|-------------------------------|-------------------------------------------------------------------------|
| Infrastructure & Networking | **Amazon VPC**                | Isolated network environment for all tiers                            |
|                           | **Subnets (Public & Private)** | Separates Web, App, and DB tiers across multiple AZs                   |
|                           | **Internet Gateway**          | Provides internet access to public subnets                              |
|                           | **NAT Gateways**              | Enables private subnets to access the internet                          |
|                           | **Elastic IPs**              | Used with NAT Gateways for static outbound IPs                           |
|                           | **Route Tables**              | Controls traffic routing within the VPC                                 |
|                           | **Security Groups**           | Manages access control between tiers and from internet                  |
|                           | **DB Subnet Group**           | Required for multi-AZ Aurora deployments                                |
| Compute & Hosting         | **Amazon EC2**                | Hosts Web (React + Nginx) and App (Node.js) tiers                       |
|                           | **Auto Scaling Groups**       | Automatically adjusts EC2 instances based on traffic                    |
| Load Balancing            | **Application Load Balancer (ALB)** | External ALB for web tier, internal ALB for app tier              |
| Database                  | **Amazon Aurora MySQL**       | Managed, scalable MySQL-compatible relational database                  |
|                           | **Aurora Read Replica**        | Provides high availability and performance for read operations         |
| Security & Secrets        | **AWS IAM**                   | Defines access permissions for EC2 and Secrets Manager                  |
|                           | **AWS Secrets Manager**        | Stores Aurora credentials securely                                     |
| Orchestration & Automation | **AWS CloudFormation**         | Automates provisioning of all infrastructure components               |


#### Implementation:
- CloudFormation templates deployed for network infrastructure (VPC, subnets, security groups)
- CloudFormation template for Aurora MySQL database setup
- Manual EC2 instance provisioning within the CloudFormation-created VPC
- Frontend and backend services deployed and tested on EC2 instances
- Database connectivity verified between application and Aurora cluster

**Outcome**: Hybrid approach demonstrating both automated infrastructure and manual application deployment

![CloudFormation Architecture](https://github.com/user-attachments/assets/01a5a360-e550-4b76-82c7-8a27800ec777)

---

## Project 2: Fully Automated ECS Deployment Pipeline for Book App on AWS

**Goal**: Deploy containerized Book App using manual setup and CloudFormation-based CI/CD pipelines

#### AWS Services Used

| Category                  | AWS Service               | Purpose                                                                 |
|---------------------------|---------------------------|-------------------------------------------------------------------------|
| Infrastructure & Networking | **Amazon VPC**            | Provides isolated network environment for ECS and ALB                 |
|                           | **Subnets (Public/Private)** | Separates access control and network segmentation                    |
|                           | **Internet Gateway, NAT Gateway** | Enables internet access for public and private subnets          |
|                           | **Route Tables**          | Manages traffic routing across the network                              |
|                           | **Security Groups**       | Controls access to ECS tasks, ALB, and other components                 |
| Container & Deployment    | **Amazon ECS (Fargate)**   | Runs containers without managing servers                               |
|                           | **Amazon ECR**            | Stores container images securely                                        |
|                           | **Application Load Balancer (ALB)** | Distributes incoming traffic to ECS services                  |
|                           | **ECS Task Definitions & Services** | Defines how containers run and scale                          |
| CI/CD & Automation        | **AWS CodeCommit**        | Git-based code repository for storing application source code           |
|                           | **AWS CodeBuild**         | Builds and packages container images automatically                      |
|                           | **AWS CodeDeploy**        | Manages ECS deployment and blue-green deployments                       |
|                           | **AWS CodePipeline**      | Automates the end-to-end CI/CD pipeline                                 |
| Security                  | **AWS IAM**               | Controls access via roles and policies across all AWS services          |


### Implementation:

#### Manual Deployment
- Manual creation of VPC components (subnets, security groups, NAT gateway)
- ECR repository setup for container image storage
- ECS Fargate cluster and service configuration through AWS Console
- Application Load Balancer and target groups manual setup
- IAM roles creation for ECS task execution
- Local Docker image build and push to ECR using AWS CLI
- Book App deployed and accessible via ALB DNS name

#### Standard CI/CD Pipeline
- CloudFormation templates for automated CodePipeline setup
- CodeCommit, CodeBuild, and CodeDeploy integration
- Automated rolling updates to existing ECS service
- Pipeline triggers on code commits for continuous deployment

#### Blue-Green Deployment
- CloudFormation templates for blue-green deployment pipeline
- Separate load balancer configuration for zero-downtime deployments
- Automated traffic shifting between blue and green environments
- Safe rollback capabilities on deployment failures

**Outcome**: Containerized Book App with manual control and automated CI/CD options for different deployment strategies

<img width="1911" height="1046" alt="Screenshot 2025-07-29 164220" src="https://github.com/user-attachments/assets/6371e465-3c0b-497d-b8e5-e3489413c98d" />

---

## Project 3: AWS Serverless Stock Trading Platform
The AWS Serverless Stock Trading Platform is a fully cloud-native, serverless application designed to simulate real-time stock trading. It is built using AWS Lambda, API Gateway, Amazon S3, and CloudFront, offering users a fast, scalable, and cost-effective trading interface accessible through a responsive web UI.

**Goal**:
Combine Infrastructure as Code (IaC) with manual provisioning to enable a flexible deployment strategy for a Three-Tier Web Application on AWS.

#### AWS Services Used

| Category               | AWS Service             | Purpose                                                                 |
|------------------------|-------------------------|-------------------------------------------------------------------------|
| Compute                | **AWS Lambda**          | Executes backend trading logic (buy, sell, stock check)                |
| API & Integration      | **Amazon API Gateway**  | Exposes Lambda functions as RESTful APIs                               |
| Orchestration          | **AWS Step Functions**  | Manages the flow between multiple Lambda functions                     |
| Storage & Hosting      | **Amazon S3**           | Hosts static frontend files (HTML, CSS, JS)                            |
| Content Delivery       | **Amazon CloudFront**   | Caches and delivers the frontend globally with low latency             |
| DevOps & Deployment    | **AWS CloudFormation**  | Automates deployment of infrastructure components                      |
| Web Hosting (Optional) | **AWS Amplify**         | Simplifies hosting and CI/CD for the frontend                          |
| Networking             | **Amazon VPC**          | Used in hybrid or advanced setups for secure communication             |
| Security               | **AWS IAM**             | Manages permissions for Lambda, API Gateway, and Step Functions        |
| Secrets Management     | **AWS Secrets Manager** | (Optional) Manages sensitive data like API keys and credentials        |

#### Implementation:
- CloudFormation templates used to deploy core infrastructure:
- VPC with public/private subnets
- Route tables, internet/NAT gateways
- Security groups for controlled access
- Aurora MySQL cluster provisioned using CloudFormation for the data tier
- Manual provisioning of EC2 instances for the web and app tiers within the pre-created VPC
- Frontend and backend applications deployed and configured on EC2 instances
- Database connectivity tested and verified between backend EC2 and Aurora MySQL
- Environment variables and security groups configured to allow seamless integration

**Outcome**:
A hybrid deployment model that combines the reliability and repeatability of Infrastructure as Code with the flexibility of manual provisioning, showcasing real-world deployment workflows for a traditional three-tier architecture on AWS.

<img width="1893" height="1021" alt="Screenshot 2025-07-31 024047" src="https://github.com/user-attachments/assets/a9bd5e59-19e4-4891-97aa-74e8510625c6" />

*Each project includes detailed implementation guides, troubleshooting tips, and cleanup procedures. Explore individual project folders for complete documentation and video tutorials.*

