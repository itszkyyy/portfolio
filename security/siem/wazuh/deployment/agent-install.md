# Agent Installation
Following the installation of the Wazuh stack, we now have to install Wazuh agents onto end-points. These agents perform all the actions of Wazuh, such as log collection/forwarding, configuration assessment, active response, and system health collection.
## Note: Please make sure that you've opened the required ports on the host or network firewall in the <a href='/security/defense/siem/wazuh-siem/wazuh-fullstack-install.md'>Wazuh Installation</a> guide.

# Linux
Install using the appropriate guide for your package manager:
## APT
    1. Install the following packages if missing:
        `apt-get install gnupg apt-transport-https`
    2. Install the GPG key:
        `curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg`
    3. Add the repository:
        `echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list`
    4. Update package information:
        `apt get-update`
    5. Install the agent:
        `# WAZUH_MANAGER='<insert_ip_here>' (sudo) apt-get install wazuh-agent`
    6. Enable the service for start on boot, start the service, and check the status:
        `systemctl enable wazuh-agent && systemctl start wazuh-agent && systemctl status wazuh-agent`


## RPM
    1. Import the GPG key:
        rpm --import https://packages.wazuh.com/key/GPG-KEY-WAZUH
    2. Add the repository:
        ```cat > /etc/yum.repos.d/wazuh.repo << EOF
        [wazuh]
        gpgcheck=1
        gpgkey=https://packages.wazuh.com/key/GPG-KEY-WAZUH
        enabled=1
        name=EL-\$releasever - Wazuh
        baseurl=https://packages.wazuh.com/4.x/yum/
        priority=1
        EOF```
    3. Install the agent:
        ``` # WAZUH_MANAGER='<insert_ip_here>' (sudo) dnf install wazuh-agent
    4. Enable the service, start the service, and check the status:
        `systemctl enable wazuh-agent && systemctl start wazuh-agent && systemctl status wazuh-agent`
    
## YUM
    1. Import the GPG Key:
        `rpm --import https://packages.wazuh.com/key/GPG-KEY-WAZUH`
    2. Add the repository (>= RHEL 8.0):
        ```cat > /etc/yum.repos.d/wazuh.repo << EOF
        [wazuh]
        gpgcheck=1
        gpgkey=https://packages.wazuh.com/key/GPG-KEY-WAZUH
        enabled=1
        name=EL-\$releasever - Wazuh
        baseurl=https://packages.wazuh.com/4.x/yum/
        protect=1
        EOF```
    2.a Add the repository (<= RHEL 9.0)
        ```cat > /etc/yum.repos.d/wazuh.repo << EOF
        [wazuh]
        gpgcheck=1
        gpgkey=https://packages.wazuh.com/key/GPG-KEY-WAZUH
        enabled=1
        name=EL-\$releasever - Wazuh
        baseurl=https://packages.wazuh.com/4.x/yum/
        priority=1
        EOF```
    3. Install the agent:
        ` # WAZUH_MANAGER='<insert_ip_here>' (sudo) dnf install wazuh-agent`
    4. Enable the service, start the service, and check the status:
        `systemctl enable wazuh-agent && systemctl start wazuh-agent && systemctl status wazuh-agent`

## Note that the configuration for the agent is stored at '/var/ossec/etc/ossec.conf'

# Windows
## Powershell
    1. Download the Windows installer from Wazuh:
        `Invoke-Webrequest -uri 'https://packages.wazuh.com/4.x/windows/wazuh-agent-4.14.5-1.msi' -OutFile wazuh-agent-4.14.15-1.msi`
    2. Install:
        `.\wazuh-agent-4.14.15-1.msi /q WAZUH_MANAGER='<insert_ip_here>'`
    3. Start the wazuhsvc service:
        `Start-Service wazuhsvc`
## CMD
    1. Download the Windows Istaller:
        `curl -O 'https://packages.wazuh.com/4.x/windows/wazuh-agent-4.14.5-1.msi' 
    2. Install:
        `wazuh-agent-4.14.15-1.msi /q WAZUH_MANAGER='<insert_ip_here>'`
    3. Start the service:
        `NET start Wazuhsvc`

## Note that the configuration file is stored at C:\\'Program Files (x86)'\ossec-agent