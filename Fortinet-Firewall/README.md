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
      
    <kbd>![Firewall Policy](images/firewall-policy.png)</kbd>

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
