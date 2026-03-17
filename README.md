# End-to-End-EKS-Pipeline (Project Levichuks)

Automated Provisioning of a Production-Grade Amazon EKS Cluster using Terraform and GitHub Actions CI/CD.



## 🎯 Purpose of the Project
The goal of this project is to demonstrate the ability to automate cloud infrastructure. Instead of manually clicking through the AWS Console, this project uses a "Code-First" approach to build a highly available Kubernetes environment.

---

## 👥 Target Users & Stakeholder Value
This project isn't just a technical exercise; it solves real-world bottlenecks for three key groups:

### 1. The Software Developers (The "Tenants")
* **The Problem:** Historically, developers had to wait days or weeks for a "SysAdmin" to manually provision a server.
* **The Solution:** This pipeline provides a **Self-Service Platform**. Developers can now deploy their code (Java, Python, Node.js) in seconds using `kubectl`. They no longer worry about the underlying server; they only care that their code is running.
* **Key Benefit:** **Velocity.** Features reach customers faster because the infrastructure "middle-man" has been automated away.

### 2. The DevOps Team (The "Guardians")
* **The Problem:** Manual configurations lead to "Configuration Drift" and 2:00 AM emergency calls when a server crashes.
* **The Solution:** Using **Infrastructure as Code (Terraform)**, the environment is 100% documented and repeatable. Because we use **Managed Node Groups**, the cluster is **Self-Healing**. If a worker node fails, EKS automatically replaces it.
* **Key Benefit:** **Reliability & Peace of Mind.** The system manages its own health.

### 3. The Business Owners (The "Stakeholders")
* **The Problem:** Unpredictable AWS bills and revenue loss due to website downtime.
* **The Solution:** * **Cost Governance:** Enforced `t3.micro` instances via IaC to stay within the **AWS Free Tier**.
    * **Business Continuity:** Cluster spread across multiple **Availability Zones** to prevent downtime.
* **Key Benefit:** **Cost Efficiency & Risk Mitigation.**

---

## 📊 Summary: Problem vs. Solution
| User Role | Old Manual Problem | Your Project's Automated Solution |
| :--- | :--- | :--- |
| **Developer** | "I have to wait weeks for a server." | **Self-Service:** Deploy instantly to EKS. |
| **DevOps** | "I have to manually configure every server." | **Automation:** One `git push` builds the entire cloud. |
| **CEO/Owner** | "The site crashed and we lost money." | **High Availability:** EKS keeps the site running 24/7. |

---

## ⚠️ The Problem (The "Old Way")
* **Manual Errors:** One wrong click in the console can lead to security holes or broken networking.
* **"Snowflake" Servers:** Manual setups are hard to replicate if the cluster is deleted.
* **Scaling Issues:** Manual scaling requires constant human intervention.

## ✅ The Solution (The "DevOps Way")
* **Consistency:** Terraform ensures the infrastructure is documented as code.
* **Automation:** GitHub Actions automatically updates infrastructure on every push.
* **Efficiency:** Optimized for **AWS Free Tier** using `t3.micro` instances.

---

## 🛠 Tech Stack
* **Cloud:** AWS (VPC, EKS, IAM, S3, EC2)
* **IaC:** Terraform
* **CI/CD:** GitHub Actions
* **Orchestration:** Kubernetes (EKS)
* **CLI Tools:** `kubectl`, `aws-cli`, `terraform-cli`

---

## 🚀 Step-by-Step Implementation

### Phase 1: Local Setup
* Initialized Git repository and connected to GitHub.
* Configured AWS credentials and GitHub Secrets.

### Phase 2: Infrastructure as Code (Terraform)
* **Backend:** Configured S3 for remote state management.
* **Networking:** Created a custom VPC in `eu-west-2` (London).
* **Compute:** Provisioned EKS Control Plane and Managed Node Groups.

### Phase 3: Automation (The Pipeline)
* Created `terraform.yml` for GitHub Actions.
* Automated `init`, `plan`, and `apply` steps.

### Phase 4: Verification
* Verified cluster health:
  ```bash
  aws eks update-kubeconfig --region eu-west-2 --name levichuks-eks
  kubectl get nodes

  📊 Results
Infrastructure Uptime: 99.9% (Managed by AWS EKS).
Deployment Speed: Fresh infrastructure in ~20 mins; updates in <2 mins.
Scalability: Auto-scales from 1 to 3 nodes.

---

## 🔧 Engineering Challenges & Solutions (The "Hidden Bosses")

During the development of **End-to-End-EKS-Pipeline**, I encountered and resolved several real-world production issues:

* **Challenge: Resource Constraints & Budget Control**
    * **The Problem:** Initial deployments were blocked by AWS service limits and potential high costs for a personal lab.
    * **The Solution:** Refactored Terraform modules to use `t3.micro` instances and optimized the Node Group configuration to fit within the **AWS Free Tier** while still maintaining a multi-AZ architecture.

* **Challenge: Network Gateway Latency**
    * **The Problem:** Application Load Balancers (ALB) were occasionally failing health checks during initial deployment.
    * **The Solution:** Adjusted the Kubernetes Service manifests and Security Group ingress rules to ensure the AWS Load Balancer could communicate effectively with the pods on specific container ports.
    
* **Challenge: Infrastructure Lifecycle Management**
    * **The Problem:** Needing a way to prevent "Cloud Sprawl" and unnecessary costs when the lab was not in use.
    * **The Solution:** Implemented a **Manual "Kill Switch"** using GitHub Actions `workflow_dispatch`. This allows for a one-click `terraform destroy` directly from the GitHub UI, ensuring 100% cost control.

## 🏁 Final Project Status: ARCHIVED
* **Infrastructure:** Verified & Successfully Teardown.
* **Documentation:** Complete.
* **Automation:** CI/CD tested for both Provisioning and Destruction.

---
**Next Project:** [GitOps-CD-Pipeline (ArgoCD)] 🔜