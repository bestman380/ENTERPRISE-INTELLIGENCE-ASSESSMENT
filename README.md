# Enterprise Intelligence Assessment — NIITPH

Open-Source Exposure and Security Intelligence report on the **National Institute of Information Technology, Port Harcourt (NIITPH)**, produced as an academic OSINT/network-reconnaissance exercise.

| | |
|---|---|
| **Prepared by** | Iboroma Bestman Lawson |
| **Date** | 10 July 2026 |
| **Classification** | Confidential — For Academic and Internal Review Use Only |
| **Primary subject** | National Institute of Information Technology, Port Harcourt (NIITPH) |

> ⚠️ **This repository is private.** It contains unredacted personal and infrastructure data (staff names, emails, phone numbers, IP addresses, domain records) collected during the assessment. Do not make this repository public or share its contents outside the intended academic/internal review audience.

---

## Contents

```
.
├── README.md
├── report/
│   └── Enterprise_Intelligence_Assessment_NIITPH_2.docx   # full source report
└── images/                                                # evidence screenshots, by finding
    ├── Fig_A1_google-dork_wigwe-university-website.png
    ├── Fig_A2_wigwe-university_current-site_no-profile.png
    ├── Fig_A3_wayback-machine_archived-lecturer-profile.png
    ├── Fig_B1_domain-enumeration_dork-results.png
    ├── Fig_B2_email-discovery_dork-results.png
    ├── Fig_B3_linkedin_employee-profiling_dork-results.png
    ├── Fig_B4a_niitph_indexed-pages.png
    ├── Fig_B4b_niitph_indexed-pages.png
    ├── Fig_C1_staff-identity_centre-head.png
    ├── Fig_C2_staff-identity_chief-counsellor.png
    ├── Fig_C3_support-email_instagram-listing.png
    ├── Fig_D1_osint-framework_ip-lookup.png
    ├── Fig_D2_whois_bgp-he-net_data.png
    ├── Fig_E1_maltego_transform-graph.png
    ├── Fig_E2_maltego_transform-graph.png
    ├── Fig_E3_maltego_transform-graph.png
    ├── Fig_F1_staff-info_public-platforms.png
    └── Fig_G1_nmap_scan-output.png
```

Image filenames map directly to the figure references used throughout the report (e.g. *Fig. A1*, *Fig. B4*, *Fig. G1*), grouped by finding letter (A–G) as defined in Section 7.

---

## 1. Introduction

This assessment applies Open-Source Intelligence (OSINT) and network reconnaissance techniques to evaluate the organizational exposure of NIITPH. The objective is to identify publicly available information, analyze infrastructure visibility, and determine potential risks from an attacker's perspective.

The assessment scenario involves NIITPH experiencing suspicious login attempts and increased visibility, indicating possible reconnaissance activity by threat actors.

A smaller, separate OSINT case study is also included, examining the public exposure of a named lecturer through a different institution's website (Wigwe University). This case study illustrates OSINT technique and information persistence independently — no relationship between this individual case and NIITPH was stated or is assumed.

## 2. Overview

Using passive techniques — search-engine dorking, WHOIS lookup, Wayback Machine review, and public social-platform review (LinkedIn, Instagram) — together with limited active reconnaissance (an OSINT Framework IP lookup and an Nmap host/port scan), the assessment surfaced:

- Publicly exposed staff identities and contact details
- An unauthenticated login portal
- Domain and DNS configuration details
- A set of network services reachable on NIITPH's hosting IP address

## 3. Objectives

- Identify publicly available information
- Assess employees' and organizational exposure
- Discover digital assets and footprints
- Investigate publicly available infrastructure
- Correlate intelligence findings into meaningful conclusions
- Assess security risks based on collected intelligence
- Produce a professional intelligence report

## 4. Scope

- Two named web targets: the Wigwe University public website (individual case study) and the NIITPH public web presence (niitph.com, with a related reference to niit.com)
- Passive, unauthenticated OSINT collection: search-engine dorking, WHOIS/registration lookup, Wayback Machine archive review, public social-platform review (LinkedIn, Instagram)
- One instance of light active reconnaissance: an Nmap host-discovery and port scan of NIITPH's resolved IP address, **176.123.0.55**
- Entity and relationship mapping of the niitph.com domain using Maltego

No credential testing, exploitation, social engineering, or intrusive scanning beyond the single Nmap scan was performed.

## 5. Tools Used

| Tool | Purpose |
|---|---|
| Google Dorking | Advanced search |
| Whois | Domain information |
| TheHarvester | Email and subdomain discovery |
| Wayback Machine | Historical website analysis |
| Maltego | Relationship mapping |
| Httrack | Offline website analysis |
| Shodan | Internet-facing asset discovery |
| OSINT Framework | Domain / infrastructure reconnaissance |
| Gantt Project | Planning |

## 6. Methodology

Followed the intelligence cycle: **Planning → Collection → Processing → Analysis → Dissemination**.

## 7. Findings summary

Findings are grouped A–G; risk levels map to MITRE ATT&CK® Reconnaissance (TA0043) techniques (T1589, T1590, T1593, T1594, T1595, T1596). Full detail and evidence screenshots are in the report and `images/` folder.

| Group | Finding |
|---|---|
| **A** | Individual OSINT case study — a lecturer's profile, removed from the live Wigwe University site, still recoverable via a Wayback Machine snapshot (6 Aug 2025) |
| **B** | NIITPH passive reconnaissance — domain enumeration, email discovery, and LinkedIn employee-profiling dorks; indexed pages/entry points found via `site:niitph.com` |
| **C** | NIITPH information leakage — named senior staff (Centre Head, Chief Counsellor) with direct emails, three organizational phone numbers, a public support email, and an unauthenticated login portal at `niitph.com/encore/auth` |
| **D** | NIITPH infrastructure intelligence — resolved IP `185.53.179.146` via OSINT Framework; WHOIS shows domain created May 2025, DNSSEC unsigned, and shared hosting confirmed via bgp.he.net |
| **E** | Relationship mapping via Maltego — transforms surfaced related subdomains (mail, webdisk, whm, cpanel, cpcontacts) |
| **F** | Human attack surface — staff information corroborated across public platforms (LinkedIn + official site) |
| **G** | Infrastructure accessibility — Nmap host-discovery and full port scan against `185.53.179.146` |

## 8. Intelligence Correlation

- **Staff identity corroboration** — named senior staff surface independently via the About Us page and LinkedIn, raising confidence the identities/roles are accurate and actively maintained.
- **Single infrastructure profiled three ways** — the IP `176.123.0.55` was independently reached via OSINT Framework, WHOIS, and Nmap, giving high confidence it is NIITPH's actual production hosting address.
- **Domain age and hardening posture** — niitph.com registered May 2025, DNSSEC unsigned: a recently established web presence without baseline DNS hardening.
- **Shared hosting and service exposure** — bgp.he.net shows co-hosting with multiple domains; Maltego surfaced related subdomains (mail, webdisk, whm, cpanel, cpcontacts), consistent with the open ports found by Nmap.
- **Login portal plus staff identity** — the unauthenticated login portal exists alongside directly attributable staff emails/phone numbers, giving an attacker both a reachable auth endpoint and named targets.
- **Archive persistence pattern** — the Wigwe University case study is not linked to NIITPH by any evidence collected; it illustrates that removed content can persist in the Wayback Machine (NIITPH's own historical pages were not separately checked).

## 9. Intelligence Assessment

Assessed with **moderate-to-high confidence** that NIITPH maintains a publicly indexed, recently registered (circa May 2025) web presence hosted in a shared environment, with several named staff and direct contact channels exposed across at least two independent public sources, and an unauthenticated login portal reachable from the open internet alongside a broader-than-typical set of open network services.

This exposure pattern is consistent with information typically gathered during the reconnaissance phase preceding social-engineering or credential-based attacks. No evidence indicates any identified service has already been exploited; this assessment describes external exposure only.

## 10. Risk Analysis

| Level | Risk |
|---|---|
| **High** | Unauthenticated login portal combined with harvested staff emails — enables credential-harvesting/phishing against a real, reachable endpoint |
| **High** | Employee email and phone exposure across multiple public sources — enables targeted spear-phishing, vishing, or impersonation |
| **Medium** | Multiple network services reachable on the hosting IP — widens attack surface |
| **Medium** | DNSSEC unsigned on niitph.com — no protection against DNS spoofing/cache-poisoning |
| **Medium** | Shared IP hosting with multiple co-tenant domains — compromise of the platform/co-tenant could indirectly affect NIITPH |
| **Low / Informational** | Recently registered domain (May 2025) — limits historical monitoring/reputation data |
| **Informational** | Archive persistence of removed content — demonstrates content removed from a live site can remain publicly visible elsewhere |

## 11. Recommendations

- Place the login portal (`niitph.com/encore/auth`) behind stronger access controls — MFA, IP allow-listing/VPN, login rate-limiting/lockout
- Reduce direct public exposure of individual staff emails; use role-based/generic addresses (e.g. `info@`, `admissions@`) with internal routing, and provide phishing/vishing awareness training
- Review every exposed network service on the hosting IP; disable/restrict what doesn't need to be internet-facing; firewall/allow-list the rest
- Enable DNSSEC on the niitph.com domain
- Confirm the hosting provider's tenant-isolation and patching practices given shared-IP hosting
- Periodically audit organizational exposure via search-engine dorking, WHOIS, and Wayback Machine; submit removal/opt-out requests for sensitive historical content where appropriate
- Establish a recurring internal OSINT self-assessment using the same tool set to track exposure over time

## 12. Reference

- Google Search and Bing Search (search-engine dorking)
- LinkedIn (linkedin.com)
- Instagram
- Wayback Machine (web.archive.org)
- WHOIS / CentralOps.net domain and network lookup
- BGP.he.net (Hurricane Electric BGP Toolkit)
- OSINT Framework (osintframework.com)
- Maltego (Community/Desktop Edition)
- Nmap, run from Kali Linux

---

*This README summarizes `report/Enterprise_Intelligence_Assessment_NIITPH_2.docx`, which remains the authoritative source document.*
