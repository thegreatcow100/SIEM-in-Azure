# Security Information and Event Management in Azure

# Introduction

In this project, I built a honeypot using a virtual machine in Microsoft Azure. Microsoft Log Analytics workspace collected and stored the logs from the virtual machine. The logs were then utilized by Microsoft Sentinel to build an attack map to visualize the data. The data were collected over 24 hours, during which all traffic was allowed into the system. The system was then hardened, and data were collected for another 24 hours.

---

## Resources Utilized

- **[Azure Virtual Machines (VM)](https://learn.microsoft.com/en-us/azure/virtual-machines/overview) :** Host honeypot.  

- **[Windows 10](https://www.microsoft.com/en-us/software-download/windows10) :** Operating system utilized in VM. 

- **[Azure Network Security Groups](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) :** Configure firewall security rules for VM port traffic.  

- **[Azure Log Analytics Workspace](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview) :** Collect failed connection logs from the VM event viewer.  

- **[Microsoft Defender](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-cloud-introduction) :** Configured security for cloud resources.

- **[Microsoft Sentinel](https://learn.microsoft.com/en-us/azure/sentinel/overview?tabs=azure-portal) :** Visualize collected data from Log Analytics Workspace into an attack map.
  
- **[Windows Remote Desktop](https://support.microsoft.com/en-us/windows/how-to-use-remote-desktop-5fe128d5-8fb1-7a23-3b8a-41e636865e8c) :** Access VM as administrator.  

- **[Event Viewer](https://learn.microsoft.com/en-us/shows/inside/event-viewer) :** View failed connections to virtualized Windows machines in real-time.  

- **[Microsoft Powershell](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.4&viewFallbackFrom=powershell-7.3) :** Used Powershell script to automate log collection.  

- **[Geolocation API](https://ipgeolocation.io/documentation.html) :** Gather location data of bad actors based on IP address.  
 
---

## Methods

### Creating the Honeypot  
The Honeypot was created using Azure Virtual Machine (VM). After creating the VM with a Windows image, Azure Network Security Groups were employed to open all ports and allow all traffic into the VM. Inside the VM, the firewall was turned off.  


### Tracking  
Event log data from the VM was collected using Azure Log Analytics Workspace. Within the VM, PowerShell scripting was utilized to automate the process of gathering failed authentication logs from the Event Viewer. These logs were then assembled into a text document which was then forwarded to the Azure Log Analytics Workspace.  


### Examination  
As incoming traffic is received, the PowerShell script collects all failed port connections and saves the data into a text document. Azure Log Analytics Workspace then gathers the data in the text document and stores it as a data log.  

- The first dataset was collected over 24 hours, during which the VM's firewall was disabled, allowing unrestricted traffic into the system.  
- After hardening the system, data was recollected over another 24-hour period with the firewall enabled and the VM's port settings reconfigured.  


### Mapping  
The script uses a geolocation API to take logs and find their longitude and latitude. Subsequently, Microsoft Sentinel takes the geolocation and attack data to generate a visual map. Sentinel was used to create an attack map visualizing the log data gathered during the vulnerable and hardened 24-hour periods. The log counts between the vulnerable and the hardened systems were compared to determine discrepancies.

---

## Attack Map Before  

![Map before](https://github.com/user-attachments/assets/071e1117-8aa2-4cf4-bc84-acba40656d2c)

This attack map indicates the RDP failures over a 24-hour timeframe. In this timeframe, there were approximately **9.5k failed RDP connections** to the network. Despite being a network unaffiliated with any specific company, it still evidenced a significant volume of traffic. This underscores the constant efforts of actors attempting to breach systems at all hours of the day.

---

## Attack Map After

![Map after](https://github.com/user-attachments/assets/8836953d-5d63-4a7a-b910-1f645c47597b)

This attack map demonstrates the RDP failures over a 24-hour timeframe after hardening. In this timeframe, there were approximately **90 failed RDP connections** to the network. Although a few bad actors attempted to force their way into the system, implementing system-hardening measures made a significant impact.

There was a **99.05% decrease in failed connection attempts** after system hardening was conducted.

---

## Reflection

This project was a joy to complete. As a novice in the cybersecurity field, it was a wonderful opportunity to apply newfound skills gained from courses and research to create this project. Working inside a cloud environment for the first time was a daunting task, as there were many resources that I had to learn from scratch. Understanding the tools in the cloud taught me a foundational skillset that I can apply to other cloud platforms in the future. Observing bad actors attempting to attack your machine in real-time and watching the attack map develop over time was truly exciting. After system hardening and recollecting the data, the drastic decrease in attack traffic was rewarding. Given that some traffic still entered, it emphasizes the opportunity to further improve my skills and discover more ways to reduce the attack surface of my VM.

---

## Conclusion

This project involved the creation of a honeypot within a VM. A large amount of log data was collected and analyzed using various tools available within the Microsoft Azure cloud ecosystem. Powershell scripting was used to automate the data collection process, and a geolocation API was used to gather pivotal information required to visualize the data. The reduction in traffic from pre- to post-hardening underscores the importance of implementing security measures on networks and devices.




