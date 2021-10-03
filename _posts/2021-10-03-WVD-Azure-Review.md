# WVD Azure Review
---
Windows Virtual Desktop (WVD)

### 6 Controls to check

1. [Identity - Conditional Access, MEM support, MFA](#1)
2. [Session Host - Defender ATP, Policies](#2)
3. [Apps - Application Control, Applocker](#3)
4. [Infrastructure - Azure Security Center, Secure Score, Best Practices](#4)
5. [Networking - Reverse Connect, Service tags, Firewall](#5)
6. [Data - Information Protection, Azure Disk Encryption](#6)
---

## Identity <a name="1"></a>
Security Controls and best practices

**Require Multi-Factor Authentication**
  * Activate Azure MFA for Azure AD Accounts

**Enable Conditional Access**
  * Configure a Conditional Access Policy and Target WVD

**MEM Support (Microsoft Endpoint Manager)**
  * Windows 10 Enterprise (hybrud AAD) support GA

https://aka.ms/mfawvd

## Session Host <a name="2"></a>
Security Controls and best practices

**Microsoft Defender ATP**
  * Next-generation Antivirus
  * Endpoint Detection and response
  * Network Protection, Web content filtering, attack surface reduction
  * Threat Vulnerability Management

**Patch software vulnerabilities**
  * Update live host or redeploy using latest gallery image

**Control device redirections**
  * look into disabling smart card, port, drives, camera redirection

**Windows security baseline**
  * Apply windows 10 security baseline

**Define Group Policies**
  * Set time limit for active but idle remote desktop services sessions
  * Set time limit for disconnected sessions (be careful of data loss)

## Apps <a name="3"></a>
Security Controls and best practices

**App locker**
  * Control what applications users can run

**Application control**
  * Control what drivers and applications can run

https://aka.ms/wvdappssec

## Networking <a name="4"></a>
Security Controls and best practices

**Reverse Connect**
  * Disable all inbound traffic
  * Connects via a lightweight agent over tcp/443

**NSG Firewall service tags**
  * Limit network-level traffic WVD traffic with service tags

**Firewall**
  * Consider Azure Firewall for application-level protection with WindowsVirtualDesktop FQDN tag

https://aka.ms/wvdfirewall

## Infrastructure <a name="5"></a>
Security Controls and best practices

**Enable Azure Defender and Azure Security Center**
  * Providers threat and vulnerability management assessments

**Operationalize your secure score**
  * Secure score provides recommendations and best practice advice for increasing your security posture

**Follow Azure best practices**
  * Secure surrounding infrastructure with documented best practices

https://aka.ms/azuresecurebp

## Data <a name="6"></a>
Security Controls and best practices

**Microsoft Information Protection**
  * Discover, classify, and protect sensitive information where ever it lives

**Azure Disk Encryption**
  * Helps protect and safeguard your data

Extra Link - [https://docs.microsoft.com/en-us/azure/virtual-desktop/](https://docs.microsoft.com/en-us/azure/virtual-desktop/)
