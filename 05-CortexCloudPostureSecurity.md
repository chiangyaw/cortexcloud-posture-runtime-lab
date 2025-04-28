# Cortex Cloud Hands-On Lab for Posture & Runtime Security
## Onboarding AWS Account to Cortex Cloud for Posture Security
As mentioned on the previous section, Cortex Cloud Posture Security focuses on providing the visibility of your cloud estate, detecting different security risks with different factors, using AI-driven detection and prioritization, helping to consolidate numerous alerts into a fully contextualized, high-priority case. The context spanning across code, cloud and runtime keep the team focused on the important risks. 

In this section, you will be exploring the security issues detected based on the AWS vulnerable infrastructure that you have deployed, and how prioritization works in Cortex Cloud.

Note: The data ingestion to Cortex Cloud will take some time. For the data to be fully populated, including vulnerability information and attack path analysis, it will take up to 24 hours for the initial ingestion. If you have the time, you can come back and look into the Issues generated the next day. If not, your instructor has probably simulated some issues on Cortex Cloud for you to take a look

### Posture Case Investigation
1. On Cortex Cloud, go to Cases & Issues > Cases. Change the filter to Posture Domain.
![](/resources/cc-12.png?raw=true)

2. Run through the list of cases created on Cortex Cloud, and check whether there is any cases created for the AWS vulnerable infrastructure that you have deployed. Filter to the host if require.

3. You should see a posture case created for the ubuntu EC2 instance which you have deployed as part of the AWS vulnerable infrastructure, with the prefix that you have included. If not, do check with your instructor for any other cases identified.

4. In the Posture case identified, you should see a number of issues grouped in a single case. This is part of the prioritization capabilities in Cortex Cloud. Cortex Cloud help to identify related issues, and group them together in a single case, so that this case gets assigned to a single security engineer/analyst to work things out.

5. Click on the case, and click on the Issues & Insights tab. Run through the issues that were identified. The issues are all related to a single EC2 instance, where different findings increased the overall risks of the asset. 
![](/resources/cc-13.png?raw=true)

6. Click on the issue "Data exfiltration risk due to a publicly exposed AWS EC2 instance with s3:GetObject and s3:ListBucket permissions and not configured to use Metadata Service v2 (IMDSv2)". Run through the description and evidence, explaining why this is a critical risk. 
![](/resources/cc-14.png?raw=true)

Note: The Attack Path policies are out-of-the-box policies that are enabled by default. These policies identify the confluence of issues that increase the likelihood of a security breach and are based on relationships such as, overly permissive identities, permissions, network exposure, infrastructure misconfiguration, and vulnerabilities that would enable an attacker to target your application. This helps security engineer/analyst to prioritize risks as part of their day to day operation.

7. Click on Actions tab, and run through the findings. The Actions tab provides recommendation to reduce the overall risk on the issue. As part of this example, it is recommended to enable IMDSv2 on the AWS EC2 instance, which enables session-oriented authentication, requiring a token to be obtained before accessing instance metadata, making it harder for attackers to exploit misconfigurations or vulnerabilities to access sensitive data. The recommendation provided comes in different form factors, you can either change your terraform code to have it updated, make changes via AWS Management Console or run a simple CLI command on your AWS Cloudshell. 
![](/resources/cc-15.png?raw=true)


8. Close off the Issue tab, and move back to the Case. Click on Key Assets & Artifacts. Click on the asset in the asset list. The asset tab gives you an overview of the asset involved in the case. In this tab, you can look into the key highlights of the asset, and also properties such as IPs, VM images, cloud region, etc for further investigation. 
![](/resources/cc-16.png?raw=true)

Note: The screenshot below is taken from an asset with XDR agent installed. The information that you're seeing on provisioned EC2 instance with your prefix might be a bit different, especially on the Scan Information part.

9. Click on Vulnerabilities tab, and run through the vulnerabilities found on this asset. You can also add on filters to check on a specific CVE or CVSS score.
![](/resources/cc-17.png?raw=true)

10. Click on the Access tab. This tab gives you an overview on the identity access for this asset. On the "Where can this identity access?", you can also check on what are the excessive permissions granted for the asset, and not being utilized during the tracking period. This allows the security engineer/analyst to understand whether the asset has been granted with overly permissive permission, and recommending least privilege access.
![](/resources/cc-18.png?raw=true)
![](/resources/cc-19.png?raw=true)

The further details provided as part of the findings would help the security engineer/analyst to further reduce the overall risks of the asset.

### Vulnerability Management
Vulnerability Management is one of the key responsibility of cloud security engineers. Software vulnerabilities contributed to a large sum of attacks on cloud native application. Cortex Cloud helps to detect, prioritize and remediate vulnerabilities from code to cloud on a unified platform. 

Note: As part of this lab, it will only cover vulnerability discovered in Runtime / Posture. 

1. On the side menu, click on Posture Management > Vulnerability Management > Vulnerability Issues. You can see the number of vulnerability issues for the monitored assets within Cortex Cloud. Click into the "Fix Available". This will help to filter down to the vulnerability issues that are Critical & High, with Weaponized Exploit, and has Fix Available.
![](/resources/cc-20.png?raw=true)

Note: Why this is important? In typical production cloud environment with cloud native applications, you will usually see tons of vulnerabilities in different part of the applications. The ideal case is to have 0 vulnerability, but organization rarely able to achieve that, unless they don't use any OSS. Hence, having the right focus on vulnerabilities that are important is key. With this filter, security engineer or analyst is able to focus on the higher prioritized vulnerabilities, so that they can get it patched or fixed before it gets exploited by the attackers.

2. Click on any of the CVE in the list, run through the details mentioned in the side popped out window.

3. On the existing Vulnerability Issues table, scroll towards the right, look into the different findings on that particular CVE, and the fix versions.
![](/resources/cc-21.png?raw=true)

The information listed can be exported out as a CSV as well with Query Builder, which is customizable. 


Cortex Cloud Posture Security looks into different aspect of cloud visibility. More content on DSPM, AI-SPM, and ASPM coming soon!

Move on to the next section [here](/06-CortexCloudXDRAgent.md)!