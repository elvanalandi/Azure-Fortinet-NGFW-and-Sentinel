## Part 2: Configuring Routing and Advanced Fortinet Firewall Settings  
**Objective**: To implement network routing configurations within Azure, focusing on segmenting traffic between the WAN, DMZ, and internal networks. This part will enhance security by establishing controlled access points and managing traffic flow with Fortinet's NGFW.  

**Tools and Requirements**:  
- Azure Account and Subscription
- FortiGate NGFW
- Azure Virtual Machines (Windows 10 & Ubuntu)
- Azure Virtual Networks
- Basic Networking Knowledge
- SSH Client
- Azure CLI/PowerShell
- Basic knowledge of Remote Desktop (RDP)
  
### 2.1. Configuring Network Routing  
  - When configuring network routing, route tables are necessary to determine where data should be directed. To configure a route table, search for **Route tables** in the search bar at the top of the page. This will take you to the route tables page, where you can click the **Create route table** button. We'll make DMZ route table first.  
      
    <kbd>![Route Tables Dashboard](images/route-tables-dashboard.png)</kbd>

  - Define the subscription, resource group, region, and name for the DMZ route table. Set **Propagate gateway routes** to **Yes** to automatically receive routes from a connected gateway, ensuring traffic is routed through the gateway to other networks.  
    
    <kbd>![DMZ Route Table Create Page](images/dmz-route-table-creation.png)</kbd>  
    
  - Review the DMZ route table and create it.  
    
    <kbd>![DMZ Route Table Review Page](images/dmz-route-table-review.png)</kbd>  
    
  - Wait until your deployment is complete. After that, click the **Go to resource** button to view the DMZ route table.  
    
    <kbd>![DMZ Route Table Deployment Page](images/dmz-route-table-deployment.png)</kbd>  
    
  - Here is the DMZ route table that has been created. No routes have been set up yet.  
    
    <kbd>![DMZ Route Table](images/dmz-route-table.png)</kbd>  
    
  - To add a route, go to the **Routes** menu under the **Settings** section on the left and click **Add**. Specify the route name, and set the **Destination IP** to 0.0.0.0/0, with the **Next hop address** as the Fortigate IP (10.10.100.4) to direct traffic from the DMZ network to the internet.  
    
    <kbd>![Add DMZ Route To Internet](images/dmz-add-route-to-internet.png)</kbd>  
    
  - The new route has been set. Now, we will add the subnet to the route table.  
    
    <kbd>![DMZ Route Table New Route](images/dmz-route-table-2.png)</kbd>  
    
  - **Subnets** can also be accessed under **Settings**. Associate the subnet with the DMZ network to enable the route to direct traffic from the DMZ to the internet.  
    
    <kbd>![DMZ Route Table Add Subnet](images/dmz-rt-add-subnet.png)</kbd>  
    
  - The final result of the DMZ route table is shown in the image below.  
    
    <kbd>![DMZ Route Table New Subnet](images/dmz-route-table-3.png)</kbd>  
    
  - Using the same steps, we will now create the WAN route table.  
    
    <kbd>![WAN Route Table Create Page](images/wan-route-table-creation.png)</kbd>  
    
  - The WAN network will route traffic to the DMZ network, so the **Destionation IP** is the subnet of the DMZ network (10.10.100.0/24), and the **Next hop address** is  port 1 of the Fortinet Firewall (10.10.1.4).  
    
    <kbd>![Add WAN Route To DMZ](images/wan-add-route-to-dmz.png)</kbd>  
    
  - Here is the final result of the WAN route table.  
    
    <kbd>![WAN Route Table](images/wan-route-table.png)</kbd>  
    
  - Next, test the route table to verify if it's working by performing a network test from the Windows 10 VM.  
    
    <kbd>![Windows 10 VM](images/win10-vm.png)</kbd>
    
  - Connect to the Windows 10 VM using Bastion.  
    
    <kbd>![Starting Windows 10 VM](images/start-win10-vm.png)</kbd>  
    
  - Provide the Windows 10 VM Credentials.  
    
    <kbd>![Connect Windows 10 VM Using Bastion](images/win10-bastion.png)</kbd>  
    
  - Open **Command Prompt** from the Windows search bar or by using Windows Run (Win + R) and type `cmd`. Then, ping the Fortinet private IP address and the Linux VM to test the connectivity.  
    
    <kbd>![Testing The Network Routing](images/routing-test.png)</kbd>  
    
  - The internet may not be working, but that's okay, as we haven't configured the firewall rules yet.  
    
    <kbd>![Testing The Access To Internet](images/internet-access.png)</kbd>
    
### 2.2. Configuring Firewall Rules  
  - Log in to the Fortigate and go to **Firewall Policy**. Currently, there is only one rule, which is an implicit deny. To allow internet access, click the **+ Create new** button to add additional rules.  
      
    <kbd>![Firewall Policy](images/new-firewall-policy.png)</kbd>  
    
  - Change the action to **Accept**, set the incoming interface to the DMZ port (port 2) and the outgoing interface to the WAN port (port 1). The allowed services should be **PING** and **DNS**. Set both the Source and Destination to **all**. Then, activate **NAT** since the firewall will act as a NAT device between two networks.    
    
    <kbd>![Add DMZ to Internet Firewall Policy](images/add-dmz-to-internet-policy.png)</kbd>  
    
  - Allow traffic for all sessions in the logging options and enable the policy to apply the changes.  
    
    <kbd>![DMZ to Internet Logging Options](images/dmz-to-internet-logging-options.png)</kbd>  

    <kbd>![DMZ to Internet Policy](images/dmz-to-internet-policy.png)</kbd>  
    
  - Test the ping again, but this time ping Google's DNS server (8.8.8.8) to verify internet connectivity.  
    
    <kbd>![Testing Internet Connection](images/test-internet-connection.png)</kbd>
    
  - In the **Forward Traffic** menu in Fortigate, the traffic should now show as successfully leaving the network, indicating that the route and firewall rules are correctly configured for internet access.  
    
    <kbd>![Internet Connection Traffic](images/internet-connection-traffic.png)</kbd>
    
  - Think of **Virtual IP** as a form of NAT. We'll configure it to forward RDP traffic from the internet to the Windows VM.  
    
    <kbd>![Edit Virtual IP](images/edit-virtual-ip.png)</kbd>
    
  - Return to the **Firewall Policy** and create a new policy. Set the incoming interface to the WAN network (port 1) and the outgoing interface to the DMZ network (port 2). Set the destination to the Virtual IP that you've created and the service to **RDP**. This time, disable **NAT** because the **Virtual IP** already handles port forwarding.  
    
    <kbd>![Add Internet to RDP Policy](images/add-internet-to-rdp-policy.png)</kbd>
    
  - Enable the policy and allow logging for all sessions to monitor the traffic.  
    
    <kbd>![Internet to RDP Logging Options](images/internet-to-rdp-logging-options.png)</kbd>  
  
    <kbd>![Internet to RDP Policy](images/internet-to-rdp-policy.png)</kbd>  
    
  - Now, configure the remote desktop settings on the Windows VM. Search for **Remote desktop settings** and ensure that **Remote Desktop** is enabled. Then, go to the **Advanced settings** to configure additional options as needed.  
    
    <kbd>![RDP Settings](images/rdp-settings.png)</kbd>
    
  - Uncheck **Require computers to use Network Level Authentication to connect** in the **Advanced settings** to allow RDP connections without the need for NLA.  
    
    <kbd>![Advanced RDP Settings](images/advanced-rdp-settings.png)</kbd>
    
  - Turn off the firewall on the Windows VM. The easiest way to access this is by searching for **Firewall & network protection** in the Windows search bar.  
    
    <kbd>![Turning Off Windows Firewall](images/turn-off-win-firewall.png)</kbd>
    
  - Try connecting again using **Remote Desktop Connection** from the local computer (not the VM) by entering the public IP address or the Virtual IP of the Windows VM.  
    
    <kbd>![RDP to Windows 10 Virtual Machine](images/rdp-to-win10-vm.png)</kbd>  
  
    <kbd>![Providing Credentials](images/provide-creds.png)</kbd>  
    
  - Click **Yes** when prompted with a certificate warning to proceed with the remote desktop connection.  
    
    <kbd>![Certificate Verification](images/cert-verification.png)</kbd>
    
  - We should now be able to connect to the VM from the external network using Remote Desktop.  
    
    <kbd>![Windows 10 RDP Connection](images/win10-vm-rdp-conn.png)</kbd>  

### 2.3. Configuring IPS (Intrusion Prevention System) Rules  
  - The routes have been set. Now, to block suspicious traffic, we can utilize the **IPS (Intrusion Prevention System)** feature from Fortinet NGFW (Next-Generation Firewall) to detect and block potential threats.  
      
    <kbd>![IPS Menu](images/ips-menu.png)</kbd>  
    
  - Click **+ Create new** to create a new IPS sensor rule. Activate **Block malicious URLs** and select **Block**. Then, click on **+ Create New** in the **IPS Signatures** to define the signatures for blocking suspicious traffic.   
    
    <kbd>![New IPS Rule](images/new-ips-rule.png)</kbd>  
    
  - Choose the following settings for the IPS signature rule:  
    - Type: **Signature**
    - Action: **Monitor**
    - Packet logging: **Disable**
    - Status: **Enable**
    - Rate-based settings: **Default**
  
    For the signatures, select all the brute force signatures to monitor and detect any brute force attack attempts.  
    
    <kbd>![Add Signature](images/add-signature.png)</kbd>  
    
  - To apply the IPS rule:  
    - Edit the **Internet to Windows** firewall policy.  
    - Scroll down to the Security Profiles section.  
    - Add the IPS rule (in my case, the rule name is cyber_lab).  
    - Activate the rule to enable it.
    - Allow log traffic for all sessions and enable the policy to start monitoring and blocking suspicious traffic according to the IPS rule.
    
    <kbd>![Edit Firewall Policy 1](images/edit-firewall-policy-1.png)</kbd>  
  
    <kbd>![Edit Firewall Policy 2](images/edit-firewall-policy-2.png)</kbd>  
    
  - To create a custom IPS signature with higher sensitivity for brute force attempts, follow these steps:
    - Go to the IPS Signatures menu.
    - Click + Create New to create a custom signature.
    - Copy and paste the following signature into the signature definition:
    `F-SBID( --attack_id 7170; --name "MS.RDP.Connection.Brute.Force."; --protocol TCP; --dst_port 3389; --flow from_client; --seq 1, relative; --pattern "|e0|"; --distance 5,packet; --within 1,packet; --rate 5,20; --track SRC_IP ; )`.
    - Save and apply the custom signature to your IPS policy for higher sensitivity in detecting RDP brute force attempts.  
    
    <kbd>![New IPS Signature](images/new-ips-signature.png)</kbd>  
    
  - Go back to the **Intrusion Prevention** section and add the custom signature. In the **Custom IPS Signature** section, select the custom signature you created (in my case, **RDP_Brute_Force**) and apply it to the relevant policy. Enable the policy to activate the custom signature for monitoring traffic.  
    
    <kbd>![Using Custom IPS Signature](images/custom-ips-signature.png)</kbd>  
    
  - We should now be able to block brute force attacks. I tested it by repeatedly attempting to connect via RDP using incorrect credentials, and you can see the deny traffic logs, indicating that the IPS successfully blocked the brute force attempts.  
    
    <kbd>![IPS Blocking Result](images/ips-block-result.png)</kbd>  

### 2.4. Configuring Log Analytics with FortiGate Event Forwarding via Syslog  
  - In this part, we'll integrate the **Log Analytics Workspace** with Fortigate. Start by searching for **Log Analytics Workspace** in the **Marketplace** and click **Create**.  
      
    <kbd>![Log Analytics Workspace in Marketplace](images/log-analytics-market.png)</kbd>  
    
    <kbd>![Log Analytics Workspace Page](images/log-analytics-page.png)</kbd>  
    
  - Set up the subscription, resource group, name, and region for the **Log Analytics Workspace** according to your preferences. Review the workspace settings before proceeding to create it.  
    
    <kbd>![Log Analytics Workspace Creation Page](images/log-analytics-creation-page.png)</kbd>  

    <kbd>![Log Analytics Workspace Review](images/log-analytics-review.png)</kbd>  
    
  - Allow the deployment to complete before proceeding to the next step.  
    
    <kbd>![Log Analytics Workspace Deployment](images/log-analytics-deployment.png)</kbd>  
    
  - Go to the new **Log Analytics Workspace** from the **Resource group**.  
    
    <kbd>![Log Analytics Workspace Resource](images/log-analytics-resource.png)</kbd>  
    
  - Once in the **Overview** of the workspace, navigate to the **Agents** menu under the **Settings** section on the left.  
    
    <kbd>![Log Analytics Workspace Agents](images/log-analytics-agents.png)</kbd>  
    
  - Follow the instructions to download the agent onto the Linux VM. Under **Download and onboard agent for Linux**, ensure the **Linux servers** is selected, then copy the provided command.  
    
    <kbd>![Log Analytics Workspace Agent Setup](images/log-analytics-agent-setup.png)</kbd>  
    
  - Connect to the Ubuntu VM via **Bastion**, entering the required credentials. Once connected to the VM, set it aside temporarily, and proceed to the **Fortinet firewall** configuration.  
    
    <kbd>![Access Linux VM](images/log-analytics-linux-vm.png)</kbd>  

    <kbd>![Connect Linux VM Via Bastion](images/log-analytics-linux-vm-bastion.png)</kbd>  

    <kbd>![Provide Linux VM Credentials](images/linux-bastion-creds.png)</kbd>  
    
  - In **Firewall Policy**, edit the **DMZ to Internet** policy. Add **HTTP** and **HTTPS** services to allow downloading files from the internet using `wget`.  
    
    <kbd>![DMZ to Internet Firewall Policy](images/log-analytics-firewall-policy.png)</kbd>  

    <kbd>![Add HTTP and HTTPS Services in Firewall Policy](images/add-https-firewall-policy.png)</kbd>  
    
  - Return to the Ubuntu VM and paste the command you previously copied to initiate the download and setup of the Linux agent.  
    
    <kbd>![Install Log Analytics Agent on Linux VM](images/install-agent-on-vm.png)</kbd>  
    
  - After that, Return to the **Agents** section and create a **Data Collection Rules** by clicking on the **Data Collection Rules** button. This will allow the agent you set up to start collecting data.  
    
    <kbd>![Data Collection Rules Button](images/data-collection-rules.png)</kbd>  
    
  - Click on the **Create** button.  
    
    <kbd>![Data Collection Rules Dashboard](images/data-collection-rules-dashboard.png)</kbd>  
    
  - Specify the **Name, Subscription, Resource Group and Region** for the Data Collection Rule. For the **Platform Type**, select **Linux**.  
    
    <kbd>![Data Collection Rule Creation](images/data-collection-rule-creation.png)</kbd>  
    
  - Next, click on **Add resources** and select your Linux VM from the available options.  
    
    <kbd>![Adding Data Collection Rule Resource](images/add-data-collection-rule-resource.png)</kbd>  
    
  - In the next section, select all the **Linux Syslog** log options under **Data source**.  
    
    <kbd>![Adding Data Source](images/add-data-source.png)</kbd>  
    
  - Specify the **Destination type**, **Subscription**, and the **Log Analytics Workspace** that you created earlier as the **Destination Details**.  
    
    <kbd>![Add Data Collection Destination](images/add-destination.png)</kbd>  
    
  - Review the settings for the **Data Collection Rule** and click **Create** to finalize the setup.  
    
    <kbd>![Data Collection Rule Review](images/data-collection-rule-review.png)</kbd>  
    
  - The agent is now successfully connected to the **Log Analytics Workspace**.  
    
    <kbd>![Log Analytics Workspace Agent Connection](images/log-analytics-agent-connection.png)</kbd>  
    
  - To ingest the syslog data into **Azure Sentinel**, go to the **Log Settings** in **Fortigate**. Then, navigate to the CLI menu on the top left side.  
    
    <kbd>![Firewall Log Settings](images/firewall-log-settings.png)</kbd>  
    
  - Use the following commands in the CLI to configure syslog on the Fortigate:  
    `config log syslogd setting`  
    `set status enable`  
    `set server 10.10.100.6 # Replace with your Linux VM IP.`  
    `set format cef`  
    `set mode reliable`  
    `end`  
    
    <kbd>![Firewall Log Settings Setup in CLI](images/firewall-log-settings-setup-cli.png)</kbd>  
    
  - To validate the settings, use the following command in the CLI: `get log syslogd setting`.  
    
    <kbd>![Firewall Log Settings Validation](images/log-settings-validation.png)</kbd>

    We'll proceed with deploying **Microsoft Sentinel** in [Part 3](../Azure-Sentinel/README.md).
