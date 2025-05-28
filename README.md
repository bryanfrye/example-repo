# example-repo

Example repo generated via repo-deploy

**Cloud Provider:** aws  
**Selected Linters:** yaml,cloudformation,cfn-nag

# example-repo

This is a test infrastructure-as-code (IaC) repository that demonstrates the deployment, configuration, and full lifecycle management of a secure LAMP stack hosted in AWS.

## Overview

This repo provisions the following resources:

- **2× EC2 Instances** (`t3.micro`) across multiple subnets
- **Security Groups** allowing secured HTTPS traffic
- **Application Load Balancer (ALB)** with:
  - HTTP (80) redirecting to HTTPS (443)
  - HTTPS forwarding to EC2 Target Group
- **CloudFormation Templates** for infrastructure provisioning
- **Ansible Playbooks** for instance configuration and LAMP setup

Once provisioned, EC2 instances are automatically configured using Ansible to run a hardened and monitored LAMP stack, providing a complete, production-style deployment workflow.

## Goals

This repo is designed to demonstrate:

- End-to-end AWS provisioning with CloudFormation
- Configuration management using Ansible
- Secure-by-default deployments (HTTPS, SGs, minimal access)
- Observability via logging and monitoring hooks (TBD)
- Repo-scoped IaC structure with CI/CD pipeline hooks

## Structure
```bash
├── deploy/
│   ├── cloudformation/        # CloudFormation templates
│   └── parameters/            # Parameter files for stacks
├── scripts/                   # Shell scripts (linting, deployment, etc)
├── ansible/                   # Playbooks and roles (planned)
├── .github/
│   └── workflows/             # GitHub Actions CI/CD
├── .linters                   # Enabled linters for CI
├── .repo-deploy-version       # Tracked repo-deploy version
└── Makefile                   # Local runner commands
```

## Deployment
To test deployment locally before commiting, you can use the provided Makefile commands:
```bash
make lint - verify the syntax of the CloudFormation templates and any other configured linters (yaml, cfn-nag, cfn-lint)
make deploy - deploy the CloudFormation stack using the templates in `deploy/cloudformation/` and any ansible playbooks in `scripts/ansible/`
make check-version - check the version of repo-deploy used to generate this repo
make update - update the repo to the latest version of repo-deploy pulling any changes to github workflows or pertinent files
```

## Prequisites:
- AWS CLI configured with appropriate permissions
- Ansible installed locally
- Python 3.x with `boto3` and `ansible` libraries installed
- Any linting tools installed (e.g., `cfn-lint`, `cfn-nag`, `yamllint` - scripts to install these are provided in the `scripts/` directory)
- Make utility installed
- GitHub Actions enabled for CI/CD workflows

## TODO
- [ ] Add Ansible playbooks for LAMP stack configuration
- [ ] Implement logging and monitoring hooks
- [ ] Add more comprehensive CI/CD workflows
- [ ] Document and implement security hardening steps
- [ ] Expand with additional resources (RDS, S3, etc.)
- [ ] Additional default parameter files for CloudFormation stacks to make deployment easier

## Additional TODO
- [ ] Azure and GCP support within the same repo-deploy structure
- [ ] Add additional IaC examples (e.g., Terraform, Pulumi)
- [ ] Add more complex CI/CD workflows (e.g., multi-stage deployments, blue-green deployments)
- [ ] Puppet/Bolt/Chef support for configuration management
- [ ] Add more comprehensive observability (e.g., CloudWatch, CloudTrail, ELK stack)
- [ ] Containerization support (e.g., Docker, Kubernetes)
