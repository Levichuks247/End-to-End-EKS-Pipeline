# End-to-End-EKS-Pipeline
Automated Provisioning of a Production-Grade Amazon EKS Cluster using Terraform and GitHub Actions CI/CD.
End-to-End-EKS-Pipeline (Project Levichuks)
An automated Infrastructure-as-Code (IaC) project 
that provisions a production-ready Amazon EKS 
(Kubernetes) cluster using Terraform and GitHub 
Actions.

🎯 Purpose of the Project
The goal of this project is to demonstrate the 
ability to automate cloud infrastructure. Instead of 
manually clicking through the AWS Console, this 
project uses a "Code-First" approach to build a 
highly available Kubernetes environment.

👥 Target Users & Stakeholder Value
This project isn't just a technical exercise; it 
solves real-world bottlenecks for three key groups:

1. The Software Developers (The "Tenants")
The Problem: Historically, developers had to wait 
days or weeks for a "SysAdmin" to manually provision 
a server.
The Solution: This pipeline provides a Self-Service 
Platform. Developers can now deploy their code 
(Java, Python, Node.js) in seconds using kubectl. 
They no longer worry about the underlying server; 
they only care that their code is running.
Key Benefit: Velocity. Features reach customers 
faster because the infrastructure "middle-man" has 
been automated away.
2. The DevOps Team (The "Guardians")
The Problem: Manual configurations lead to 
"Configuration Drift" (where no one knows exactly 
how a server was set up) and 2:00 AM emergency calls 
when a server crashes.
The Solution: By using Infrastructure as Code 
(Terraform), the environment is 100% documented and 
repeatable. Because we use Managed Node Groups, the 
cluster is Self-Healing. If a worker node fails, EKS 
automatically replaces it without human 
intervention.
Key Benefit: Reliability & Peace of Mind. The system 
manages its own health, and moving the entire setup 
to a new AWS region is as simple as changing one 
line of code.
3. The Business Owners (The "Stakeholders")
The Problem: Unpredictable AWS bills and revenue 
loss due to website downtime.
The Solution: * Cost Governance: We use IaC to 
enforce specific instance types (like t3.micro), 
ensuring the project stays within the Free Tier and 
prevents "billing surprises."
Business Continuity: The cluster is spread across 
multiple Availability Zones. If one AWS data center 
goes dark, the business stays online.
Key Benefit: Cost Efficiency & Risk Mitigation.
📊 Summary: Problem vs. Solution
User Role	Old Manual Problem	Your 
Project's Automated Solution
Developer	"I have to wait weeks for a server."	
Self-Service: Deploy instantly to EKS.
DevOps	"I have to manually configure every server."	
Automation: One git push builds the entire cloud.
CEO/Owner	"The site crashed and we lost 
money."	High Availability: EKS keeps the site 
running 24/7.

⚠️ The Problem (The "Old Way")
Manual Errors: Manually creating VPCs, IAM roles, 
and clusters is prone to human error. One wrong 
click can lead to security holes or broken 
networking.
"Snowflake" Servers: Manual setups are hard to 
replicate. If the cluster is deleted, it might take 
hours or days to rebuild it exactly as it was.
Scaling Issues: Without automation, scaling a team 
or an application requires constant manual 
intervention by DevOps engineers.
Cost Management: It is easy to accidentally leave 
expensive, non-free-tier instances running when 
building things manually.
✅ The Solution (The "DevOps Way")
Consistency: By using Terraform, the infrastructure 
is documented as code. Running the code twice 
results in the exact same environment.
Automation: Using GitHub Actions, every time a 
change is pushed to the main branch, the 
infrastructure updates automatically.
Self-Healing: The project uses EKS Node Groups, 
which automatically replace any worker server that 
becomes unhealthy.
Efficiency: We optimized the cluster to use t3.micro 
instances, ensuring the project remains within the 
AWS Free Tier while still providing a full 
Kubernetes experience.
🛠 Tech Stack
Cloud: AWS (VPC, EKS, IAM, S3, EC2)
IaC: Terraform
CI/CD: GitHub Actions
Orchestration: Kubernetes (EKS)
CLI Tools: kubectl, aws-cli, terraform-cli
🚀 Step-by-Step Implementation
Phase 1: Local Setup
Initialized a Git repository and connected it to 
GitHub.
Configured AWS credentials locally and as GitHub 
Secrets for security.
Installed kubectl to interact with the future 
cluster.
Phase 2: Infrastructure as Code (Terraform)
Backend: Configured an S3 bucket to store the 
terraform.tfstate file, allowing for collaborative 
work and state persistence.
Networking: Created a custom VPC with public subnets 
across multiple Availability Zones in eu-west-2 
(London).
Security: Defined IAM Roles and Policies for both 
the EKS Cluster and the Worker Nodes.
Compute: Provisioned the EKS Control Plane and a 
Managed Node Group using t3.micro instances.
Phase 3: Automation (The Pipeline)
Created a GitHub Actions workflow (terraform.yml).
Automated the terraform init, plan, and apply steps.
Implemented a fix to ensure all resources remain 
within the AWS Free Tier.
Phase 4: Verification
Connected the local machine to the cluster using:
aws eks update-kubeconfig --region eu-west-2 --name 
levichuks-eks
Verified cluster health with kubectl get nodes and 
kubectl get pods -A.
📊 Results
Infrastructure Uptime: 99.9% (Managed by AWS EKS).
Deployment Speed: Fresh infrastructure is ready in 
~20 minutes; updates take <2 minutes.
Scalability: The cluster is configured to scale from 
1 to 3 nodes automatically.
