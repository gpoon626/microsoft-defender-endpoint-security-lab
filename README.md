# Microsoft Defender Endpoint Security Lab

> Repository Status: Active

This repository documents hands-on Microsoft Defender for Endpoint case studies completed in an authorized lab environment. The project focuses on endpoint security posture, configuration-risk assessment, vulnerability analysis, remediation prioritization, alert investigation, and endpoint response decisions.

## Case Studies

| Case study                                                                                                                                  | Status   |
| ------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| [Endpoint Security Posture and Vulnerability Prioritization](case-studies/01-endpoint-security-posture-and-vulnerability-prioritization.md) | Complete |

## Current Case Study

### Endpoint Security Posture and Vulnerability Prioritization

A Microsoft Defender for Endpoint assessment was conducted against the Windows 11 lab device `win11-lab`.

The assessment identified 58 active security recommendations and 94 vulnerability records. Further investigation focused on an LDAP client-signing configuration weakness and two Critical Microsoft Edge vulnerabilities.

The case study demonstrates how configuration risk, CVSS severity, exposure, exploitation indicators, affected software, and available remediation should be considered together when prioritizing endpoint-security work.

[Read the complete case study](case-studies/01-endpoint-security-posture-and-vulnerability-prioritization.md)

## Key Findings

* LDAP client signing was not required on the assessed endpoint.
* Defender identified one applicable device as exposed to the LDAP configuration weakness.
* Defender reported 94 vulnerability records associated with the device.
* Two reviewed Microsoft Edge vulnerabilities were rated Critical with CVSS scores of `9`.
* The installed Microsoft Edge version was below the version recommended by Defender.
* No public exploitation, verified exploitation, or available exploit kits were identified for the prioritized vulnerability at the time of review.
* The assessment produced remediation recommendations without deploying configuration changes.

## Planned Case Study

The next case study will examine Defender alert investigation and endpoint-containment decisions using controlled activity from the authorized lab environment.

It may include:

* Establishing a no-alert baseline
* Generating and reviewing a safe Defender test detection
* Investigating suspicious-process evidence
* Evaluating device-isolation options
* Reviewing organization-wide Defender security reporting

The case study will be published after its evidence and findings have been reviewed.

## Technologies and Concepts

* Microsoft Defender for Endpoint
* Microsoft Defender Vulnerability Management
* Microsoft Defender portal
* Windows 11
* Microsoft Edge
* Endpoint security recommendations
* Configuration-risk assessment
* CVSS severity analysis
* Vulnerability prioritization
* Exposure assessment
* Remediation planning

## Repository Structure

```text
microsoft-defender-endpoint-security-lab/
├── README.md
├── case-studies/
│   └── 01-endpoint-security-posture-and-vulnerability-prioritization.md
└── evidence/
    └── endpoint-security-posture/
        ├── README.md
        ├── 01-defender-device-security-posture.png
        ├── 02-active-security-recommendations.png
        ├── 03-ldap-client-signing-risk-details.png
        ├── 04-ldap-client-signing-remediation-options.png
        ├── 05-ldap-client-signing-exposed-device.png
        ├── 06-discovered-vulnerabilities-overview.png
        ├── 07-cve-2026-95329-vulnerability-details.png
        ├── 08-cve-2026-95322-vulnerability-details.png
        ├── 09-prioritized-cve-threat-insights.png
        └── 10-edge-update-security-recommendation.png
```

## Scope and Ethics

* All activities were performed in an authorized lab environment.
* No production endpoints or user devices were affected.
* The completed assessment did not deploy the reviewed remediation settings.
* Findings represent the endpoint and Defender data available when the evidence was collected.
* Security recommendations should be tested and evaluated for operational impact before deployment.
