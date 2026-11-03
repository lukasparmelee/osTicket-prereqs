# Azure Network Security Groups & Network Traffic Analysis

**Hands-on networking lab | Microsoft Azure · Wireshark · Windows 10 · Ubuntu Linux**

## Project overview

Built a two-VM lab in Microsoft Azure to observe network protocols with Wireshark and test how Network Security Group (NSG) rules affect connectivity. The environment included a Windows 10 VM and an Ubuntu 22.04 LTS VM on a shared virtual network. This repository documents the original setup, experiments, observations, and supporting screenshots.

**Skills demonstrated:** Virtual networking, packet capture and filtering, ICMP troubleshooting, NSG rule testing, SSH, DNS, DHCP, RDP, Windows and Linux command-line tools.

> **Scope:** Personal learning lab, not a production deployment. Azure resources used for the lab have since been deleted. Example credentials are redacted; never reuse demonstration passwords.

## Quick navigation

- [Original lab walkthrough and evidence](#original-lab-walkthrough-and-evidence)
- [What this project demonstrates](#what-this-project-demonstrates)

## What this project demonstrates

- **Connectivity testing:** Used ping and Wireshark to inspect ICMP requests and replies.
- **Network controls:** Changed an Azure NSG rule and observed the effect on packet delivery, then restored connectivity.
- **Protocol analysis:** Examined SSH, DHCP, DNS, and RDP traffic in a controlled environment.
- **Documentation:** Recorded lab configuration, commands, observations, and screenshots for repeatability.

## Original lab walkthrough and evidence

The detailed walkthrough below is preserved from the original repository documentation, including its screenshot references. The only intentional content change is redacting a demonstration password.

---

[![Traffic Examination](https://camo.githubusercontent.com/3a8495cd3d36fd2394f1ab608d4ab8ef61c09b0b44a88df5885689ff23f152b5/68747470733a2f2f692e696d6775722e636f6d2f55613775646f532e706e67)](https://camo.githubusercontent.com/3a8495cd3d36fd2394f1ab608d4ab8ef61c09b0b44a88df5885689ff23f152b5/68747470733a2f2f692e696d6775722e636f6d2f55613775646f532e706e67)

# Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines

In this tutorial, we observe various network traffic to and from Azure Virtual Machines using Wireshark and experiment with Network Security Groups (NSGs) to understand how traffic filtering impacts communication between systems.   


---

## 🧠 Environments and Technologies Used

- Microsoft Azure (Virtual Machines / Compute)
- Remote Desktop Protocol (RDP)
- PowerShell & Linux Command-Line Tools
- Wireshark (Protocol Analyzer)
- Network Protocols: ICMP, SSH, DHCP, DNS, RDP

---

## 💻 Operating Systems Used

- Windows 10 (21H2)
- Ubuntu 22.04 LTS

---

## ⚙️ High-Level Steps

- Create Resource Group and Virtual Machines in Azure
- Capture and Analyze Network Traffic with Wireshark
- Configure Network Security Groups (Firewall)
- Observe Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Clean Up Azure Resources

---

## 🧩 Actions and Observations

### **Part 1: Creating Virtual Machines**

[![Azure VM Creation](./windows.png)](./windows.png)
[![Azure VM Creation](./linux.png)](./linux.png)

In the Azure Portal, a new Resource Group was created along with two Virtual Machines: a Windows 10 VM and an Ubuntu (Linux) VM. Both were placed within the same Virtual Network (VNet) and Subnet to enable internal communication.

- Resource Group: `RG-Network-Activities`
- Network: `lab2-vnet`
- Authentication: Username: labuser / Password: [REDACTED LAB PASSWORD]
- Validation: Both VMs successfully connected within the same private network.

✅ **Result:** Two connected VMs in one virtual network.

---

### **Part 2: Observing ICMP Traffic**

[![ICMP Ping Capture](./ws.png)](./ws.png)

Wireshark was installed on the Windows 10 VM to capture ICMP traffic. A ping command was sent to the Ubuntu VM's private IP address, and ICMP Echo Requests and Replies were successfully observed in real-time within Wireshark.

---

### Part 3: Configuring Network Security Group (Firewall)

[![Network Security Group Rules](./ping.png)](./ping.png)
[![Network Security Group Rules](./rule.png)](./rule.png)
[![Network Security Group Rules](./timeout.png)](./timeout.png)

A continuous ping was initiated from the Windows VM to the Ubuntu VM. The inbound ICMP rule was then created in the Ubuntu VM’s Network Security Group (NSG).
Ping requests immediately began timing out, and Wireshark confirmed that no ICMP replies were received.

---

[![Network Security Group Rules](./re-enable.png)](./re-enable.png)

After deleting the ICMP rule in the NSG, connectivity was restored and the pings resumed successfully.

---

### Part 4: Observing SSH Traffic

[![SSH Traffic Capture](./ssh.png)](./ssh.png)

After restoring ICMP connectivity, I moved on to capture and analyze SSH traffic. In Wireshark, I applied the SSH filter and initiated an SSH session from the Windows VM to the Ubuntu VM using PowerShell.

Once connected, I entered several basic commands such as `pwd` and `ls` to generate traffic. Wireshark displayed continuous encrypted SSH packets representing command execution and communication between the two virtual machines. After verifying the session, I exited the SSH connection.

---

### Part 5: Observing DHCP Traffic

[![DHCP Renewal Capture](./DHCP.png)](./DHCP.png)

To observe DHCP behavior, I filtered Wireshark using the `udp.port == 67 || udp.port == 68` keyword and initiated a DHCP renewal on the Windows 10 VM.

I ran ipconfig /release and ipconfig /renew this triggered DHCP Discover, Offer, Request, and Acknowledge packets, visible in real-time on Wireshark. The process confirmed how the VM requests a new IP lease from the DHCP server on the network.

---

### Part 6: Observing DNS Traffic

[![DNS Query Capture](./dns.png)](./dns.png)

Next, I analyzed DNS queries to external domains. In Wireshark, I filtered for `dns` traffic, then used the `nslookup` tool to query multiple websites.

Wireshark displayed DNS Query and Response packets, confirming domain name resolution and returning the appropriate IP addresses for each domain.

---

### Part 7: Observing RDP Traffic

[![RDP Traffic Analysis](./rdp.png)](./rdp.png)

Finally, I captured Remote Desktop Protocol (RDP) traffic between my local machine and the Windows VM.
Wireshark was filtered to show only RDP packets using the expression:

RDP traffic appeared as continuous packet streams because the protocol constantly transmits live screen updates, keyboard input, and mouse activity in real-time.

---

