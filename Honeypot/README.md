## Honeypot Deployment and Threat Visualization with Azure Sentinel  
**Objective**: Deploy honeypots as decoys, integrate Log Analytics Workspaces, and Azure Sentinel to analyze Windows Security Event Logs using KQL, and visualize attack data in World Map Workbooks.  
  
**Tools and Requirements**:  
- [Azure Account and Subscription](https://azure.microsoft.com/en-us/free/) (Free $200 Credit for 30 days)
- Microsoft Sentinel
- [Custom Powershell Script](https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1)  
- Remote Desktop Protocol (RDP)
- [IP Geo Location API](https://ipgeolocation.io/)
- Kusto Query Language (KQL)
  
### 1. Create a Honeypot Virtual Machine  
  - Go to the Microsoft Azure Dashboard, search for "virtual machines", and then click **Create** > **Azure virtual machine**.  
      
    <kbd>![Creating Windows VM Basic Configuration](images/create-win-vm.png)</kbd>  

    <kbd>![Windows VM Networking Configuration](images/win-vm-networking.png)</kbd>  

    <kbd>![Windows VM Network Security Group Configuration](images/win-vm-nsg.png)</kbd>  

    <kbd>![Windows VM Management Configuration](images/win-vm-management.png)</kbd>  

    <kbd>![Windows VM Monitoring Configuration](images/win-vm-monitoring.png)</kbd>  
  
### 2. Create a Log Analytics Workspace  
  -   
      
    <kbd>![Creating Log Analytics Workspace Configuration](images/create-log-analytics.png)</kbd>  

### 3. Configure Microsoft Defender for Cloud  
  -   
      
    <kbd>![Microsoft Defender for Cloud Configuration](images/ms-defender.png)</kbd>  
  
    <kbd>![Microsoft Defender for Cloud Plans](images/defender-plans.png)</kbd>  
      
    <kbd>![Microsoft Defender for Cloud Data Collection](images/defender-data-collection.png)</kbd>  

### 4. Connect Log Analytics Workspace to Virtual Machine  
  -   
      
    <kbd>![Virtual Machine Connections](images/vm-connection.png)</kbd>  

    <kbd>![Connecting VM to Log Analytics Workspace](images/connect-vm-to-log.png)</kbd>  

### 5. Configure Microsoft Sentinel  
  -   
      
    <kbd>![Connecting Sentinel to Log Analytics Workspace](images/sentinel-to-log.png)</kbd>  
    
### 6. Disable the Firewall in Virtual Machine  
  -   
      
    <kbd>![Windows Firewall](images/wf.png)</kbd>  
  
    <kbd>![Turn Off Windows Firewall](images/wf-off.png)</kbd>  
  
    <kbd>![Remote Desktop Settings](images/rdp-settings.png)</kbd>  
  
    <kbd>![Remote Desktop Advanced Settings](images/rdp-advanced-settings.png)</kbd>  
    
### 7. Adding the Security Log Exporter Script  
  -   
      
    <kbd>![IP Geolocation](images/ip-geo.png)</kbd>  
  
    <kbd>![Security Log Exporter Script](images/log-exporter-script.png)</kbd>  
  
### 8. Create a Custom Log in Log Analytics Workspace  
  -   
      
    <kbd>![Log Analytics Workspace Tables](images/log-analytics-table.png)</kbd>  
  
    <kbd>![Create A Custom Log](images/custom-log.png)</kbd>  

    <kbd>![Custom Log Record Delimiter](images/custom-log-delimiter.png)</kbd>  

    <kbd>![Custom Log Collection Path](images/custom-log-path.png)</kbd>  

    <kbd>![Custom Log Name](images/custom-log-name.png)</kbd>  

    <kbd>![Custom Log Name](images/custom-log-review.png)</kbd>  
    
### 9. Visualize Attack in Map using Workbooks  
  -   
      
    <kbd>![Microsoft Sentinel Logs](images/sentinel-logs.png)</kbd>  
  
    <kbd>![Create A New Workbook](images/create-workbook.png)</kbd>  

    <kbd>![Workbook Query](images/workbook-query.png)</kbd>  

    <kbd>![Workbook Map Settings](images/workbook-map-settings.png)</kbd>  

    <kbd>![Geo Location Map Result](images/geo-ip-result.png)</kbd>  

    <kbd>![Task Scheduler](images/taskschd.png)</kbd>  

    <kbd>![Create A New Task](images/create-task.png)</kbd>  

    <kbd>![Task Triggers](images/task-trigger.png)</kbd>  

    <kbd>![Task Actions](images/task-action.png)</kbd>  

    <kbd>![Task Conditions](images/task-condition.png)</kbd>  

    <kbd>![Task Settings](images/task-settings.png)</kbd>  

    <kbd>![Running Task](images/run-task.png)</kbd>  
