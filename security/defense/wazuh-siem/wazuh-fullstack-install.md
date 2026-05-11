At the time of this writing, 2026-02-24, the current version of Wazuh is 4.14.

---

## Requirements
- Server or Linux VM allocated with at least a 4 core CPU, 8 GiB of RAM, and 50GB of storage.  

<img src='/security-projects/wazuh-siem/attachments/wazuh-recommended-hardware.png' width='500' alt='hardware requirements'>

- Linux distribution of your choice.
	- Note: Windows cannot be used as per Wazuh documentation at `https://documentation.wazuh.com/current/quickstart.html`
- Internet connection.

--- 

## Install

It should be noted that this install is on a single server, Wazuh supports a cluster install.

1. Download and run the Wazuh installation assistant: 
	1. `curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash ./wazuh-install.sh -a`
	2. Note: While it is dangerous to blindly start a script, best practice dictates to curl the script and examine it prior to use.
2. Once the installation is complete, you will see an output that displays access credentials and that the install was successful:
	1.  INFO: --- Summary ---
INFO: You can access the web interface https://<WAZUH_DASHBOARD_IP_ADDRESS>
    User: admin
    Password: <ADMIN_PASSWORD>
INFO: Installation finished.
3. If there is a firewall in place, make sure that the following inbound ports are allowed on the server:
	1. 443/tcp for HTTPS web user interface.
	2. 1514/tcp for Agent connection service.
	3. 1515/tcp for Agent enrollment services.
	4. 1516/tcp for Wazuh cluster installs.
4. Access the Wazuh interface with `https://<WAZUH_DASHBOARD_IP_ADDRESS>` and your credentials.

--- 

## Agents
Wazuh is an agent-based SIEM solution, that also have the capability to handle rsyslog requests for when the agent cannot be installed. The agent can be installed on Linux, Windows, MacOS, Solaris, AIX, and HP-UX.

The links to the various OS agents can be found at 'https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html' 

--- 
## Lessons Learned
This was a very straightforward install. This enabled me on how a SIEM is deployed, and integrated in a given environment. 
- The use of Wazuh over Splunk is due to Wazuh's open-source nature that assures that I have access to as much features without the need of a license. While Splunk is ideal for a true enterprise experience, the limiting nature of it's free license was a no-go.

--- 

## References
- https://documentation.wazuh.com/current/quickstart.html
- https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html