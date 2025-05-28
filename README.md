<img src="https://github.com/AnderMendoza/AnderMendoza/raw/main/assets/line-neon.gif" width="100%">

![Github Banner 3 - Creating Active Directory Infrastructure in the Cloud (Azure) Banner](https://github.com/user-attachments/assets/a1e1d48d-80a0-4479-b267-fbb413f42ae2)

<img src="https://github.com/AnderMendoza/AnderMendoza/raw/main/assets/line-neon.gif" width="100%">

<h1>Establishing Active Directory Infrastructure in Microsoft Azure</h1>
This guide details the setup of an Active Directory infrastructure in Microsoft Azure, establishing the foundation for future Active Directory deployment and management projects.
<br/>

<h2>🚨Prerequisite🚨</h2>

- [Creating Virtual Machines in the Cloud](https://github.com/mxwllslvr/creating-virtual-machines-in-the-cloud)

<h2>Technologies Utilized</h2>

- Microsoft Azure (Compute/Virtual Machines)
- Remote Desktop Protocol (RDP) via mstsc
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems</h2>

- Windows 11 Home (24H2)
- Windows Server 2022
- Windows 10 (21H2)

<br/><br/><br/>

<h1>Deployment and Configuration Steps</h1>

<h3>Provision Resource Group and Virtual Machines:</h3>
<br/>

<p><img width="850" alt="image" src="https://github.com/user-attachments/assets/5b154674-045f-4029-afd1-1886b5e409dd"/></p>
<p>In the Azure Portal, create a new Resource Group named CloudInfraRG. Click Review + Create and Create.</p>
<br/><br/>

<p><img width="850" alt="image" src="https://github.com/user-attachments/assets/05e349cc-b7a5-4f09-bebd-2559bc08aa55"/></p>
<p>Deploy two Virtual Machines within the same Virtual Network and region (e.g., (US) East US 2). 

<i>Refer to the <a href="https://github.com/mxwllslvr/creating-virtual-machines-in-the-cloud">prerequisite guide for VM creation</a> details if needed.</i>
<br/><br/><br/>
Configure the first VM:

```
Name: DC-1 (Domain Controller)
Image: Windows Server 2022
Size: At least Standard_D2s_v5 (2 vCPUs, 8 GiB memory)
```

Configure the second VM:

```
Name: Client-1 Image: Windows 10 Pro
Size: At least Standard_D2s_v5 (2 vCPUs, 8 GiB memory)
```
<br/>
Record the Public IP addresses for both VMs and the Private IP address for DC-1 (e.g., 10.0.0.4) for RDP and configuration purposes.</p>
<br/><br/>
