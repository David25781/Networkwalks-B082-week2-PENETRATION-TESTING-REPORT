# 🛡️ PENETRATION TESTING REPORT

### Footprinting, Reconnaissance & Network Scanning

<p align="center">

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

</p>

---

## 👤 Pentester

**David Fumeira Ndjimbo**
*Cybersecurity Professional*

| Information           | Details                             |
| --------------------- | ----------------------------------- |
| 🎓 Program / Batch    | **B082 – Networkwalks**             |
| 📅 Date               | **19 August 2026**                  |
| 📚 Week               | **02**                              |
| 🎯 Focus              | **Footprinting & Network Scanning** |
| 🖥️ Operating Systems | **Kali Linux & Windows**            |
| 🔐 Authorization      | **Authorized / Own Local Network**  |

---

## 📌 Scope

This week's activities covered two main penetration testing phases:

* **Phase 1 — Reconnaissance & Footprinting**
* **Phase 2 — Scanning & Network Discovery**

### Authorized Targets

1. **Networkwalks — `networkwalks.com`**
2. **My own local LAN network**

> ⚠️ **Authorization Notice:** Activities against the Networkwalks domain were performed under the authorized internship environment. Network scanning was performed against my own local network.

---

# 📑 Table of Contents

* [1. Disclaimer](#1--disclaimer)
* [2. Introduction](#2--introduction)
* [3. Objectives](#3--objectives)
* [4. Tools Used](#4--tools-used)
* [5. Phase 1 — Footprinting & Reconnaissance](#5--phase-1--footprinting--reconnaissance)

  * [WHOIS](#51--whois)
  * [WhatWeb](#52--whatweb)
  * [nslookup](#53--nslookup)
  * [cURL](#54--curl)
  * [WAFW00F](#55--wafw00f)
  * [DNSRecon](#56--dnsrecon)
* [6. Phase 2 — Network Scanning](#6--phase-2--network-scanning)

  * [Zenmap / Nmap](#61--zenmap--nmap)
  * [Windows CMD](#62--windows-cmd)
* [7. Findings & Risk Analysis](#7--findings--risk-analysis)
* [8. Recommendations](#8--recommendations)
* [9. Conclusion](#9--conclusion)
* [10. Evidence](#10--evidence)
* [11. Author](#11--author)

---

# 1. ⚠️ Disclaimer

All activities documented in this repository were performed for **authorized educational and cybersecurity training purposes**.

Testing was limited to:

* Systems for which authorization was provided.
* My own devices and local network.
* Passive reconnaissance and network discovery activities within the defined scope.

No exploitation, destructive activity, credential attacks, denial-of-service testing, or unauthorized access was performed as part of these exercises.

> **Important:** Unauthorized access or security testing against systems you do not own or have permission to test may be illegal. Always obtain appropriate authorization before performing security assessments.

---

# 2. 📖 Introduction

During **Week 2 of my Cybersecurity Internship at Networkwalks**, I focused on the initial phases of penetration testing: **reconnaissance, footprinting, and network discovery**.

The first part involved gathering publicly available technical information about:

```text
networkwalks.com
```

using several Kali Linux reconnaissance tools.

The second part involved using **Zenmap/Nmap** to discover live hosts on my own local network.

The objective was to understand how penetration testers move from collecting information about a target to identifying active systems within an authorized environment.

---

# 3. 🎯 Objectives

The main objectives of Week 2 were:

* 🔎 Perform domain reconnaissance.
* 🌐 Identify DNS infrastructure.
* 🧩 Fingerprint web technologies.
* 📡 Resolve domain names to IP addresses.
* 📋 Analyze HTTP response headers.
* 🛡️ Identify Web Application Firewall protection.
* 🗂️ Enumerate DNS records.
* 🖥️ Discover live hosts on a local network.
* 🔗 Identify IP and MAC addresses.
* 🗺️ Build a basic network topology.
* 📊 Analyze the security relevance of collected information.

---

# 4. 🛠️ Tools Used

| Tool                  | Purpose                                             |
| --------------------- | --------------------------------------------------- |
| 🐉 **Kali Linux**     | Reconnaissance and security assessment platform     |
| 🪟 **Windows**        | Local network identification and Zenmap environment |
| 🔍 **WHOIS**          | Domain registration and name server information     |
| 🕵️ **WhatWeb**       | Web technology fingerprinting                       |
| 🌐 **nslookup**       | DNS name-to-IP resolution                           |
| 📡 **cURL**           | HTTP response/header analysis                       |
| 🛡️ **WAFW00F**       | Web Application Firewall detection                  |
| 🗂️ **DNSRecon**      | DNS record enumeration                              |
| 🗺️ **Zenmap / Nmap** | Network and host discovery                          |
| 💻 **Windows CMD**    | Local IP and MAC address identification             |

---

# 5. 🔎 Phase 1 — Footprinting & Reconnaissance

The first phase focused on gathering information about the `networkwalks.com` domain using multiple Kali Linux tools.

---

## 5.1 WHOIS

### Command

```bash
whois networkwalks.com
```

### Key Findings

| Information     | Result                 |
| --------------- | ---------------------- |
| Domain          | `networkwalks.com`     |
| Registrar       | GoDaddy.com, LLC       |
| Creation Date   | 06 November 2019       |
| Registry Expiry | 06 November 2027       |
| Name Server 1   | `ns6135.hostgator.com` |
| Name Server 2   | `ns6136.hostgator.com` |
| DNSSEC          | Unsigned               |

### Security Relevance

WHOIS information can provide useful intelligence about a domain's registration, DNS infrastructure and service providers.

---

## 5.2 WhatWeb

### Command

```bash
whatweb networkwalks.com
```

### Technologies Identified

The scan identified several technologies and components, including:

* **Apache**
* **WordPress 7.0.4**
* **WordPress Download Manager 3.3.58**
* **Bootstrap**
* **jQuery 3.7.1**
* **Google Tag Manager**
* **HTML5**
* **HTTPS**
* **Google-related services**

The website title was identified as:

```text
Networkwalks Academy
```

### Security Relevance

Technology fingerprinting helps identify the software stack used by a web application. This information can later be compared against security advisories and known vulnerabilities during an authorized security assessment.

> **Note:** Technology/version identification alone does not prove that a vulnerability exists.

---

## 5.3 nslookup

### Command

```bash
nslookup networkwalks.com
```

### Result

```text
Name:    networkwalks.com
Address: 192.232.216.135
```

### Finding

The domain resolved to:

```text
192.232.216.135
```

### Security Relevance

DNS resolution provides information about the infrastructure hosting a domain and can be useful during asset identification.

---

## 5.4 cURL

### Command

```bash
curl -I networkwalks.com
```

### Key Observations

The server returned:

```text
HTTP/1.1 301 Moved Permanently
```

and redirected the HTTP request to:

```text
https://networkwalks.com/
```

The response headers exposed information including:

* Apache
* WordPress
* WordPress security configuration
* Cache-related headers
* Security policy headers
* HTTP → HTTPS redirection
* Cookie information

### Security Relevance

HTTP response headers can provide useful information for technology fingerprinting and security configuration analysis.

---

## 5.5 WAFW00F

### Command

```bash
wafw00f networkwalks.com
```

### Result

```text
The site https://networkwalks.com is behind
ModSecurity (SpiderLabs) WAF.
```

### Finding

A **ModSecurity (SpiderLabs) Web Application Firewall** was detected.

### Security Relevance

A WAF provides an additional security layer between clients and the web application. Identifying the presence of a WAF helps a penetration tester understand the target's defensive architecture during an authorized assessment.

---

## 5.6 DNSRecon

### Command

```bash
dnsrecon -d networkwalks.com
```

### DNS Records Identified

| Record | Finding                    |
| ------ | -------------------------- |
| SOA    | `ns6135.hostgator.com`     |
| NS     | `ns6135.hostgator.com`     |
| NS     | `ns6136.hostgator.com`     |
| A      | `192.232.216.135`          |
| MX     | `mail.networkwalks.com`    |
| TXT    | Google site verification   |
| TXT    | SPF configuration          |
| SRV    | cPanel email autodiscovery |
| DNSSEC | Unsigned                   |

### SPF Observation

The DNS enumeration identified an SPF record containing:

```text
v=spf1 +a +mx +ip4:50.87.144.87 +include:websitewelcome.com ~all
```

### Security Relevance

DNS enumeration can reveal information about:

* Web infrastructure
* Email infrastructure
* Name servers
* Service discovery
* Domain verification
* Email security configuration

---

# 6. 🌐 Phase 2 — Network Scanning

The second activity focused on discovering active devices within my **own authorized local network**.

---

## 6.1 Zenmap / Nmap

### Network

```text
192.168.1.0/24
```

### Scan Type

A Ping Scan was performed using:

```bash
nmap -sn 192.168.1.0/24
```

### Objective

The scan was used to identify:

* Live hosts
* IP addresses
* MAC addresses
* Device vendors
* Network topology

### Hosts Identified

| IP Address      | Vendor / Observation |
| --------------- | -------------------- |
| `192.168.1.65`  | Apple                |
| `192.168.1.69`  | Unknown vendor       |
| `192.168.1.70`  | Intel Corporate      |
| `192.168.1.71`  | Not identified       |
| `192.168.1.254` | ZTE                  |

### MAC Address Privacy

MAC addresses identified during the scan were **masked in this public repository** to avoid unnecessarily exposing device identifiers.

Example:

```text
98:60:CA:XX:XX:XX
3E:BC:59:XX:XX:XX
B8:8A:60:XX:XX:XX
DC:51:93:XX:XX:XX
```

### Network Topology

Zenmap's topology functionality was used to visualize the discovered network environment and identify relationships between the scanning host and discovered devices.

---

## 6.2 Windows CMD

Windows command-line tools were used to identify local network information, including:

```text
Local IP Address
MAC Address
Network Configuration
```

This information was then used to understand the local subnet before performing network discovery with Zenmap.

---

# 7. 📊 Findings & Risk Analysis

| # | Finding                            | Evidence                                             | Potential Impact                       | Risk      |
| - | ---------------------------------- | ---------------------------------------------------- | -------------------------------------- | --------- |
| 1 | Web technology information exposed | WhatWeb identified WordPress and WP Download Manager | May assist technology fingerprinting   | 🟡 Medium |
| 2 | Server IP identifiable             | `nslookup` resolved the domain                       | Helps identify hosting infrastructure  | 🟢 Low    |
| 3 | HTTP technical information exposed | cURL returned server/security headers                | May assist further reconnaissance      | 🟢 Low    |
| 4 | WAF technology identifiable        | WAFW00F detected ModSecurity                         | Reveals defensive architecture         | 🟢 Low    |
| 5 | DNS infrastructure exposed         | DNSRecon identified DNS, mail and service records    | Helps build infrastructure profile     | 🟡 Medium |
| 6 | Multiple live hosts discovered     | Zenmap identified active hosts                       | Unknown devices should be investigated | 🟡 Medium |

### Risk Scale

* 🔴 **Critical**
* 🟠 **High**
* 🟡 **Medium**
* 🟢 **Low**
* 🔵 **Informational**

> **Important:** These findings represent reconnaissance observations and do not constitute confirmed vulnerabilities. No exploitation or vulnerability validation was performed during these exercises.

---

# 8. 🛡️ Recommendations

### 1. Review Publicly Exposed Technology Information

Regularly review information exposed by web applications and minimize unnecessary technology/version disclosure where appropriate.

### 2. Keep Web Technologies Updated

Ensure WordPress, plugins, themes, web servers and supporting components are regularly updated and monitored for security advisories.

### 3. Review HTTP Security Headers

Regularly review HTTP response headers and ensure security-related headers are appropriately configured.

### 4. Review DNS Records

Periodically audit DNS records and remove obsolete or unnecessary records and services.

### 5. Maintain and Monitor the WAF

Keep the Web Application Firewall properly configured, updated and monitored for suspicious activity.

### 6. Perform Regular Internal Network Discovery

Organizations should periodically identify devices connected to their internal networks.

### 7. Investigate Unknown Devices

Unknown or unauthorized devices discovered during network scans should be investigated.

### 8. Maintain Network Documentation

Network topology, IP addressing and device information should be properly documented and regularly updated.

### 9. Perform Authorized Security Assessments

Reconnaissance and scanning should always be conducted within a clearly defined and authorized scope.

---

# 9. 📝 Conclusion

Week 2 provided practical experience with the initial stages of penetration testing, particularly **reconnaissance, footprinting and network discovery**.

Using tools such as **WHOIS, WhatWeb, nslookup, cURL, WAFW00F and DNSRecon**, I was able to collect information about the Networkwalks domain, DNS infrastructure, web technologies, HTTP configuration and WAF protection.

Using **Zenmap/Nmap and Windows CMD**, I also gained practical experience in discovering live hosts and identifying devices within my authorized local network.

The exercises demonstrated how different reconnaissance tools complement each other and how publicly available information can be combined to build a technical profile of an environment.

Overall, this week strengthened my practical understanding of:

```text
Reconnaissance
      ↓
Footprinting
      ↓
DNS Enumeration
      ↓
Web Fingerprinting
      ↓
WAF Detection
      ↓
Network Discovery
      ↓
Risk Analysis
```

No exploitation was performed. The activities remained focused on **information gathering and authorized network discovery**.

---

# 10. 📸 Evidence

Evidence collected during the practical exercises includes:

<img width="672" height="655" alt="image" src="https://github.com/user-attachments/assets/b4db10f6-550f-4ca1-ae55-61b27e4d8282" />

<img width="672" height="348" alt="image" src="https://github.com/user-attachments/assets/8f16209a-83c3-4118-b7f6-44e310d447a5" />

<img width="672" height="291" alt="image" src="https://github.com/user-attachments/assets/73ca6162-d19c-485b-ac0a-6383d9d6c73b" />

<img width="672" height="293" alt="image" src="https://github.com/user-attachments/assets/2e80acc7-f93b-4c27-9536-f48e7308d99d" />

<img width="672" height="315" alt="image" src="https://github.com/user-attachments/assets/be69f641-4556-426a-bdca-e5bd00008dff" />

<img width="672" height="478" alt="image" src="https://github.com/user-attachments/assets/11764934-ceff-4290-beb1-038d4849b194" />

<img width="672" height="185" alt="image" src="https://github.com/user-attachments/assets/af94e2e5-3765-4438-a85a-b03cfd499d38" />

<img width="672" height="641" alt="image" src="https://github.com/user-attachments/assets/e3341492-1e23-41d3-89b1-9648d737705a" />


> Screenshots containing sensitive information such as private IP addresses, MAC addresses, credentials or internal network details should be sanitized before being published publicly.

---

# 11. 👤 Author

### David Fumeira Ndjimbo

**Cybersecurity Professional | B082 Networkwalks**

📍 Cybersecurity Internship — Week 02

### Focus Areas

`Cybersecurity` · `Network Security` · `Reconnaissance` · `OSINT` · `Penetration Testing` · `Network Scanning`

---

## 📚 Project Information

| Category     | Details                              |
| ------------ | ------------------------------------ |
| **Program**  | Cybersecurity Program — Networkwalks |
| **Week**     | 02                                   |
| **Modules**  | W2-PM1 · W2-PM5                      |
| **Focus**    | Footprinting & Network Scanning      |
| **Platform** | Kali Linux & Windows                 |
| **Status**   | Completed                            |

---

<p align="center">

**🔐 Learn • Practice • Secure**

*Cybersecurity Internship — Networkwalks*



---

**End of Report**
