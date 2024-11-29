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
    <kbd>![Creating Windows VM Basic Configuration](images/create-win-vm.png)</kbd>  

    <kbd>![Windows VM Networking Configuration](images/win-vm-networking.png)</kbd>  

    <kbd>![Windows VM Network Security Group Configuration](images/win-vm-nsg.png)</kbd>  

    <kbd>![Windows VM Management Configuration](images/win-vm-management.png)</kbd>  

    <kbd>![Windows VM Monitoring Configuration](images/win-vm-monitoring.png)</kbd>  
  
### 2. Create a Log Analytics Workspace  
    <kbd>![Creating Log Analytics Workspace Configuration](images/create-log-analytics.png)</kbd>  

### 3. Configure Microsoft Defender for Cloud  
    <kbd>![Microsoft Defender for Cloud Configuration](images/ms-defender.png)</kbd>  
  
    <kbd>![Microsoft Defender for Cloud Plans](images/defender-plans.png)</kbd>  
      
    <kbd>![Microsoft Defender for Cloud Data Collection](images/defender-data-collection.png)</kbd>  

### 4. Connect Log Analytics Workspace to Virtual Machine  
    <kbd>![Virtual Machine Connections](images/vm-connection.png)</kbd>  

    <kbd>![Connecting VM to Log Analytics Workspace](images/connect-vm-to-log.png)</kbd>  

### 5. Configure Microsoft Sentinel  
    <kbd>![Connecting Sentinel to Log Analytics Workspace](images/sentinel-to-log.png)</kbd>  
    
### 6. Disable the Firewall in Virtual Machine  

### 7. Adding the Security Log Exporter Script  

### 8. Create a Custom Log in Log Analytics Workspace  

### 9. Visualize Attack in Map using Workbooks  

