# Configuring On-premises Active Directory within Azure VMs 🖥️🔐

This guide walks through the setup and configuration of an **on-premises-style Active Directory Domain Services (AD DS)** environment within **Microsoft Azure virtual machines**. Perfect for lab testing, hybrid environments, or learning enterprise identity management.

---

## 🌐 Technologies Used

- Microsoft Azure (Virtual Machines)
- Windows Server 2022
- Active Directory Domain Services (AD DS)
- Remote Desktop Protocol (RDP)

---

## 🧱 Architecture Overview

- **1 Domain Controller (DC-1)** - Hosts Active Directory, DNS, and Group Policy
- **1 Client Machine (Client-1)** - Joins the domain and tests authentication

Both machines are deployed in the same virtual network (VNet) with a private IP address scheme.

---

## 🛠️ Setup Steps

### 1. Create the Azure VMs
- Create two Windows Server VMs in the same **Resource Group** and **Virtual Network**
- Name them `DC-1` and `Client-1`
- Ensure both VMs are using the **same subnet**
- Allow **RDP (port 3389)** through the NSG for remote access

### 2. Configure `DC-1` (Domain Controller)
- Rename the computer to `DC-1`
- Set a **static private IP address**
- Open **Server Manager** → `Add Roles and Features`
  - Install **Active Directory Domain Services** and **DNS Server**
- Promote the server to a **domain controller**
  - New Forest: `yourdomain.local`

### 3. Configure DNS for `Client-1`
- Set `Client-1`'s **preferred DNS** to `DC-1`'s private IP (e.g., `10.0.0.4`)
- Rename the computer to `Client-1`
- Join it to the domain:
  - `System Properties → Change Settings → Domain: yourdomain.local`

### 4. Test Domain Join
- Log in to `Client-1` using domain credentials
- Verify domain policies and DNS resolution

---

## ✅ Post-Configuration Checklist

- [x] `DC-1` is a domain controller and DNS server  
- [x] `Client-1` is domain joined  
- [x] RDP working for both VMs  
- [x] Users and OUs can be created in Active Directory  

---

## 🎓 Tips

- Use **Group Policy Management** on `DC-1` to configure user/workstation policies.
- You can add more clients to simulate a full enterprise network.
- Create users in `Active Directory Users and Computers (ADUC)` to test logins.

---

## 📌 Example Use Cases

- Lab testing for MCSA, Azure, or AD certifications
- Practicing Group Policy configuration
- Testing login scripts, shared drives, and AD integration

---

> This lab simulates an on-premises environment completely within Azure — no physical hardware required!
