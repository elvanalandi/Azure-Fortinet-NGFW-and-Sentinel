## Part 2: Configuring Routing and Advanced Fortinet Firewall Settings  
**Objective**: To implement network routing configurations within Azure, focusing on segmenting traffic between the WAN, DMZ, and internal networks. This part will enhance security by establishing controlled access points and managing traffic flow with Fortinet's NGFW.  
### 2.1. Configuring Network Routing  
  -   
      
    <kbd>![Route Tables Dashboard](images/route-tables-dashboard.png)</kbd>  
  
    <kbd>![DMZ Route Table Create Page](images/dmz-route-table-creation.png)</kbd>  
    
    <kbd>![DMZ Route Table Review Page](images/dmz-route-table-review.png)</kbd>  

    <kbd>![DMZ Route Table Deployment Page](images/dmz-route-table-deployment.png)</kbd>  

    <kbd>![DMZ Route Table](images/dmz-route-table.png)</kbd>  

    <kbd>![Add DMZ Route To Internet](images/dmz-add-route-to-internet.png)</kbd>  

    <kbd>![DMZ Route Table New Route](images/dmz-route-table-2.png)</kbd>  

    <kbd>![DMZ Route Table Add Subnet](images/dmz-rt-add-subnet.png)</kbd>  

    <kbd>![DMZ Route Table New Subnet](images/dmz-route-table-3.png)</kbd>  

    <kbd>![WAN Route Table Create Page](images/wan-route-table-creation.png)</kbd>  

    <kbd>![Add WAN Route To DMZ](images/wan-add-route-to-dmz.png)</kbd>  

    <kbd>![WAN Route Table](images/wan-route-table.png)</kbd>  

    <kbd>![Windows 10 VM](images/win10-vm.png)</kbd>

    <kbd>![Starting Windows 10 VM](images/start-win10-vm.png)</kbd>  

    <kbd>![Connect Windows 10 VM Using Bastion](images/win10-bastion.png)</kbd>  

    <kbd>![Testing The Network Routing](images/routing-test.png)</kbd>  

    <kbd>![Testing The Access To Internet](images/internet-access.png)</kbd>
    
### 2.2. Configuring Firewall Rules  
  -   
      
    <kbd>![Firewall Policy](images/new-firewall-policy.png)</kbd>

    <kbd>![Add DMZ to Internet Firewall Policy](images/add-dmz-to-internet-policy.png)</kbd>

    <kbd>![DMZ to Internet Logging Options](images/dmz-to-internet-logging-options.png)</kbd>  

    <kbd>![DMZ to Internet Policy](images/dmz-to-internet-policy.png)</kbd>

    <kbd>![Testing Internet Connection](images/test-internet-connection.png)</kbd>

    <kbd>![Internet Connection Traffic](images/internet-connection-traffic.png)</kbd>

    <kbd>![Edit Virtual IP](images/edit-virtual-ip.png)</kbd>

    <kbd>![Add Internet to RDP Policy](images/add-internet-to-rdp-policy.png)</kbd>

    <kbd>![Internet to RDP Logging Options](images/internet-to-rdp-logging-options.png)</kbd>

    <kbd>![Internet to RDP Policy](images/internet-to-rdp-policy.png)</kbd>

    <kbd>![RDP Settings](images/rdp-settings.png)</kbd>

    <kbd>![Advanced RDP Settings](images/advanced-rdp-settings.png)</kbd>

    <kbd>![Turning Off Windows Firewall](images/turn-off-win-firewall.png)</kbd>

    <kbd>![RDP to Windows 10 Virtual Machine](images/rdp-to-win10-vm.png)</kbd>

    <kbd>![Providing Credentials](images/provide-creds.png)</kbd>

    <kbd>![Certificate Verification](images/cert-verification.png)</kbd>

    <kbd>![Windows 10 RDP Connection](images/win10-vm-rdp-conn.png)</kbd>  

### 2.3. Configuring IPS (Intrusion Prevention System) Rules  
  -   
      
    <kbd>![IPS Menu](images/ips-menu.png)</kbd>  

    <kbd>![New IPS Rule](images/new-ips-rule.png)</kbd>  

    <kbd>![Add Signature](images/add-signature.png)</kbd>  

    <kbd>![Edit Firewall Policy 1](images/edit-firewall-policy-1.png)</kbd>  

    <kbd>![Edit Firewall Policy 2](images/edit-firewall-policy-2.png)</kbd>  

    <kbd>![New IPS Signature](images/new-ips-signature.png)</kbd>  

    <kbd>![Using Custom IPS Signature](images/custom-ips-signature.png)</kbd>  

    <kbd>![IPS Blocking Result](images/ips-block-result.png)</kbd>  

### 2.4. Configuring Log Analytics with FortiGate Event Forwarding via Syslog  
  -   
      
    <kbd>![Log Analytics Workspace in Marketplace](images/log-analytics-market.png)</kbd>

    <kbd>![Log Analytics Workspace Page](images/log-analytics-page.png)</kbd>  

    <kbd>![Log Analytics Workspace Creation Page](images/log-analytics-creation-page.png)</kbd>  

    <kbd>![Log Analytics Workspace Review](images/log-analytics-review.png)</kbd>  

    <kbd>![Log Analytics Workspace Deployment](images/log-analytics-deployment.png)</kbd>  

    <kbd>![Log Analytics Workspace Resource](images/log-analytics-resource.png)</kbd>  

    <kbd>![Log Analytics Workspace Agents](images/log-analytics-agents.png)</kbd>  

    <kbd>![Log Analytics Workspace Agent Setup](images/log-analytics-agent-setup.png)</kbd>  

    <kbd>![Access Linux VM](images/log-analytics-linux-vm.png)</kbd>  

    <kbd>![Connect Linux VM Via Bastion](images/log-analytics-linux-vm-bastion.png)</kbd>  

    <kbd>![Provide Linux VM Credentials](images/linux-bastion-creds.png)</kbd>  

    <kbd>![DMZ to Internet Firewall Policy](images/log-analytics-firewall-policy.png)</kbd>  

    <kbd>![Add HTTP and HTTPS Services in Firewall Policy](images/add-https-firewall-policy.png)</kbd>  

    <kbd>![Install Log Analytics Agent on Linux VM](images/install-agent-on-vm.png)</kbd>  

    <kbd>![Data Collection Rules Button](images/data-collection-rules.png)</kbd>  

    <kbd>![Data Collection Rules Dashboard](images/data-collection-rules-dashboard.png)</kbd>  

    <kbd>![Data Collection Rule Creation](images/data-collection-rule-creation.png)</kbd>  

    <kbd>![Adding Data Collection Rule Resource](images/add-data-collection-rule-resource.png)</kbd>  

    <kbd>![Adding Data Source](images/add-data-source.png)</kbd>  

    <kbd>![Add Data Collection Destination](images/add-destination.png)</kbd>  

    <kbd>![Data Collection Rule Review](images/data-collection-rule-review.png)</kbd>  

    <kbd>![Log Analytics Workspace Agent Connection](images/log-analytics-agent-connection.png)</kbd>  

    <kbd>![Firewall Log Settings](images/firewall-log-settings.png)</kbd>  

    <kbd>![Firewall Log Settings Setup in CLI](images/firewall-log-settings-setup-cli.png)</kbd>  

    <kbd>![Firewall Log Settings Validation](images/log-settings-validation.png)</kbd>  
