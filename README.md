# enterprise-ad-lab-build
Simulated small business: Northbridge Solutions Inc. IT required to deploy on-prem Active Directory for centralized authentication and resource management.

---

# Enterprise Active Directory Lab Build

**Simulated Small Business Deployment — Northbridge Solutions Inc.**

---

## 📌 Project Overview

This project documents the deployment of a small business on-premises Active Directory environment using virtualization.

The goal was to simulate a real-world IT infrastructure build for centralized authentication, DNS management, and workstation domain integration.

This lab was designed to demonstrate foundational IT Support competencies required for Level 1 / Level 2 roles.

---

## 🏢 Business Scenario

Northbridge Solutions Inc. required centralized identity management to:

* Authenticate users through Active Directory
* Manage users and security groups
* Enable controlled access to shared resources
* Standardize workstation login via domain accounts
* Support future Group Policy enforcement

IT was tasked with deploying a Domain Controller and joining client machines to the domain.

---

## 🖥 Lab Environment

**Platform:** Oracle VirtualBox
**Domain Name:** `lab.local`
**Server OS:** Windows Server 2022 (Desktop Experience)
**Client OS:** Windows 10
**Network Type:** Internal Network

### Infrastructure

* **DC01**

  * Role: Domain Controller + DNS Server
  * IP Address: `192.168.10.10`
  * Services Installed:

    * Active Directory Domain Services (AD DS)
    * DNS Server

* **CLIENT01**

  * Domain-joined Windows 10 machine
  * DNS configured to point to `192.168.10.10`

---

## 🧭 Architecture Overview

![Image](https://media.licdn.com/dms/image/v2/D4D12AQGV9esQC0ILPA/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1661333506982?e=2147483647\&t=0KfhXBBipaESxVpnQF8MfR2fQdAF_eDCVs3EPt60ylA\&v=beta)

![Image](https://learn.microsoft.com/en-us/windows-server/remote/media/step-2-plan-the-multisite-infrastructure/ramultisitetopo1.png)

![Image](https://sandilands.info/sgordon/images/virtnet/virtualbox-topology-csr-2.png)

![Image](https://user.oc-static.com/upload/2021/08/10/16285905987723_STATIC-GRAPHICS_2c4-2%20copy.png)

---

## 🔧 Implementation Steps

### 1️⃣ Installed Windows Server 2022

* Created VM in VirtualBox
* Allocated RAM and storage
* Installed OS with Desktop Experience

### 2️⃣ Configured Static IP on DC01

* IP: `192.168.10.10`
* Subnet: `255.255.255.0`
* DNS: `192.168.10.10` (self-reference after AD install)

**Why:**
Domain Controllers must use static IP addresses to ensure consistent DNS resolution.

---

### 3️⃣ Installed Active Directory Domain Services

* Added AD DS role via Server Manager
* Promoted server to Domain Controller
* Created new forest: `lab.local`

**Why:**
This establishes centralized authentication and directory services.

---

### 4️⃣ Verified DNS Functionality

* Confirmed forward lookup zone created
* Tested resolution via:

  ```
  nslookup
  ping DC01
  ```

**Why:**
Active Directory depends entirely on DNS for authentication and domain services.

---

### 5️⃣ Configured CLIENT01

* Installed Windows 10 VM
* Set DNS server to `192.168.10.10`
* Joined machine to `lab.local`
* Verified successful login using domain credentials

---

## ✅ Validation & Testing

The following validation checks were performed:

* Domain login successful on CLIENT01
* DNS resolution functioning
* Domain Controller reachable via ping
* ADUC console accessible
* Event Viewer reviewed for errors
* Replication status verified (single DC environment)

---

## 🛠 Troubleshooting Encountered

### Issue: “Destination Host Unreachable”

**Cause:**
Incorrect IP configuration on client machine.

**Resolution:**

* Verified configuration using `ipconfig /all`
* Corrected DNS server to `192.168.10.10`
* Flushed DNS cache
* Retested connectivity

---

### Issue: Domain Join Failure

**Cause:**
Client not pointing to internal DNS.

**Resolution:**

* Adjusted network adapter to Internal Network
* Ensured DNS pointed to Domain Controller
* Re-attempted domain join successfully

---

## 🧠 Skills Demonstrated

* Windows Server installation & configuration
* Static IP configuration
* Active Directory Domain Services deployment
* DNS management fundamentals
* Domain join process
* Basic troubleshooting methodology
* Log review and validation
* Structured documentation

---

## 🔐 Security Considerations

* Administrator credentials secured
* Default passwords changed after setup
* Password complexity enforced
* Domain access limited to authorized accounts

---

## 📈 Lessons Learned

* DNS configuration is critical for AD functionality.
* Static IP misconfiguration is a common root cause of domain failures.
* Proper network isolation (Internal Network) prevents cross-network conflicts.
* Structured validation reduces troubleshooting time.

---

## 🎯 Outcome

The deployment successfully simulated a small business AD environment capable of:

* Centralized authentication
* User lifecycle management
* Secure workstation domain access
* Foundation for Group Policy implementation
* Scalable group and permission architecture

This project demonstrates foundational enterprise IT Support capabilities aligned with real-world corporate environments.

---

---


