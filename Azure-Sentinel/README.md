## Part 3: Deploying Microsoft Sentinel for Firewall Integration, Log Analytics, and Incident Response  
**Objective**: Set up a centralized monitoring and incident response system using Microsoft Sentinel by integrating Log Analytics workspace, integrating firewall logs, and configuring custom alerts for effective threat detection and response.  
### 3.1. Deploying Azure Sentinel  
  - Search for **Azure Sentinel** in the **Marketplace**. The correct option will appear on the right side with the title **Azure Sentinel**.  
      
    <kbd>![Azure Sentinel Marketplace](images/sentinel-marketplace.png)</kbd>  
    
  - Click the **Create** button to begin the setup.  
    
    <kbd>![Azure Sentinel Page](images/sentinel-page.png)</kbd>  
    
  - First, we'll need to add Microsoft Sentinel to a workspace. Click on **Connect workspace** or **+ Add** button to proceed.  
    
    <kbd>![Azure Sentinel Workspace](images/sentinel-workspace.png)</kbd>  
    
  - Specify the necessary details, such as the **Log Analytics Workspace**, **Region**, **Resource Group**, and **Subscription**. Finally, review the settings and click **Create**.  
    
    <kbd>![Add Azure Sentinel to Workspace](images/add-sentinel-to-workspace.png)</kbd>   

### 3.2. Verifying Log Ingestion from Fortinet Firewall to Linux VM  
  - To verify the logs from the Linux VM, there are two methods you can use:  
  1. Using the tcpdump command:
     - Run the following command to monitor traffic on port 514 (the default syslog port):  
       `sudo tcpdump port 514`  
       <kbd>![Ubuntu tcpdump](images/ubuntu-tcpdump.png)</kbd>  
  2. Using the syslog file:
     - Run this command to view the last few lines of the syslog:  
       `tail -5 /var/log/syslog`      
       <kbd>![Ubuntu syslog](images/ubuntu-syslog.png)</kbd>  
    
In my case, the second method (checking the syslog file) provided clearer and more direct feedback because was able to see the actual logs coming from FortiGate, confirming that syslog messages are being ingested correctly.  

### 3.3. Configuring Data Connector  
  - Search for **Fortinet FortiGate Next-Generation Firewall connector** in the **Microsoft Sentinel Content Hub**. This connector will collect logs from **FortiGate** to **Sentinel**. Navigate to **Install with dependencies** and click the **Install** button under **Fortinet FortiGate Next-Generation Firewall connector**.  
      
    <kbd>![Azure Sentinel Content Hub](images/sentinel-contenthub.png)</kbd>  

    <kbd>![FortiGate Connector](images/fortigate-connector.png)</kbd>  
    
  - After the installation, go to the **Data connectors** menu, and you’ll see that Fortinet is installed but not yet connected (indicated by the gray stripe on the left side of the box).  
    
    <kbd>![Azure Sentinel Data Connectors](images/data-connectors.png)</kbd>  
    
  - Click on Fortinet, and follow the configuration instructions. We only need to copy the commands to our Linux VM. The first command installs the CEF collector, and the second command forwards Fortinet logs to the Syslog agent. You can also validate the installation using the third command.  
    
    <kbd>![Fortinet Connector Configuration Page 1](images/fortinet-configuration-1.png)</kbd>  

    <kbd>![Fortinet Connector Configuration Page 2](images/fortinet-configuration-2.png)</kbd>  
    
  - Before doing that, we'll first remove the old onboard agent using the following command: `sudo sh onboard_agent.sh --purge`.  
    
    <kbd>![Removing Old Onboard Agent](images/removing-agent.png)</kbd>  
    
  - Next, install the new agent and the CEF collector by running the first command in the instructions (located under part 1.2).  
    
    <kbd>![Installing New Agent](images/install-new-agent.png)</kbd>  
    
  - Now, Fortinet is connected to the data connector. Although this connector appeared to be deprecated when I created this lab, it should not be an issue since this lab is for simulation purposes.  
    
    <kbd>![Data Connectors Result](images/data-connectors-result.png)</kbd>  

### 3.4. Testing Log Query  
  - Now, test the log query from the **Logs** menu in Microsoft Sentinel. Run the `CommonSecurityLog` query, and you should see logs from Fortinet.  
      
    <kbd>![Querying Logs](images/logs-query.png)</kbd>  
    
  - Then, I attempted the brute force attack again, as demonstrated in Part 2.  
      
    <kbd>![RDP Test](images/rdp-test.png)</kbd>  
    
    <kbd>![Inserting RDP Credentials](images/rdp-creds.png)</kbd>  

    <kbd>![Forward Traffic](images/forward-traffic.png)</kbd>  
    
  - The query using my public IP address as the SourceIP returns the event details in **Sentinel Logs**.  
      
    <kbd>![Azure Sentinel Log](images/sentinel-log.png)</kbd>  
    
### 3.5. Creating A Manual Alert  
  - Here, I created a **Scheduled query rule**so that the brute force attack can be investigated in the Incidents. From **Analytics** under **Microsoft Sentinel**, go to the scheduled query rule.  
      
    <kbd>![Azure Sentinel Schedule Query Rule](images/sentinel-sched-rule.png)</kbd>  
    
  - Defined the **Name**, **Severity**, and **MITRE ATT&CK**. For MITRE ATT&CK, select **Credential Access - Brute Force**. Enable the status to activate the rule.  
      
    <kbd>![Schedule Query Rule Creation](images/sched-rule-creation.png)</kbd>  
    
  - Then, set the rule query. I used **DeviceEventCategory** to search for the IPS Signature (note that this query may not be valid if you have other different threat signatures in IPS). The entity for mapping will be the Source IP address. The query is: `CommonSecurityLog | where DeviceEventCategory contains "ips"`.  
      
    <kbd>![Set Rule Query](images/rule-query.png)</kbd>  
    
  - Next, you can configure this based on your preferences. For my setup, I changed the query to run every 5 minutes and enabled it to start automatically.  
      
    <kbd>![Query Scheduling](images/query-sched.png)</kbd>  

    <kbd>![Rule Review](images/rule-review.png)</kbd>  
    
  - The new rule will now appear in the **Analytics** section of Microsoft Sentinel.  
      
    <kbd>![Azure Sentinel Analytics Page](images/sentinel-analytics.png)</kbd>  
    
  - Wait for a moment to allow the incident to be generated. Once it's ready, return to the **Microsoft Sentinel** overview page. The incident will appear there to review..  
      
    <kbd>![Azure Sentinel Overview Page](images/sentinel-overview.png)</kbd>  
    
  - To view the full details of the incident, navigate to the **Incidents** page in Microsoft Sentinel. There, you will find the generated incident. Click on the incident to open it and explore all relevant details, such as the source of the attack, affected entities, and any associated alerts or activities.  
      
    <kbd>![Azure Sentinel Incident Page](images/sentinel-incident.png)</kbd>  
    
  - By going to the **Investigate** section, you can see a visual representation of the incident and its context. The mapping you set earlier, such as the Source IP address, will provide a clear view of the attacker's activity.
    
    This investigative view in Microsoft Sentinel helps you to piece together the bigger picture, offering insights into the attacker's methods and timeline, making it easier to identify potential threats and respond appropriately.  
      
    <kbd>![Incident Details](images/incident-details.png)</kbd>  

    <kbd>![Incident Investigation](images/incident-investigation.png)</kbd>  
