🧠 Basic Terraform Interview Questions
1. What is Terraform?

Terraform is an open-source Infrastructure as Code (IaC) tool that lets you define and provision infrastructure using declarative configuration files.

2. Difference between Terraform and Ansible/Puppet/Chef?
   
<pre>Feature	          |         Terraform	                     |              Ansible
Type	             |     IaC (Provisioning)	               |        Configuration Management

Language 	       |    HCL (Declarative)	                  |         YAML (Procedural)

Execution	       |    Creates immutable infrastructure	   |         Manages existing infrastructure

State Management	 |  Yes (terraform.tfstate)	             |          No</pre>

4. What is Terraform State File?

It’s a local or remote file (terraform.tfstate) that keeps track of the real-world infrastructure Terraform manages.

4. What are Providers in Terraform?

Providers are plugins used to interact with cloud platforms (AWS, Azure, GCP, etc.) or services (GitHub, Kubernetes).

Example:

<pre> provider "aws" {
  region = "us-east-1"
} </pre>

5. What is Terraform Plan and Apply?

terraform plan: Previews changes before applying them.

terraform apply: Executes the planned actions to create/update resources.

⚙️ Intermediate Questions

6. What are Variables and Outputs in Terraform?

Variables make configurations dynamic; outputs display useful information after deployment.

Example:

<pre>variable "instance_type" {
  default = "t2.micro"
}
output "instance_ip" {
  value = aws_instance.web.public_ip
}</pre>

7. What is a Terraform Module?

A reusable set of Terraform configurations.

Example: A module for EC2 + Security Group + KeyPair used across environments.

8. What is Terraform Workspace?

Workspaces allow multiple environments (dev, test, prod) using the same configuration but separate state files.

🧩 Scenario-Based Questions

9. Scenario 1:

You deployed an EC2 instance using Terraform. Later, someone manually terminated it in AWS. What happens when you run terraform apply again?

✅ Terraform detects the resource is missing and recreates it to match the configuration.

10. Scenario 2:

You updated an S3 bucket name in Terraform code. What will Terraform do on apply?

✅ Since S3 bucket names are immutable, Terraform will destroy the old bucket and create a new one, possibly losing data unless versioning or import is handled carefully.

11. Scenario 3:

How do you manage sensitive data like passwords or access keys in Terraform?

✅ Use:

Environment variables (TF_VAR_)

Encrypted storage (Vault, AWS Secrets Manager)

.tfvars files (excluded from Git using .gitignore)

sensitive = true in variable definition

12. Scenario 4:

You have multiple developers working with Terraform. How do you avoid conflicts in the state file?

✅ Use remote backend (e.g., S3 + DynamoDB for state locking):

<pre>backend "s3" {
  bucket         = "my-terraform-state"
  key            = "dev/terraform.tfstate"
  region         = "us-east-1"
  dynamodb_table = "terraform-lock"
}</pre>

13. Scenario 5:

How do you import existing AWS resources into Terraform?

✅ Use:

terraform import aws_instance.my_ec2 i-1234567890abcdef


Then run terraform plan to verify it’s now tracked by Terraform.

14. Scenario 6:

You want to deploy the same infrastructure across multiple regions. How do you achieve that?

✅ Use modules and for_each or count:

<pre>variable "regions" {
  default = ["us-east-1", "us-west-2"]
}

module "servers" {
  for_each = toset(var.regions)
  source   = "./modules/ec2"
  region   = each.key
}</pre>

💡 Advanced & Real-World Scenarios

15. Scenario 7:

How do you handle version control in Terraform modules?

✅ Use a specific tag or commit in module source:

<pre>module "network" {
  source  = "git::https://github.com/myorg/network.git?ref=v1.0.0"
}</pre>

16. Scenario 8:

Terraform apply failed midway — some resources were created, others were not. What do you do?

✅ Steps:

Run terraform plan to see drift.

Fix code or state manually if necessary.

Re-run terraform apply.

If corrupted, use terraform state rm or terraform refresh.

17. Scenario 9:

How do you roll back infrastructure changes?

✅ Terraform doesn’t have a direct rollback command.

You need to:

Restore a previous .tfstate version (from S3 versioning, Git, etc.)

Run terraform apply again to revert to that state.

18. Scenario 10:

How do you make Terraform configurations reusable and modular for multiple projects?

✅ Use:

Root modules for each environment.

Child modules for specific resources.

Variable files (dev.tfvars, prod.tfvars) to switch configurations.

🔐 Terraform Best Practices

Always use remote backend with locking.

Keep state files encrypted.

Use modules for DRY principle.

Run terraform fmt and terraform validate before applying.

Version your providers and modules for consistency.
