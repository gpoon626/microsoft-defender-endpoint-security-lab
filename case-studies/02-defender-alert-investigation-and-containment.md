# Defender Alert Investigation and Endpoint Containment

> Status: Complete

## Scenario

The Microsoft Defender for Endpoint device overview initially showed no active alerts or incidents for the Windows 11 lab device `win11-lab`.

A controlled PowerShell test was then performed to validate whether Microsoft Defender Antivirus would block the activity locally and report it to the centralized Defender portal.

The resulting alert was investigated by reviewing the local protection history, centralized alert details, process tree, device risk, exposure level, available containment actions, and organization-wide Defender reporting.

## Objectives

* Establish the device’s alert baseline
* Generate a controlled Defender test detection
* Confirm that the activity was blocked locally
* Verify that the detection reached the Defender portal
* Review the alert severity, status, and affected asset
* Investigate the associated PowerShell process chain
* Evaluate whether endpoint isolation was necessary and available
* Review organization-wide security reporting

## Environment

* Authorized Microsoft 365 lab tenant
* Microsoft Defender for Endpoint
* Microsoft Defender Antivirus
* Windows Security
* Windows 11 virtual machine named `win11-lab`
* Windows 11 version 25H2
* Defender alert queue and process tree
* Defender Device Inventory
* Defender Unified security summary

## Activities and Findings

### 1. Alert Baseline Review

Before the controlled test, the Defender device overview reported no active alerts or incidents for `win11-lab`.

The endpoint was active, onboarded, and communicating with Microsoft Defender for Endpoint. This provided a baseline for comparing the device state after the test activity.

### 2. Controlled Detection Test

A controlled PowerShell behavior test was executed on `win11-lab`.

Windows Security detected:

```text
Behavior:Win32/BmTestOfflineUI
```

The local protection history showed:

* Local classification: Severe
* Status: Removed
* Affected process: `powershell.exe`
* Result: The threat or application was removed from the device

This confirmed that Microsoft Defender Antivirus detected and blocked the controlled activity locally.

### 3. Centralized Alert Validation

After the local block, Microsoft Defender for Endpoint created the alert:

```text
Suspicious 'BmTestOfflineUI' behavior was blocked
```

The alert showed:

* Centralized alert severity: Low
* Workflow status: New
* Detection status: Blocked
* Category: Suspicious activity
* Detection source: Antivirus
* Service source: Microsoft Defender for Endpoint
* Impacted asset: `win11-lab`

The local protection history and centralized alert used different severity labels. The local item was classified as Severe, while the Defender portal assigned the resulting alert a Low severity. These values represented different parts of the detection and alerting process and were documented separately.

### 4. Process Investigation

The alert process tree was reviewed to determine how the activity occurred.

The process evidence showed a PowerShell process launching another PowerShell process containing the controlled test command. Defender then detected and terminated the active `Behavior:Win32/BmTestOfflineUI` behavior.

The evidence associated with the PowerShell process showed:

* Remediation status: Blocked
* Verdict: Malicious
* Detection technology: Client heuristic

The command, process timing, and affected endpoint were consistent with the controlled test. The malicious verdict described the detected behavior and did not, by itself, establish that an uncontrolled compromise had occurred.

### 5. Scope and Containment Assessment

Defender provided general investigation guidance, including reviewing related devices, network addresses, files, machine activity, unfamiliar processes, and user activity.

The alert-specific containment section stated that no recommended actions were found.

The Device Inventory page showed:

* One onboarded device
* Risk level: Low
* Exposure level: Medium
* Sensor health state: Active
* Onboarding status: Onboarded

The device response menu was also reviewed. **Isolate Device** and several other response actions were unavailable in the current session.

The screenshot did not establish whether the unavailable actions resulted from permissions, licensing, or another product condition. No attempt was made to bypass the restriction.

The endpoint was not isolated because:

* The activity was intentionally generated in the authorized lab
* Defender blocked and removed the detected behavior
* The process activity matched the controlled test
* The device risk remained Low
* No evidence showed continuing uncontrolled activity

In a real investigation involving unknown or ongoing malicious behavior, unavailable isolation capability would require immediate escalation to an authorized responder with the necessary access.

### 6. Organization-Wide Security Reporting

The Defender Reports area was reviewed, and the Unified security summary was generated and exported.

Unlike the alert and device pages, this report provided an organization-wide view of the authorized lab tenant for the previous 30 days.

The posture summary showed:

* Secure Score: `47.42`
* Security posture improvement: `38.43%`
* SaaS security score: `16.87`
* SaaS security-score improvement: `0.05%`
* One onboarded device
* `100%` of the tenant’s device inventory protected

The complete eight-page report covered:

* Posture
* Protection
* Detection
* Investigation and response
* Optimizations

The report added tenant-level context, but the alert details and process tree remained the primary sources for investigating the specific endpoint activity.

## Assessment

| Area reviewed              | Finding                                         | Security significance                                                    |
| -------------------------- | ----------------------------------------------- | ------------------------------------------------------------------------ |
| Initial alert state        | No active alerts or incidents                   | Established the device baseline before testing                           |
| Local antivirus response   | Test behavior blocked and removed               | Confirmed endpoint protection responded locally                          |
| Centralized reporting      | Low-severity alert created                      | Confirmed the detection reached the Defender portal                      |
| Process evidence           | PowerShell activity matched the controlled test | Connected the alert to its known source                                  |
| Local and portal severity  | Severe locally; Low in the portal               | Demonstrated that local threat and centralized alert severity can differ |
| Device risk                | Low                                             | Did not indicate elevated device risk after the blocked test             |
| Device exposure            | Medium                                          | Showed that security exposure existed separately from alert risk         |
| Alert-specific remediation | No recommended actions found                    | Required analyst judgment instead of automated guidance                  |
| Device isolation           | Unavailable in the current session              | Would require escalation if containment were necessary                   |
| Unified security summary   | Organization-wide report generated              | Added tenant-level context to the endpoint investigation                 |

## Security Considerations

Alert severity should not be used as the only investigation criterion. Even a Low-severity alert should be reviewed to identify the affected device, process chain, detection source, remediation status, and surrounding context.

A malicious evidence verdict does not automatically prove that an endpoint was compromised. Analysts must determine whether the activity came from an authorized test, expected administrative action, or uncontrolled behavior.

Endpoint isolation is a disruptive containment action. The decision should consider whether malicious activity is ongoing, whether the endpoint presents continued risk, and whether isolation could interrupt essential services.

Organizations should also confirm that appropriate responders have access to containment actions before an actual incident occurs.

Organization-wide reports provide useful posture and trend information, but they do not replace detailed alert and process-level investigation.

## Outcome

The controlled PowerShell activity was successfully detected, blocked, removed, and reported to Microsoft Defender for Endpoint.

The centralized alert was traced back to the expected PowerShell process chain on `win11-lab`. The available evidence was consistent with the authorized test, and no evidence indicated continuing uncontrolled activity.

Device isolation was not performed. The action was unavailable in the current session, and the known test context, blocked result, and Low device-risk level did not justify further containment.

The investigation demonstrated the complete path from endpoint prevention to centralized alert triage, process analysis, containment evaluation, and organization-wide reporting.

## Limitations

* The investigation involved one authorized Windows 11 lab virtual machine.
* The activity was a controlled detection test rather than an actual compromise.
* Device-isolation functionality was unavailable in the current session.
* The screenshots did not establish why the response actions were unavailable.
* No live response session or investigation package was collected.
* The test did not validate Defender coverage against every attack technique.
* The Unified security summary represented the lab tenant’s organization-wide reporting scope for the selected 30-day period.
* No production systems or user devices were affected.

## Skills Demonstrated

* Microsoft Defender for Endpoint administration
* Endpoint alert triage
* Microsoft Defender Antivirus validation
* Process-tree analysis
* Detection and remediation verification
* Alert-context interpretation
* Endpoint risk and exposure assessment
* Containment decision-making
* Security-report interpretation
* Organization-wide posture review

## Evidence

| Evidence                                                                                                                               | What it demonstrates                                                                                      |
| -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| [No-alert device baseline](../evidence/endpoint-security-posture/01-defender-device-security-posture.png)                              | The device had no active alerts or incidents before the controlled test                                   |
| [Controlled Defender test and local block](../evidence/defender-alert-investigation/01-controlled-defender-test-and-local-block.png)   | Windows Security detected, blocked, and removed the controlled behavior                                   |
| [Defender alert queue](../evidence/defender-alert-investigation/02-defender-alert-queue-test-detection.png)                            | The local detection generated a centralized Low-severity alert                                            |
| [Alert process tree](../evidence/defender-alert-investigation/03-defender-alert-process-tree.png)                                      | The alert was connected to the expected PowerShell process chain                                          |
| [Investigation and containment guidance](../evidence/defender-alert-investigation/04-alert-investigation-and-containment-guidance.png) | Defender provided general investigation guidance but no alert-specific containment action                 |
| [Device risk and exposure status](../evidence/defender-alert-investigation/05-device-inventory-risk-and-exposure-status.png)           | The device remained Low risk with Medium exposure                                                         |
| [Unavailable device-isolation action](../evidence/defender-alert-investigation/06-device-isolation-action-unavailable.png)             | Isolation and other response actions were unavailable in the current session                              |
| [Unified security summary selection](../evidence/defender-alert-investigation/07-unified-security-summary-report-selection.png)        | The organization-wide report was accessed from Defender Reports                                           |
| [Organization-wide posture summary](../evidence/defender-alert-investigation/08-organization-wide-security-posture-summary.png)        | The report summarized tenant-level posture and onboarding coverage                                        |
| [Complete Unified security summary](../evidence/defender-alert-investigation/09-organization-wide-unified-security-summary.pdf)        | The exported report covered posture, protection, detection, investigation and response, and optimizations |

Additional descriptions are available in the [evidence documentation](../evidence/defender-alert-investigation/README.md).

