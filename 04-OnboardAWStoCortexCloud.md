# Cortex Cloud Hands-On Lab for Posture & Runtime Security
## Onboarding AWS Account to Cortex Cloud for Posture Security
One of the key capabilities that Cortex Cloud offer would be Posture Security. Cortex Cloud Posture Security conolidate cloud security posture tools into a single unified platform, offering capabilities such as:
* Cloud Security Posture Management (CSPM)
* Cloud Infrastructure Entitlement Management (CIEM)
* Agentless Disk Scanning (ADS)
* Vulnerability Management
* Data Security Posture Management (DSPM)
* AI Security Posture Management (AI-SPM)
* CI/CD Security
* Application Security Posture Management (ASPM)
With different security capabilities, Cortex Cloud is able to provide AI-driven detection and prioritization, helping to consolidate numerous alerts into a fully contextualized, high-priority case. The context spanning across code, cloud and runtime keep the team focused on the important risks. 

As part of this lab, you will learn how to onboard your AWS account to Cortex Cloud, with these features enabled. 

1. On Cortex Cloud, go to Settings > Data Sources. Click on Add Data Source.
![](/resources/cc-02.png?raw=true)

2. Click on Amazon Web Services (AWS) and Connect Another Instance.
![](/resources/cc-03.png?raw=true)

3. Choose Account under Scope, leave Scan Mode as Cloud Scan, click on Show advanced settings. Indicate a Instance Name so that you easily identify your AWS account later. Under Additional Security Capabilties, make sure you tick all of them (including Data security posture management). Then, click Save.
![](/resources/cc-04.png?raw=true)
![](/resources/cc-05.png?raw=true)

4. On the next page, you can choose to execute it directly in AWS or Download the CloudFormation template. In this lab, we will choose to execute directly on AWS.
![](/resources/cc-06.png?raw=true)

5. Once you click on "Execute in AWS", you will be redirect to AWS console in a new tab. Make sure you're in the correct region. If you're not, switch it to your selected region. Indicate a stack name (eg. `bechong-ccr-app`), tick on "I acknowledge .....", and click Create Stack.
![](/resources/cc-07.png?raw=true)
![](/resources/cc-08.png?raw=true)

6. The CloudFormation stack will typically take 5-10 minutes to complete the deployment. In the meantime if you head back to Cortex Cloud page, it will show as "connecting". Once the CloudFormation stack is deployed successfully, the integration with Cortex Cloud is done completely.

Note: The data ingestion to Cortex Cloud will take some time. For the data to be fully populated, including vulnerability information and attack path analysis, it will take up to 24 hours for the initial ingestion. If you have the time, you can come back and look into the Issues generated the next day. If not, your instructor has probably simulated some issues on Cortex Cloud for you to take a look

### Troubleshooting
There would be situation where your Cloudformation stack will be be on "Rollback" status, due to deployment failure. This is most likely due to having a single AWS account shared across different team members. To rectify this, re-run the onboarding procedure, and untick "Collect Audit Logs (CloudTrail)".
![](/resources/cc-09.png?raw=true)

Click [here](/05-CortexCloudPostureSecurity.md) to move to the next section!