# Cortex Cloud Hands-On Lab for Posture & Runtime Security
## Cortex Cloud Runtime Security
As part of this lab, a vulnerable deployment has already been deployed as part of the initial terraform script. To check out what are the items deployed, refer to the CDR YAML manifest [here](https://github.com/hankthebldr/CDR/blob/master/cdr.yml). 

Cortex Cloud uses [Precision AI™](https://www.paloaltonetworks.com/blog/security-operations/smartgrouping-precision-ai-driven-investigation/) to automatically group related alerts into incidents. The resulting incidents are given a severity rating based on the highest severity alert contained within the incident, as well as an incident score based on feature extraction from the grouped alerts in order to help analysts prioritize their response efforts.

Take a moment to review any incidents that were created as a result of running the attack script. While SmartGrouping generally does a very good job of automatically grouping related events, there may still be multiple separate incidents created. Pay close attention to the following details:
    * How many incidents were created?
    * What is the severity level of the incidents?
    * What is the incident score of the incidents?
    * How many alerts does each incident contain?
        * What are the sources of those alerts?
    * How many different MITRE ATT&CK Tactics were identified?
    * What assets were identified?
        * How many endpoints?
        * How many user accounts?
        * Are there any malicious artifacts?
        * What groups do the hosts and users belong to?

### Incident management
After doing some initial triage and seeing that there is very clearly malicious activity, it’s time to take ownership of the incident(s) and begin an investigation.

Note: Cortex Cloud intelligently group related activity into a single incident. In environments where multiple labs are using the same shared tenant, there may be situations where incidents span multiple individuals’ Kubernetes nodes. In a shared tenant, you can find your own specific alerts by performing the following steps:
1. Navigate to Cases & Issues > Cases. Click on the filters at the top (Status = New, Under Investigation, etc), click +AND, then add a filter for Host, and filter down to the host name. 

2. This should show you a list of incidents that involve your endpoints. If the case only shows your assets on the Cases page, use the [Admin Guide](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Pro-Administrator-Guide/Manage-Incidents) to assign the incident to yourself. 

3. If the case shows assets from other users combined with yours, go into the Issues & Insights tab on the Cases page.

4. Click the Filter icon in the Host column to add a filter for your nodes.

5. Click the check box at the top left of the table to select all issues.

6. Right-click on one of the issues and select Create Case.

7. Select Security for Case Domain, give it a name and choose Critical for Severity. Indicate a description, and choose the existing issues. On Issue Details, make sure "Choose existing issue/s" is ticked and the issues are selected, and click Create New Case.
![](/resources/cc-11.png?raw=true)

### Incident investigation
Now that you’ve taken ownership of the incident, start reviewing the details of the alerts.
1. Using the [Admin Guide](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Pro-Administrator-Guide/Investigate-Artifacts-and-Assets), investigate the Artifacts and Assets contained within the incidents
    * Review the Asset View of the identified hosts
    * Review the Host Risk View of the identified hosts
    * Review the WildFire Analysis Reports of any malicious artifacts
2. Using the [Admin Guide](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Pro-Administrator-Guide/Investigate-Alerts), investigate the alerts in the incidents
3. Using the [Admin Guide](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Pro-Administrator-Guide/Causality-View), review the Causalities from the Executions tab of the incidents

### Threat hunting
After reviewing the Causalities, certain indicators may stand out. Depending on the incident you review, you may see a malicious file virus.sh, a malicious process named xmrig, or a number of other suspicious artifacts.

Using the Query Builder, you can hunt for other activity involving these indicators using simple search functionality.

1. Navigate to Incident Response -> Investigation -> Query Builder.
2. Click on File to create a query on file activity
3. In the NAME field, enter the file name you’re searching for. If you’re searching for file activity related to a process, click the +PROCESS link to enter the process name. Notice that you can add additional query criteria, including limiting the search to specific hosts.
4. Set the TIME period to ensure you cover the time period of when you ran your attacks. By default, the search is for the past 24 hours.
5. Click Run to execute the query
6. Review the results, and experiment with different queries based on the information from your incidents

As part of the initial XDR agent policy & profile configuration, you should see most of the issues are "Detected". In actual production environment, we should have the policy and profile to be set as "Prevent", so that all these threat can be prevented before damage is done in the environment. 


### Threat Prevention
Now you have experience how the XDR agent would "detect" the threat. How about changing the profiles to prevention now?
1. On The Cortex Cloud tenant, look into the Exploitation and Malware profile that you have created, change all the settings to "Prevent", and save it. Give it a few minutes for the agent to be updated.
2. Look into the same case again, notice the action of the issues.
3. On the AWS Cloudshell, run the following command, and check out the pods
    ```
    kubectl get pods -A
    ```
Do you notice any difference as per compared to before?

This lab does not include Threat Response and Automation which can be configured in Cortex Cloud. This will be added in the future!

Once you have verified the issues and cases, move on to the next section [here](/08-CortexCloudAppSec.md)!

