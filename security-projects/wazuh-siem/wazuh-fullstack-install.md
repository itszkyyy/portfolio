At the time of this writing, 2026-02-24, the current version of Wazuh is 4.14.
# Requirements
- Server or VM allocated with atleast a 4 core CPU, 8 GiB of RAM, and 50GB of storage.  ![[wazuh-recommended-hardware.png]]
- Linux distribution of your choice.
	- Note: Windows cannot be used as per Wazuh documentation at `https://documentation.wazuh.com/current/quickstart.html`
- Internet connection.

# Install

It should be noted that this install is on a single server, Wazuh supports a cluster install.

1. Download and run the Wazuh installation assistant: 
	1. `curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash ./wazuh-install.sh -a`
2. Once the installation is complete, you will see an output that displays access credentials and that the install was successful:
		1. ```
		   ```INFO: --- Summary --- 
		INFO: You can access the web interface https://<WAZUH_DASHBOARD_IP_ADDRESS> User: admin Password: <ADMIN_PASSWORD> INFO: Installation finished.```
		   ```
