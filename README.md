## Azure SOC + Honeynet: Live Traffic Analysis
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

This project demonstrates the creation of a Security Operations Center (SOC) with a mini honeynet in Microsoft Azure. I integrated various log sources into a Log Analytics workspace, leveraging Microsoft Sentinel to generate attack maps, alerts, and incidents. Security metrics were collected over 24 hours in an insecure setup, followed by the application of security controls, with metrics re-evaluated for another 24 hours to showcase the impact.

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The mini honeynet in Azure is architected with these components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![image](https://github.com/user-attachments/assets/d6e3a6d7-9418-40c1-ba94-69e1c9be6296)<br>
![image](https://github.com/user-attachments/assets/8fedae24-a7c0-4752-9fc4-98b89c8219fa)<br>
![image](https://github.com/user-attachments/assets/993d00f2-ef9a-4bbe-b2c6-1e1fe8d12f12)<br>
![image](https://github.com/user-attachments/assets/fad25459-3d37-4e35-99bc-156b03ae25bf)


## Microsoft Sentinel SIEM with KQL queries
Microsoft Sentinel was configured with KQL-based alert rules to automate threat detection and incident creation.

![image](https://github.com/user-attachments/assets/175448d7-b5f3-4fce-9af9-b0f5a5b8cc6f)
![image](https://github.com/user-attachments/assets/184b44f4-2786-4a92-b93d-b8504e39798d)

The NIST 800-61 Incident Management Lifecycle was followed to manage incidents, improving threat visibility and response times.

![image](https://github.com/user-attachments/assets/472fbaa7-d396-4f61-a607-0909b523ad2b)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2025-02-18 13:54
Stop Time 2025-02-19 13:54

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 47884
| Syslog                   | 2399
| SecurityAlert            | 4
| SecurityIncident         | 288
| NSG Inbound Malicious Flows Allowed | 1808


## Enhanced cloud security using Microsoft Defender

Microsoft Defender for Cloud was enabled to strengthen the security posture, incorporating:

NIST 800-83 compliance features, 
Private endpoints, 
Virtual network restrictions, 
Firewalls to block public access

![image](https://github.com/user-attachments/assets/9ba6e854-f9cf-4dc5-8514-66a1dd0cbf85)
![image](https://github.com/user-attachments/assets/fda85ef3-a078-4960-9b38-4ed753aaa0f4)


## Metrics After Hardening / Security Controls

![image](https://github.com/user-attachments/assets/503d4974-d528-4a3a-b2a8-3980786d2368)

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-06-19 23:02
Stop Time	2024-06-20 23:02

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 16534
| Syslog                   | 6
| SecurityAlert            | 0
| SecurityIncident         | 0
| NSG Inbound Malicious Flows Allowed | 0

![image](https://github.com/user-attachments/assets/e940e227-2039-4286-8920-63122bd0c3a9)


## Conclusion

This project involved building a mini honeynet in Azure and integrating its logs into Log Analytics. Microsoft Sentinel was then used to generate alerts and incidents from this data. We also measured metrics in the insecure environment before and after applying security controls. The significant reduction in security events and incidents post-implementation highlights the effectiveness of these controls.

