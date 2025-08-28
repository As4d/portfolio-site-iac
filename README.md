# Portfolio Site Infrastructure as Code (IaC) + Agile Methodologies

## **Overview:**
This project documents the setup of my personal portfolio site on AWS.

---

## **Key Agile Practices Implemented:**

- **Epics:** Major project phases:  
  1. Domain & DNS Setup  
  2. Terraform Cloud Setup
  3. S3 Static Website Hosting

![Epic Example](docs/jira-epic.png)

- **Kanban Board:** Tracked tasks through **To Do → In Progress → Done**.  

![Jira Board Example](docs/jira-board.png)

---

## **Tasks:**

### 1. Buy Domain & Configure Route 53
**Task:** Register domain and set up hosted zone for DNS management.  
**Approach:** Purchased domain through Route 53 and documented NS records.  
**Outcome:** Domain successfully registered and ready for AWS services.  

![Route 53 Domain](docs/register-domain.png)  
![Route 53 NS Records](docs/route53-ns.png)

---

### 2. Terraform Cloud Setup
**Task:** Set up Terraform Cloud for managing infrastructure as code.
**Approach:** Created account, create organization, set up workspace, connected to GitHub repo.
**Outcome:** Terraform Cloud workspace ready for managing AWS resources.

![Terraform Cloud Workspace](docs/terraform-cloud.png)

Added the AWS access keys as environment variables in Terraform Cloud for authentication.

![Terraform Cloud Access Keys](docs/terraform-cloud-workspace-access-keys.png)

Tested Terraform Cloud by running a simple plan to ensure connectivity and configuration. I used the following Terraform code:

```[hcl]
provider "aws" {
  region = "eu-west-2" // london
}

resource "aws_vpc" "test" {
  cidr_block = "10.0.0.0/16"
} 
```

![Terraform Cloud Plan](docs/terraform-cloud-test-plan.png)

Successfully applied the plan to create the VPC and saved the state securely in Terraform Cloud.

![Terraform Cloud Apply](docs/terraform-cloud-test-apply.png)

**State Management Test:**

I was curious to see how Terrform cloud handles the state file if i were to delete a resoure on the cloud. I deleted the VPC from the AWS console and then ran another plan in Terraform Cloud. 

![AWS Console VPC Deletion](docs/delete-test-vpc-via-console.png)

As expected, Terraform detected that the VPC was missing and planned to recreate it. It does this as Terraforms plan command compares the current state of the infrastructure (as recorded in the state file) with the desired state defined in the configuration files.

![Terraform Cloud Plan After Deletion](docs/terraform-cloud-test-state.png)

