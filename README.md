<img src="https://github.com/AnderMendoza/AnderMendoza/raw/main/assets/line-neon.gif" width="100%">

![Github Banner 3 - Creating Active Directory Infrastructure in the Cloud (Azure) Banner](https://github.com/user-attachments/assets/a1e1d48d-80a0-4479-b267-fbb413f42ae2)

<img src="https://github.com/AnderMendoza/AnderMendoza/raw/main/assets/line-neon.gif" width="100%">

# Establishing Active Directory Infrastructure in Microsoft Azure

This guide details the setup of an Active Directory infrastructure in Microsoft Azure, establishing the foundation for future Active Directory deployment and management projects.

## 🚨 Prerequisites

- [Creating Virtual Machines in the Cloud](https://github.com/mxwllslvr/creating-virtual-machines-in-the-cloud)

## Technologies Utilized

- Microsoft Azure (Compute/Virtual Machines)
- Remote Desktop Protocol (RDP) via mstsc
- Active Directory Domain Services
- PowerShell

## Operating Systems

- Windows 11 Home (24H2)
- Windows Server 2022
- Windows 10 (21H2)

---

# Deployment and Configuration Steps

## Step 1: Provision Resource Group and Virtual Machines

### Create Resource Group

![Resource Group Creation](https://github.com/user-attachments/assets/5b154674-045f-4029-afd1-1886b5e409dd)

In the Azure Portal, create a new Resource Group named **CloudInfraRG**. Click **Review + Create** and **Create**.

### Deploy Virtual Machines

![VM Deployment](https://github.com/user-attachments/assets/05e349cc-b7a5-4f09-bebd-2559bc08aa55)

Deploy two Virtual Machines within the same Virtual Network and region (e.g., **(US) East US 2**).

*Refer to the [prerequisite guide for VM creation](https://github.com/mxwllslvr/creating-virtual-machines-in-the-cloud) details if needed.*

**Configure the first VM:**
- **Name**: DC-1 (Domain Controller)
- **Image**: Windows Server 2022
- **Size**: At least Standard_D2s_v5 (2 vCPUs, 8 GiB memory)

**Configure the second VM:**
- **Name**: Client-1
- **Image**: Windows 10 Pro
- **Size**: At least Standard_D2s_v5 (2 vCPUs, 8 GiB memory)

Record the Public IP addresses for both VMs and the Private IP address for **DC-1** (e.g., 10.0.0.4) for RDP and configuration purposes.

---

## Step 2: Set Static Private IP for DC-1

### Navigate to Network Interface

![Network Interface Navigation](https://github.com/user-attachments/assets/5f76a9bd-0c09-4603-9c36-a83df2a1772f)

1. Navigate to **Virtual Machines**, select **DC-1**, and access **Networking**
2. Click the **Network interface** link

### Configure Static IP

![Static IP Configuration](https://github.com/user-attachments/assets/af3552f3-e0d5-4662-8a1d-aad0634a38f4)

1. Select **IP configurations** and click **ipconfig1**
2. Under **Private IP address settings**, change **Allocation** to **Static**
3. Confirm the Private IP (e.g., 10.0.0.4) remains unchanged and click **Save**
4. Verify the static IP is applied in the IP configurations view

A static IP ensures **DC-1's** address remains consistent, which is critical for its role as a domain controller.

---

## Step 3: Establish RDP Connection to DC-1

![RDP Connection](https://github.com/user-attachments/assets/0eac8db9-0d5a-4b79-a9d5-57455ba0496c)

1. On your local Windows device, open the Run dialog (**Windows + R**) and type `mstsc` to launch the Remote Desktop Connection client
2. Enter **DC-1's** Public IP address and the Username created for **DC-1**. Click **Connect**
3. Authenticate using the password created for **DC-1**

Upon connection, confirm the Server Manager Dashboard appears, indicating a proper Windows Server 2022 environment. If a standard Windows desktop appears, verify **DC-1's** configuration in Azure.

---

## Step 4: Disable DC-1 Firewall

![Firewall Configuration](https://github.com/user-attachments/assets/acfc102f-4723-4899-93a9-5229b73563cb)

1. On **DC-1**, right-click the Start menu, select **Run**, type `wf.msc`, and press **Enter** to open Windows Defender Firewall settings
2. Click **Windows Defender Firewall Properties**
3. For **Domain Profile**, **Private Profile**, and **Public Profile**, set **Firewall state** to **Off**
4. Click **Apply** and **OK** for each tab to save changes

---

## Step 5: Configure Client-1 DNS Settings

### Navigate to Client-1 Network Settings

![Client-1 Navigation](https://github.com/user-attachments/assets/e9e8b9c2-24f9-4b96-bd4f-3adb12becf8b)

In the Azure Portal, navigate to **Virtual Machines**, select **Client-1**.

![Client-1 Networking](https://github.com/user-attachments/assets/dc816f59-eb1b-4ca2-a844-29f3663197ba)

Go to **Networking**. Click the **Network interface** link.

### Configure DNS Server

![DNS Configuration](https://github.com/user-attachments/assets/8af6b824-f195-4c9c-b7c1-bcf6ac453f60)

1. Select **DNS servers**
2. Choose **Custom** and enter **DC-1's** Private IP address (e.g., 10.0.0.4) as the DNS server
3. Click **Save**

### Restart Client-1

Restart **Client-1** to apply the DNS change:
1. Return to **Virtual Machines**, check **Client-1**
2. Click **Restart**, and confirm the action

---

## Step 6: Connect to Client-1, Test Connectivity, and Verify DNS Configuration

![Client-1 Testing](https://github.com/user-attachments/assets/efc3cf6a-7b07-4666-88c1-3f03bb90b0e8)

### Establish RDP Connection
1. Using `mstsc`, enter **Client-1's** Public IP address and connect with the appropriate username and password
2. Once connected, open PowerShell via the Start menu search

### Test Connectivity and DNS Configuration
1. In PowerShell on **Client-1**, run `ping 10.0.0.4` to test connectivity to **DC-1**
   - Successful replies confirm both VMs are on the same Virtual Network and **DC-1's** firewall is disabled
2. Execute `ipconfig /all` to display network configuration
3. Confirm the **DNS Server** is set to **DC-1's** Private IP (e.g., 10.0.0.4), ensuring **Client-1** uses **DC-1** for DNS resolution

---

<br/><br/>

<div align="center"> <img src="https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExMDh4OGptcm5ma2V2emw4bHAwdm1sdG13aGU4bHNjZHZiNG1rcTg5dCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xThuWcZzGnonnG3ayQ/giphy.gif" width="100%"> </div>

<br/><br/>

<img src="https://github.com/AnderMendoza/AnderMendoza/raw/main/assets/line-neon.gif" width="100%">

## Conclusion

This procedure successfully established an Active Directory infrastructure in Microsoft Azure, comprising a Resource Group (**CloudInfraRG**), a domain controller (**DC-1**), and a client machine (**Client-1**). This setup forms the basis for future Active Directory projects, including domain deployment.

**Key Achievements:**
- Created a dedicated resource group for AD infrastructure
- Configured a Windows Server 2022 domain controller with static IP
- Set up a Windows 10 client with proper DNS configuration
- Established network connectivity between domain controller and client
- Prepared the foundation for Active Directory domain services

The configuration highlights the efficiency of cloud-based infrastructure management. To optimize costs, stop both VMs in Azure when not in use. This concludes the setup process, preparing you for advanced Active Directory implementations.

<img src="https://github.com/AnderMendoza/AnderMendoza/raw/main/assets/line-neon.gif" width="100%">

<br/><br/>

<div align="center">

<a href="HTTP://www.github.com/mxwllslvr">- BACK TO MAIN PAGE -</a>

</div>
