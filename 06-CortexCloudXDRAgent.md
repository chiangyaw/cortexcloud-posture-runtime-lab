# Cortex Cloud Hands-On Lab for Posture & Runtime Security
## Installing XDR Agent for Cortex Cloud
Cortex Cloud offers Runtime Security 


### Cortex XDR initial configuration
First, we’ll need to configure profiles that will control how the XDR agent behaves in the environment. Profiles are broken down by Platform (Operating System), then category (Malware, Exploit, Agent Settings, Restrictions, and Exceptions). Default profiles cannot be modified, so it’s considered a best practice to create new profiles even if you’re not initially changing any settings as it gives you something that you can modify later should it be necessary.

This lab will only cover installation on Kubernetes cluster (EKS). Do take note that Cortex Cloud runtime security supports Windows and Linux OS as well. 

As part of the steps below, make sure you put up a prefix (eg. `bechong-`) in the profiles, policies, etc that you're creating, so that can you identify them easily

1. Using the [Admin Guide](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Documentation/Set-up-malware-prevention-profiles), add a new Malware Security Profile for Linux. For every configuration where the default action is Block, set the action to Report (or Disabled if Report is not an option).
2. Using the [Admin Guide](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Documentation/Set-up-exploit-prevention-profiles), add a new Exploit Security Profile for Windows and Linux. Set all protections to Report instead of Block with the following exceptions:
    * Leave Exploit Protection for Additional Processes as Disabled (Windows and Linux)
    * Leave Unpatched Vulnerabilities Protection as Default (Windows)
3. Using the [Admin Guide](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Documentation/Set-up-agent-settings-profiles), add a new Agent Settings Profile for Windows and Linux. Leave the default configuration as-is with the following changes:
    * Enable the XDR Pro Endpoints Capabilities (Windows and Linux)
NOTE: The XDR Pro Endpoints Capabilities is what enables the EDR functionality with the agent and is disabled by default.

### Create Cortex XDR installers
Next, we’ll create installation packages that will be used on the endpoints inside the BYOS lab environment. Cortex XDR installation packages are tied to the tenant that created them, so these installers will always point back to your XDR tenant.

1. Using the [Admin Guide](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Documentation/Create-an-agent-installation-package), create a Linux Kubernetes installation package. 
    * Name: <your-prefix>-k8s-xdr
    * Package Type: Kubernetes Installer
    * Endpoint Tags: <your-prefix>
    * Always deploy the latest agent
    * Agent Daemonset Namespace: cortex-xdr
    * Run on master node
    * Run on all nodes
    * Deployment Platform: Standard
    * Download the YAML installer

### Create groups and policies
Once the profiles and installers have been created, we’ll create dynamic groups that we can use when configuring Policies in order to dynamically assign configuration based on specified filters.

1. Using the [Admin Guide](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Documentation/Define-endpoint-groups), add a Dynamic Group for your installers. Use filters for Endpoint Type to create each group (for example, Installation Package Contains `<prefix>-k8s-xdr`)

Once the group is defined, we can tie it all together with policies. Policies are a collection of Profile configurations applied to a Target (such as an endpoint group), and are broken down by Platform.

2. Using the Admin Guide, create a new Prevention Policy Rule using the newly created profiles and groups.
    * Create a Linux Policy Rule using your prefix targeting the dynamic group you just created (for example, `<prefix>-k8s-xdr-group`)

### Install the XDR Agent on the Kubernetes cluster
To install the XDR agent on the Kubernetes cluster (we're using EKS as part of this lab), you will need to deploy it via the YAML installer and `kubectl`, and you will be doing this with AWS Cloudshell. 

1. In your AWS management console, open up AWS Cloudshell. You can either upload the file that you have downloaded to AWS Cloudshell, or create a new file via `vi` and copy paste the content to the new file, and save it.

2. Once done, you will deploy the XDR agent with the following:
    ```
    aws eks update-kubeconfig --region <region> --name <cluster-name>
    kubectl apply -f <name_of_YAML_installer>.yaml
    ```

3. Verify in your Cortex Cloud console that you're seeing the EKS worker node(s) connected under Endpoints > All Endpoints. You can do that by including an additional filter, which can be Installation Package Contains <your-prefix>.

![](/resources/cc-10.png?raw=true)

Note: it may take a few minutes for the endpoints to show up.

    
Once you have verified the installation, move on to the next section [here](/07-CortexCloudRuntimeSecurity.md)!