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