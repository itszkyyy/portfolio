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
