# Cortex Cloud Hands-On Lab for Posture & Runtime Security
## Clean Up
This is the last section of the Cortex Cloud Hands-On Lab. You can choose to play around with the vulnerable infrastructure generated. However, it is always recommended to clean things up, so that it doesn't cost your AWS account(s) more money. Both Cortex Cloud integration and the vulnerable infrastructure cost you money!

### Clean Up AWS Vulnerable Infrastructure
1. Go to AWS Cloudshell, make sure you're in the same terraform folder (eg. `aws-vul-infra`) that you have provisioned the infrastructure, run the following:
    ```
    terraform destroy --auto-approve
    ```

2. It will take some time for the resources to be deleted completely. If you're seeing some errors, you might need to delete the resource(s) manually through AWS Management Console. 


### Clean Up Cortex Cloud Integration
1. Go to AWS Management Console > CloudFormation. Find the stack that you have created (eg. `bechong-ccr-app`), and delete it.

2. It will also take some time for the CloudFormation to be deleted completely. If you're seeing some errors, you might need to delete the resource(s) manually through AWS Management Console.


### Clean Up on Cortex Cloud 
1. Go to Cortex Cloud, delete and remove the following:
    * Agent installation
    * Policy
    * Profiles


I hope the lab is useful for team, feel free to feedback to the instructor, for any improvement or suggestion!