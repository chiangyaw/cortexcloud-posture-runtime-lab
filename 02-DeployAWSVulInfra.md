# Cortex Cloud Hands-On Lab for Posture & Runtime Security
## Deploy AWS Vulnerable Infrastructure
Before we move on to Cortex Cloud, we will first need to deploy the AWS vulnerable infrastructure via ```terraform```. It will take a couple of minutes for the infrastructure completely. You can move on to the next section while waiting. These are the resources that will be provisioned by the terraform script used for this lab:
- EKS Cluster
- Ubuntu EC2 Instance
- S3 Bucket with sensitive data
- Keypair to access the Ubuntu EC2 instance
- Required network infrastructure, including VPC, subnet, route table, security group, etc
- Required IAM roles for access and provisioning

1. Git clone the terraform script to your AWS Cloudshell local directory:
    ```
    git clone https://github.com/chiangyaw/aws-vul-infra-setup.git
    cd aws-vul-infra-setup
    ```

2. Initialize Terraform:
    ```
    terraform init
    ```

3. Here is the addtional part you will need to know. As part of this lab, you will need to know and define the following:
    - Your prefix: This is required for you to identify your resources, as most of the resources will have this prefix added in front of the resource name. For example, ```<prefix>-ubuntu-instance```. Also, if you're sharing the AWS account with someone else, this is required so that it will not affect other member's deployment, as some of the resources must have unique names, especially global resources.
    - Region: most of your resources will be deployed in a single region. ```aws-vul-infra-setup``` is coded with ```ap-southeast-2```. If you're sharing the AWS account with your team member, I would recommend to pick one region per member, so that you won't be seeing other team members' resource when you're running through this lab.

4. Once you have those details in place, you will need to proceed to apply the terraform script with the following:
    ```
    terraform apply \
    -var "unique_prefix=<XXX>" \
    -var "region=<XXX> \
    --auto-approve
    ```

5. You should see Terraform creating the resources slowly. It will take a couple of minutes for the infrastructure to be provisioned completely. 

You can move on to the next section while waiting. Click [here] to the next section.