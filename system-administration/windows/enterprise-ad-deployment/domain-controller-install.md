## Requirements
--- 
- Server or VM allocated with at least 2 CPU cores, 2 GB of RAM, and 90 GB of storage.
- (Optional) Hypervisor of your choice. This instance will have steps for ESXi and Proxmox.
# ESXi
1. Obtain Windows Server 2022 Evaluation ISO from official Microsoft website.
	1. Licenses are valid for 180 days.
2. Upload ISO image to designated datastore on ESXi server.
	1.  I've created a folder for ISO images named 'os-images' on the server under datastore1.
	2. Navigate to Storage > datastore1 > Datastore browser > os-images, and click Upload then proceed to upload the Windows Server 2022 ISO.
3. Create the virtual machine for Windows Server 2022.
	1. Navigate to 'Virtual Machines' tab, and click 'Create / Register VM'.
	2. Select 'Create a new virtual machine'.
	3. Enter a name for the VM, then select 'Windows' under 'Guest OS family', and select 'Microsoft Windows Server 2022' under 'Guest OS Version'. I've also checkmarked the box beside 'Enable Windows Virtualization Based Security' as this will allow me to enable secure boot for best practices.
	4. Select your desired storage.
	5. I've decided to leave CPU, Memory, and Hard disk as ESXi is good at applying recommended hardware designations. Make sure that your network adapter is selected to the appropriate network. In my lab, I've created a vSwitch with no uplink so I may isolate the environment. Under CD/DVD Drive 1, select Data Store, and then select the ISO image you've uploaded.
	6. Proceed to click on 'Finish' then select the VM, and click on 'Power on' to boot up the instance.
	7. Proceed to console in to the VM by clicking on 'Console'.

# Windows Server Install
---
Once the Windows Server 2022 instance is booted up, you'll be prompted to install Windows Server 2022. Proceed with these steps to install Windows.
1. Click on 'Next' then 'Install Now'.
2. You can either choose to Install Standard Evaluation (no GUI) or Standard Experience Desktop Experience (GUI). This lab will be using Standard Experience to minimalize resource usage, it's also the commonly used edition in enterprises to minimalize the attack surface, and we will be setting up a Windows 10 Pro client as a means to graphically administer the domain.
3. Read and accept the Terms and Conditions.
4. Click on 'Custom: Install Microsoft Server Operating System Only'.
5. Click on 'New', then 'Apply', and 'OK' to use all the storage allocated.
6. Select the 'Primary' partition under 'Type' and then click 'Next'.
7. Windows Server 2022 will install, then proceed to reboot once complete.
# Domain Services Install
---
Once Windows Server is installed, you have to install Active Directory Domain Services (AD DS) onto the server using the following steps:

1. Send 'Ctrl-Alt-Del' to the machine.
	1.  on ESXi, its under 'Actions' > 'Guest OS' > 'Send Keys'.
2. Windows will prompt you to change the password for the Administrator account. Once complete, you will be placed into SConfig.
3. (Optional) If needed, configure network settings by typing in `8`. 
4. Exit to command line (PowerShell) by typing `15`.
5. First rename the server using `Rename-Computer -NewName <new_name>`
6. Use `Get-NetAdapter` to find the interface you want to modify. We want to modify 'Ethernet0'.
<img src='/active-directory-lab/enterprise-ad-deployment/assets/get-netadapter-output.png' width='800' alt='output'>
7. We will then assign a static IP address to the interface using ```
New-NetIPAddress -InterfaceAlias <Name of Interface> -IPAddress '<IP_ADDRESS>' -AddressFamily IPV4 -PrefixLength <subnet mask in CIDR notation> -Defaultgateway '<ROUTER_ADDRESS>'```
8. Then we will set the DNS server(s) using `Set-DnsClientServerAddress` like so. ``` Set-DnsClientServerAddress -InterfaceAlias <interface name> -ServerAddressess '<dns address>'```
9. Test your connecting using ping. I recommend pinging a public DNS server such as Cloudflare at 1.1.1.1 or 1.0.0.1, and test using a Fully Qualified Domain Name (FQDN) such as lttstore.com.
10. Proceed to run `Install-WindowsFeature Ad-Domain-Services -IncludeManagementTools -Verbose`.

---
# Lessons Learned
This dove into system administration by setting up a VM or server and installing Windows Server 2022. This provides experience on how initial configuration is performed. Additionally, with this being Windows, we were able to exercise some PowerShell administration using commands to further reenforce PowerShell understanding.

---

# References
- https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/deploy/install-active-directory-domain-services--level-100-