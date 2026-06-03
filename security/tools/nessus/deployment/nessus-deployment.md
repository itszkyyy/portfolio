
## About
Tenable Nessus is a tool used by security professionals to perform vulnerability scanning of an environment. This proactive approach reduces risk by quickly identifying vulnerabilities in an organizations environment allowing system administrators or security professionals to patch or mitigate vulnerabilities enhancing the organization's security posture.<BR><BR>
Nessus offers a free one-year license to verified students and educators found <a href='https://www.tenable.com/tenable-nessus-for-education'>here</a>. 

## Prequisites
For <= 50,000 hosts:
    <BR>1. server, virtual machine, or container with atleast 4 cores, 4 GB of memory (8 GB recommended), and 40 GB of storage.
<BR>
For > 50,000 hosts:
    <BR>1. server, virtual machine, or container with atleast 8 cores, 8 GB of memory (16 GB recommended), and 40 GB of storage.
<BR>
2. network connection.

Note: The following procedures will have to be performed with administrative privileges.
## Procedure
If you haven't yet, obtain a Nessus license from Tenable's website <a href='https://www.tenable.com/tenable-nessus-for-education'>here</a>. 
### For Linux:
1. curl the most up-to-date version of Tanable Nessus. The latest version can be found <a href='https://www.tenable.com/downloads/nessus'>here</a>.
2. Install the package.
    <BR>2a. For RPM use `RPM -i`
3. Start the service using `systemctl start nessusd`

### For Windows:
1. Download the latest version of Nessus located <a href='https://www.tenable.com/downloads/nessus'>here</a>.
2. Proceed with GUI installation process.
3. Open PowerShell or CMD.
4. For PowerShell: `Start-Service Nessus`
<BR>    For CMD: `NET Start Nessus`

Navigate to `https://<server_ip_address>:8834/` for the dashboard.<BR>
<BR>Select 'Set Up Nessus Essentials Pro'<BR>
<BR>Input your activation code.<BR>
<BR>Create your login credentials.<BR>
<BR>Nessus will now start initializing.<BR>
    Note: This can take a bit of time depending on your connection and hardware.

Once complete, you can move on forward to configuring your first scan!<BR>
<a href='../scans/scan-configuration.md'>Proceed to scan configuration</a>

<a href="../README.md/">Return to Nessus README</a>
## References
https://www.tenable.com/downloads/nessus<BR>
https://docs.tenable.com/nessus/Content/HardwareRequirements.htm