# Azure-SIEM-Project-with-Microsoft-Sentinel

## Objective
To implement a Security Information and Event Management (SIEM) system using Microsoft Sentinel on Azure to monitor Remote Desktop Protocol (RDP) activity on a virtual machine, enabling real-time detection, logging, and analysis of security events for enhanced threat visibility.

## Steps

### 1. Setting Up the Environment
a) Creating a Virtual Machine

•	I started by creating a virtual machine (VM) in Azure with preset configurations.

•	A resource group was created to manage all resources related to the project.


![image](https://github.com/user-attachments/assets/7ea45cf2-5aaa-46ed-9655-f7c95227d6a5)


 
b) Setting Up Microsoft Sentinel

•	I set up Microsoft Sentinel and linked it to a Log Analytics workspace named Ljoseph-loganalytics.

•	This workspace was tied to the resource group Ljoseph_group, ensuring that all logs and security events are collected in one place.



![image](https://github.com/user-attachments/assets/27ce930b-e51d-443a-98a6-f034ee0b1cca)

________________________________________
### 2. Collecting RDP Events

Since RDP traffic is easy to generate for monitoring purposes, I configured the system to track successful RDP sign-ins.

a) Connecting the VM to Log Analytics

•	The VM was connected to the Log Analytics workspace, but at this point, event logs were being collected without visibility in Sentinel.

b) Using Data Connectors

To forward logs from the VM to Sentinel, I set up a Data Connector, which enables connections to the broader security ecosystem:

•	Azure Monitor Agent (AMA): 
  
  o	This is the recommended method by Microsoft to ingest Security Events into Log Analytics.
  
  o	The legacy agent is being deprecated, so AMA is the preferred choice.

________________________________________

### 3. Configuring Security Monitoring

a) Creating a Data Collection Rule

•	I created a Data Collection Rule (DCR) in Azure Monitor Agent.

•	Selected the VM and enabled "All Security Events" to capture all security-related activities.

 
 ![image](https://github.com/user-attachments/assets/e6a12a1e-5a47-440e-85d8-70f5597980ee)


b) Setting Up Sentinel Analytics Rules

I configured Analytics Rules in Microsoft Sentinel to detect successful RDP sign-ins:

1.	Query for Successful RDP Sign-Ins: 

o	Security Event where activity contains “success”.

2.	Rule Setup for Alerting: 

o	Named: "Successful Local Sign-Ins"

o	Severity: Medium

o	MITRE ATT&CK Tactic: Initial Access

o	Query runs every 5 minutes to detect new sign-ins.

o	Alert threshold: Any event greater than 0 triggers an alert.

o	Incident Creation: Enabled to generate incidents from alerts.

________________________________________

### 4. Results & Observations

•	I left the SIEM running for 24 hours.

•	It generated 19 new incidents out of 1,300+ events, based on the rules set.

![image](https://github.com/user-attachments/assets/d737939d-0867-45aa-a28d-36ca29088a83)

•	Each incident can be analyzed in Sentinel’s Incident Overview tab for further investigation.

![image](https://github.com/user-attachments/assets/25292b88-e753-4a30-acdc-6ef1e48acebb)

![image](https://github.com/user-attachments/assets/e3884ea7-86e3-4321-a0e8-8ef30422cc6e)

________________________________________
## Conclusion

This project demonstrated how to set up Microsoft Sentinel on Azure to monitor RDP sign-ins. By using Log Analytics, Data Connectors, and Analytics Rules, I was able to generate real-time security insights.
________________________________________
## Next Steps & Improvements

•	Implement additional MITRE ATT&CK rules for other attack techniques.

•	Set up automated responses using Logic Apps to react to suspicious logins.

•	Monitor other security events like failed login attempts or brute-force attacks.


## Clone the repository
git clone https://github.com/LalithJoseph/Azure-SIEM-Project-with-Microsoft-Sentinel.git
