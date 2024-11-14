## Part 3: Deploying Microsoft Sentinel for Firewall Integration, Log Analytics, and Incident Response  
**Objective**: Set up a centralized monitoring and incident response system using Microsoft Sentinel by integrating Log Analytics workspace, integrating firewall logs, and configuring custom alerts for effective threat detection and response.  
### 3.1. Deploying Azure Sentinel  
  -   
      
    <kbd>![Azure Sentinel Marketplace](images/sentinel-marketplace.png)</kbd>  

    <kbd>![Azure Sentinel Page](images/sentinel-page.png)</kbd>  

    <kbd>![Azure Sentinel Workspace](images/sentinel-workspace.png)</kbd>  

    <kbd>![Add Azure Sentinel to Workspace](images/add-sentinel-to-workspace.png)</kbd>   

### 3.2. Verifying Log Ingestion from Fortinet Firewall to Linux VM  
  -   
      
    <kbd>![Ubuntu tcpdump](images/ubuntu-tcpdump.png)</kbd>  

    <kbd>![Ubuntu syslog](images/ubuntu-syslog.png)</kbd>  

### 3.3. Configuring Data Connector  
  -   
      
    <kbd>![Azure Sentinel Content Hub](images/sentinel-contenthub.png)</kbd>  

    <kbd>![FortiGate Connector](images/fortigate-connector.png)</kbd>  

    <kbd>![Azure Sentinel Data Connectors](images/data-connectors.png)</kbd>  

    <kbd>![Fortinet Connector Configuration Page 1](images/fortinet-configuration-1.png)</kbd>  

    <kbd>![Fortinet Connector Configuration Page 2](images/fortinet-configuration-2.png)</kbd>  

    <kbd>![Removing Old Onboard Agent](images/removing-agent.png)</kbd>  

    <kbd>![Installing New Agent](images/install-new-agent.png)</kbd>  

    <kbd>![Data Connectors Result](images/data-connectors-result.png)</kbd>  

### 3.4. Testing Log Query  
  -   
      
    <kbd>![Querying Logs](images/logs-query.png)</kbd>  
    
    <kbd>![RDP Test](images/rdp-test.png)</kbd>  
    
    <kbd>![Inserting RDP Credentials](images/rdp-creds.png)</kbd>  

    <kbd>![Forward Traffic](images/forward-traffic.png)</kbd>  

    <kbd>![Azure Sentinel Log](images/sentinel-log.png)</kbd>  
    
### 3.5. Creating Manual Alert  
  -   
      
    <kbd>![Azure Sentinel Schedule Query Rule](images/sentinel-sched-rule.png)</kbd>  

    <kbd>![Schedule Query Rule Creation](images/sched-rule-creation.png)</kbd>  

    <kbd>![Set Rule Query](images/rule-query.png)</kbd>  

    <kbd>![Query Scheduling](images/query-sched.png)</kbd>  

    <kbd>![Rule Review](images/rule-review.png)</kbd>  

    <kbd>![Azure Sentinel Analytics Page](images/sentinel-analytics.png)</kbd>  

    <kbd>![Azure Sentinel Overview Page](images/sentinel-overview.png)</kbd>  

    <kbd>![Azure Sentinel Incident Page](images/sentinel-incident.png)</kbd>  

    <kbd>![Incident Details](images/incident-details.png)</kbd>  

    <kbd>![Incident Investigation](images/incident-investigation.png)</kbd>  
