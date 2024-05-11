# Project-01: Create and Manage AWS Cloud Infrastructure using Terraform (as IaC) and Jenkins (CI)

<<<<<<< HEAD
The project details are moved to here: https://github.com/kbindesh/aws-infra-tf-jenkins-project
=======
<img src="images/iacwithtfandjenkins.png" width="650" height="440">

## Prerequisites

- [AWS Account](https://aws.amazon.com/free/)
- IDE
  - [Visual Studio Code](https://code.visualstudio.com/download)
- Install VS Code Extensions (Terraform, terraform-lint)
- [Git](https://git-scm.com/downloads)
- [Terraform]()
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

## Step-01: Develop and Test Terraform scripts (on local system)

### 1.1 Develop TF scripts

- Refer to the [tf-manifests](./tf-manifests/) folder for all the terraform scripts to be deployed.

### 1.2 Test the TF scripts locally

```
# Get inside the terraform script folder
cd tf-manifests

# Initialize the directory as a Terraform dir
terraform init

# Validate the Terraform scripts
terraform validate

# Generate the Terraform script plan
terraform plan

# Execute the Terraform scripts to provision AWS resources
terraform apply --auto-approve
```

- If everything looks good, delete all the created resources by running below command as we will be automating resource provisioning using Jenkins in later steps:

```
terraform destroy --auto-approve
```

### 1.3 Create a new remote repository in Github (for this lab)

- Create a new repo with atleast three branches, namely:
  - Development
  - Testing
  - Production

### 1.4 Check-in the code to SCM (Github)

- Create a new Github repository.
- Check-in the code on **feature branch**.
- Create a PR to merge the changes on Development/Integration branch.
- Approve the PR request and verify the changes on Development branch.

## Step-02: Setup the Jenkins Server (EC2 Instance/VM)

### 2.1 Provision an EC2 Instance

- **AMI**: Amazon Linux 2 (you can have any other OS)
- **Instance Type**: t2.micro
- **VPC & Subnet**: Default
- **Public IP**: Enabled
- **Security Group**: Allow Ingress traffic on SSH(22) and 8080
- **Storage**: Root Volume(at least 10GB)

### 2.2 Install and Configure Jenkins

- Connect to Jenkins server
- Configure Jenkins **On Amazon Linux 2 EC2 Instance**

```
#!/bin/bash
yum install -y java-17-amazon-corretto.x86_64
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
yum -y upgrade
yum install -y jenkins
systemctl start jenkins
systemctl enable jenkins
```

- **On other platforms**

- Refer to this link: https://www.jenkins.io/doc/book/installing/

### 2.3 Create IAM Credentials for Jenkins Server to provision Infra in AWS

### 2.4 Save the IAM Credentials on Jenkins server

### 2.5 Create a new Github Webhook for triggering Jenkins jobs

- Navigate to the Github repo created in **Step# 1.3**
- Go to **Setting** tab >> **Webhooks** >> **Add Webhook**
- **Payload URL**: https://<your_jenkins_server_public_ip_or_dns>:8080/github-webhook/
- **Content type**: application/json
- **Which events would you like to trigger this webhook?** : Let me select individual events >> Select **Pull requests** and **Pushes** checkboxes
- Check the **Active** checkbox >> **Create Webhook**

### 2.6 Install and Configure Terraform

```
# On Amazon Linux 2 (AMI)
sudo yum install -y yum-utils shadow-utils

sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo

sudo yum -y install terraform
```

- For more details, refer https://developer.hashicorp.com/terraform/install

### 2.7 Download and Install Git

```
# On Amazon Linux 2
sudo yum install -y git
```

- Refer to this link: https://git-scm.com/downloads

## Step-03: Create a Jenkins Job (Pipeline | event based)

### 3.1 Create a new Jenkins job of type Pipeline

### 3.2 Test the Jenkins job manually

## Step-04: Write a Jenkinsfile for infra deployment using Terraform

### 4.1 Create a Jenkinsfile (on local system)

### 4.2 Check-in the code to SCM (Github)

### 4.3 Validate the Jenkins job execution and AWS infrastructure creation
>>>>>>> 262aff8e01591f86f9b60c9ec01dbe235a0950b0