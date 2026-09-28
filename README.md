# Microsoft Defender Endpoint Security Lab

> Repository Status: Complete

This repository documents hands-on Microsoft Defender for Endpoint case studies completed in an authorized lab environment. The project covers endpoint security posture, vulnerability prioritization, controlled detection testing, alert investigation, containment decisions, and organization-wide security reporting.

## Case Studies

| Case study                                                                                                                                  | Status   |
| ------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| [Endpoint Security Posture and Vulnerability Prioritization](case-studies/01-endpoint-security-posture-and-vulnerability-prioritization.md) | Complete |
| [Defender Alert Investigation and Endpoint Containment](case-studies/02-defender-alert-investigation-and-containment.md)                    | Complete |

## Case Study Highlights

### Endpoint Security Posture and Vulnerability Prioritization

A Microsoft Defender for Endpoint assessment was conducted against the Windows 11 lab device `win11-lab`.

The assessment identified 58 active security recommendations and 94 vulnerability records. Further investigation focused on an LDAP client-signing configuration weakness and two Critical Microsoft Edge vulnerabilities.

The case study demonstrates how configuration risk, CVSS severity, exposure, exploitation indicators, affected software, and available remediation can be considered together when prioritizing endpoint-security work.

[Read the complete case study](case-studies/01-endpoint-security-posture-and-vulnerability-prioritization.md)

### Defender Alert Investigation and Endpoint Containment

A controlled PowerShell test was performed to validate Microsoft Defender Antivirus and Microsoft Defender for Endpoint reporting.

Defender blocked and removed the test behavior locally, created a centralized alert, and provided the associated PowerShell process tree for investigation. The device’s risk, exposure, and available response actions were reviewed before determining that isolation was not necessary for the known controlled activity.

The investigation also used the Unified security summary to compare the endpoint alert with the organization-wide security posture of the authorized lab tenant.

[Read the complete case study](case-studies/02-defender-alert-investigation-and-containment.md)

## Key Findings

* Defender identified an LDAP client-signing configuration weakness affecting the lab endpoint.
* Defender reported 94 vulnerability records associated with the device.
* Two reviewed Microsoft Edge vulnerabilities were rated Critical with CVSS scores of `9`.
* The installed Microsoft Edge version was below the version recommended by Defender.
* A controlled PowerShell test was blocked and removed by Microsoft Defender Antivirus.
* The local detection successfully generated a centralized Defender alert.
* The alert process tree connected the detection to the expected PowerShell activity.
* The device remained Low risk with Medium exposure after the controlled test.
* Device isolation and several other response actions were unavailable in the current session.
* The Unified security summary provided organization-wide posture and protection information for the lab tenant.

## Technologies and Concepts

* Microsoft Defender for Endpoint
* Microsoft Defender Vulnerability Management
* Microsoft Defender Antivirus
* Microsoft Defender portal
* Windows Security
* Windows 11
* Microsoft Edge
* Endpoint security recommendations
* Vulnerability assessment
* CVSS severity analysis
* Alert triage
* Process-tree investigation
* Endpoint risk and exposure
* Containment decision-making
* Secure Score
* Organization-wide security reporting

## Repository Structure

```text
microsoft-defender-endpoint-security-lab/
├── README.md
├── case-studies/
│   ├── 01-endpoint-security-posture-and-vulnerability-prioritization.md
│   └── 02-defender-alert-investigation-and-containment.md
└── evidence/
    ├── endpoint-security-posture/
    │   ├── README.md
    │   └── Supporting screenshots
    └── defender-alert-investigation/
        ├── README.md
        ├── Supporting screenshots
        └── Unified security summary report
```

## Scope and Ethics

* All activities were performed in an authorized lab environment.
* The Defender detection was intentionally generated as a controlled test.
* No production endpoints or user devices were affected.
* The reviewed configuration-remediation settings were not deployed.
* No device-isolation action was performed.
* Findings represent the endpoint and Defender data available when the evidence was collected.
* Security recommendations and response actions should be evaluated for operational impact before deployment.
