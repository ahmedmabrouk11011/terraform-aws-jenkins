# Provisioning a Jenkins Server on AWS with Terraform

#### Here is the architecture diagram for what this Terraform project creates
![Custom VPC architecture for AWS](https://cdn-images-1.medium.com/max/800/1*o8O9e6Q1Rd-pG3qmnC4o_w.png)

## Prerequisites
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) installed and configuration
- [Terraform](https://www.terraform.io/downloads) installed

# Instructions

### Step 1: Create a values file
Create a file called **terraform.tfvars** and populate it with: `my_ip="0.0.0.0"` with 0.0.0.0 being your IP address [Get My IP Address](https://whatismyipaddress.com/)


### Step 2: Create a Key Pair
`ssh-keygen -t rsa -b 4096 -m pem -f tutorial_kp && mv tutorial_kp.pub modules/compute/tutorial_kp.pub && mv tutorial_kp tutorial_kp.pem && chmod 400 tutorial_kp.pem`


### Step 3: Run Terraform
- Initialize terrafom: `terraform init`
- Run: `terraform apply`
- When prompted, enter: `yes`


### Step 4: To SSH into the Jenkins Server
`ssh -i tutorial_kp.pem ubuntu@$(terraform output -raw jenkins_public_ip)`


### Step 5: Get the Jenkins Server intial password
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`


### Step 6: To destroy everything Terraform built
- Run: `terraform destroy`
- When prompted, enter: `yes`
