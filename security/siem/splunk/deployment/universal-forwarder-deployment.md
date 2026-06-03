## Overview
This section covers the deployment and configuration of Splunk's universal forwarder, followed by verification of log ingestion after the installation of [[portfolio/security/siem/splunk/deployment/splunk-install|Splunk]]
## Procedure

This follows the installation the Splunk Universal Forwarder on a Linux DNS server. 
  

1. Navigated to the Splunk Universal Forwarder's website, located [here](https://www.splunk.com/en_us/download/universal-forwarder.html).  
      
    
2. Logged into the shell for my Linux instance, and elevated to root privileges.  
      
    
3. created the `/opt/splunkforwarder` directory.  
      
    
4. Downloaded and installed the forwarder to the `/opt/splunkforwarder` directory using cURL.  
      
    
5. Navigated to the `/opt/splunkforwarder/bin` directory and ran `./splunk start` then accepted the license agreement.  
      
    
6. While still in `/opt/splunkforwarder/bin`, used `./splunk add forward-server <splunk_installation_ip>:<port>`. E.g. `splunk.lab.net:9997` to add the forwarder server.  
      
    
7. Finally, used `./splunk add monitor /var/log/audit/audit.log` to add the `audit.log` of Auditd for forwarding.  
      
    
8. Navigated back to the Splunk dashboard, then to `Search & Reporting`.  
      
    
9. In the search box inputted `Index=* source="/var/log/audit/audit.log"`. Verifying that the Splunk instance is receiving logs from my forwarder.

## Conclusion
Proper configuration and verification of proper operation is crucial to assure that all the necessary information are being forwarded to the SIEM.