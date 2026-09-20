# OT Security Assessment — Automated Industrial Painting Cell
## Field-Derived Security Engineering Case Study

> **Portfolio status:** Security engineering case study derived from legitimate
> operator-level troubleshooting, field observation, and diagnostic activities
> performed in an active industrial environment.
>
> This was **not** a commissioned penetration test, red-team engagement,
> certification audit, or authorized adversarial security exercise.
>
> All public content has been reconstructed and sanitized. Employer identifiers,
> credentials, production data, proprietary topology, internal logs, screenshots,
> source code, and confidential operational artifacts are not included or
> distributed.

---

## 1. Executive Summary

This project documents security-relevant findings identified while working
inside an automated industrial painting environment under normal
operator-level access constraints.

The objective of this portfolio artifact is not to claim formal compromise or
certification non-conformance. It demonstrates the ability to translate field
observations into:

**Operational Observation → Security Consequence → Risk Hypothesis  
→ ISA/IEC 62443 / NIST SP 800-82 Mapping → Deployable Mitigation**

The assessment identified **13 security findings** across five domains:

- endpoint and physical exposure;
- identity and access control;
- network architecture;
- process integrity and traceability;
- governance and maintenance practices.

The strongest recurring themes were:

1. excessive trust at operator and engineering endpoints;
2. weak separation between business and industrial trust zones;
3. limited accountability for credentials and configuration changes;
4. insufficient protection of security-relevant operational records;
5. cyber-physical risk created by undocumented or poorly governed process
   workarounds.

---

## 2. Scope & Environment

`Field-derived case study | Automotive OT environment`

The observed environment was a sequential, interdependent industrial painting
process containing multiple automated stations, including:

- surface preparation and cleaning;
- robotic base-coat application;
- thermal curing;
- robotic clear-coat application;
- industrial HMIs and engineering endpoints;
- PLC-controlled automation;
- computer-vision-assisted process functions;
- industrial communication infrastructure.

Specific vendor identifiers, CPU models, IP addressing, VLAN identifiers,
hostnames, production recipes, internal naming conventions, and proprietary
network diagrams are intentionally excluded.

---

## 3. Evidence & Confidence Model

To avoid overstating conclusions, findings in this document are separated by
evidence type.

### Direct Observation

A condition personally observable from normal field activity, such as:

- exposed physical interfaces;
- operator interface behavior;
- credential-sharing practices;
- visible endpoint configuration;
- paper-based operational records;
- process behavior during runtime.

### Engineering Inference

A technically plausible conclusion derived from observed behavior but not
validated through privileged configuration access.

Examples include:

- likely segmentation gaps;
- potential lateral movement paths;
- probable absence of centralized telemetry;
- possible endpoint hardening deficiencies.

### Lab Validation

A defensive concept reproduced in an isolated laboratory environment.

Lab results demonstrate technical feasibility only. They are **not** presented
as evidence that the same control was deployed in the production environment.

### Not Verified

Anything requiring privileged evidence that was unavailable under the
operator-level role, such as:

- firewall rulebases;
- switch configuration;
- Active Directory policy;
- disk-encryption state;
- complete routing tables;
- centralized logging configuration;
- vulnerability scanner results;
- endpoint protection policy.

This distinction is maintained throughout the project.

---

## 4. Methodology

Security analysis was derived from legitimate operational and diagnostic
visibility available during normal production work.

No privileged security testing was required for the observations documented
here.

### Available Visibility

- runtime behavior of industrial assets;
- operator-facing HMI behavior;
- physical observation of field equipment;
- normal production workflows;
- troubleshooting information available to operators;
- maintenance and communication practices;
- non-privileged process observations.

### Unavailable Visibility

- administrative credentials;
- complete network diagrams;
- routing tables;
- switch configuration;
- firewall policy;
- engineering-domain administration;
- centralized security tooling configuration;
- vulnerability-management platform access.

The resulting methodology is therefore **observation-driven and
constraint-aware**, rather than a formal penetration-testing methodology.

---

# 5. Security Findings

## Finding 01 — Exposed Peripheral Interfaces on Field HMIs

**Evidence basis:** Direct observation

Field HMI and control-panel interfaces were physically accessible within the
production environment.

### Security Relevance

Unrestricted removable-media or peripheral access can increase exposure to:

- unauthorized removable media;
- unintended file transfer;
- malicious or unapproved peripheral devices;
- configuration changes outside established maintenance workflows.

### Verification Limitation

Kernel-level device-control policy, BIOS restrictions, endpoint-protection
configuration, and centralized removable-media policy were not available for
verification.

### Framework Relevance

- ISA/IEC 62443-3-3: FR 2 — Use Control
- ISA/IEC 62443-3-3: FR 3 — System Integrity
- NIST SP 800-82 Rev. 3: endpoint hardening and removable-media controls

### Recommended Controls

- physical port protection where operationally feasible;
- approved removable-media process;
- endpoint device-control policy;
- malware scanning through controlled transfer stations;
- maintenance-window validation before production deployment.

---

## Finding 02 — Legacy / Lifecycle-Constrained Industrial Endpoints

**Evidence basis:** Direct observation + engineering inference

Some industrial endpoints exhibited characteristics consistent with legacy or
lifecycle-constrained systems.

### Security Relevance

Legacy OT assets can create risk when:

- operating-system support has ended;
- security patches cannot be applied without vendor validation;
- application compatibility prevents normal upgrade cycles;
- endpoint replacement would require production interruption.

### Verification Limitation

Patch level, vendor support contract, compensating controls, and complete
vulnerability exposure were not available for privileged verification.

### Framework Relevance

- ISA/IEC 62443-3-3: SR 3.2 — Malicious Code Protection
- ISA/IEC 62443-3-3: SR 7.6 — Network and Security Configuration Settings
- ISA/IEC 62443-3-3: SR 7.7 — Least Functionality
- NIST SP 800-82 Rev. 3: legacy-system risk management

### Recommended Controls

- asset inventory and lifecycle classification;
- compensating network controls;
- application allowlisting where supported;
- restricted management access;
- vendor-tested patch strategy;
- monitored replacement roadmap.

---

## Finding 03 — Insufficient HMI Application Confinement

**Evidence basis:** Direct observation

Operator interface behavior indicated that the industrial runtime environment
did not fully prevent access to underlying operating-system functions.

### Security Relevance

Weak application confinement can allow users to reach functions unnecessary
for normal process operation, increasing exposure to:

- accidental configuration changes;
- unauthorized file access;
- execution of non-production software;
- modification of local system settings.

### Framework Relevance

- ISA/IEC 62443-3-3: SR 2.1 — Authorization Enforcement
- ISA/IEC 62443-3-3: SR 7.7 — Least Functionality

### Recommended Controls

- hardened kiosk configuration;
- least-privilege operator accounts;
- removal of unnecessary shell access;
- application allowlisting;
- maintenance-only administrative elevation.

---

## Finding 04 — Operational Information Shared Through Uncontrolled Channels

**Evidence basis:** Direct observation

Operational and maintenance information was at times exchanged through
communication channels not designed as controlled OT engineering repositories.

### Security Relevance

Uncontrolled handling of technical information can increase the risk of:

- loss of data governance;
- uncontrolled replication;
- insufficient retention policy;
- weak access revocation;
- exposure of sensitive operational context.

### Framework Relevance

- ISA/IEC 62443-3-3: FR 4 — Data Confidentiality
- ISA/IEC 62443-3-3: SR 4.1 — Information Confidentiality
- NIST SP 800-82 Rev. 3: protection of OT information and remote collaboration

### Recommended Controls

- approved corporate communication channels;
- classification of OT technical information;
- restricted file-sharing policy;
- managed retention;
- controlled mobile-device access.

---

## Finding 05 — Insufficiently Evidenced IT/OT Trust-Zone Separation

**Evidence basis:** Engineering inference from field-visible communication paths

Field-visible connectivity and operational behavior suggested that trust
boundaries between enterprise-facing services and industrial assets required
formal verification.

### Security Relevance

If IT and OT trust zones are insufficiently separated, compromise of a
business-network endpoint can create paths toward industrial assets.

### Important Limitation

A complete flat network was **not** independently proven from operator-level
visibility. Firewall rules, routing policy, ACLs, VLAN configuration, and
industrial DMZ architecture were unavailable for inspection.

The correct conclusion is therefore:

> **Segmentation posture required formal architectural verification.**

### Framework Relevance

- ISA/IEC 62443-3-3: SR 5.1 — Network Segmentation
- ISA/IEC 62443-3-3: SR 5.2 — Zone Boundary Protection
- ISA/IEC 62443-3-2: Zones and Conduits
- NIST SP 800-82 Rev. 3: network segmentation and boundary protection

### Recommended Controls

- authoritative network-flow inventory;
- zone-and-conduit assessment;
- IDMZ validation;
- default-deny inter-zone policy;
- protocol-specific allowlisting;
- passive OT network monitoring.

---

## Finding 06 — Paper-Based Operational Records & Weak Digital Traceability

**Evidence basis:** Direct observation

Some operational parameters and checks depended on manual paper-based records.

### Security Relevance

Paper workflows are not inherently insecure, but at scale they can introduce:

- inconsistent timestamps;
- transcription errors;
- difficult historical correlation;
- weak identity attribution;
- physical record loss;
- reduced analytical visibility.

### Framework Relevance

- ISA/IEC 62443-3-3: SR 2.8 — Auditable Events
- ISA/IEC 62443-3-3: SR 2.11 — Timestamps
- ISA/IEC 62443-3-3: SR 2.12 — Non-Repudiation
- NIST SP 800-82 Rev. 3: logging, monitoring, and operational records

### Recommended Controls

- digitized industrial forms;
- authenticated user attribution;
- trusted timestamps;
- controlled local storage;
- audit-trail retention;
- offline-capable workflow for production continuity.

---

## Finding 07 — Maintenance-Induced Degradation of Optical Assets

**Evidence basis:** Direct observation + engineering analysis

A maintenance practice used on protective optical surfaces was associated with
progressive degradation of computer-vision performance.

### Security Relevance

This finding is primarily cyber-physical and reliability-oriented.

The security concern emerges when physical degradation causes:

- degraded sensor confidence;
- unstable feedback;
- operator workarounds;
- suppression of alarms;
- undocumented control changes;
- loss of process integrity.

### Framework Relevance

- ISA/IEC 62443-3-3: FR 3 — System Integrity
- NIST SP 800-82 Rev. 3: cyber-physical process integrity and operational
  resilience

### Recommended Controls

- manufacturer-compatible cleaning procedure;
- documented maintenance standard;
- condition-based inspection;
- change control for compensating logic;
- validation of sensor performance after maintenance.

> Detailed cyber-physical root-cause analysis is documented separately in
> `project-01.md`.

---

## Finding 08 — Loss of Diagnostic Fidelity in Maintenance Reporting

**Evidence basis:** Direct observation

Machine-generated fault information was sometimes translated into subjective
human descriptions before reaching higher technical or management layers.

### Security Relevance

Loss of raw diagnostic context can make it harder to distinguish:

- mechanical faults;
- communication failures;
- control-system faults;
- intermittent network problems;
- configuration problems;
- potentially security-relevant anomalies.

### Framework Relevance

- ISA/IEC 62443-3-3: FR 6 — Timely Response to Events
- ISA/IEC 62443-3-3: SR 6.1 — Audit Log Accessibility
- ISA/IEC 62443-3-3: SR 6.2 — Continuous Monitoring

### Recommended Controls

- preserve native fault codes;
- correlate alarms with timestamped events;
- structured RCA workflow;
- centralized maintenance-event repository;
- security monitoring integrated with operational context.

---

## Finding 09 — Zone & Conduit Architecture Required Formal Verification

**Evidence basis:** Direct physical observation + engineering inference

Field observations showed limited visibility into the formal security-zone and
conduit design.

### Security Relevance

Unclear trust boundaries make it difficult to establish:

- permitted communication paths;
- security responsibility boundaries;
- protocol allowlists;
- monitoring points;
- failure-containment boundaries.

### Important Limitation

Absence of visible segmentation from the production floor is not proof that no
logical segmentation exists.

The finding therefore concerns **architectural opacity and verification need**,
not a definitive claim of total segmentation failure.

### Framework Relevance

- ISA/IEC 62443-3-2: Zones and Conduits
- ISA/IEC 62443-3-3: SR 5.1 — Network Segmentation
- ISA/IEC 62443-3-3: SR 5.2 — Zone Boundary Protection

### Recommended Controls

- validated current-state architecture;
- documented security zones;
- defined conduits;
- industrial firewall enforcement;
- passive traffic baselining;
- change-controlled architecture documentation.

---

## Finding 10 — Undocumented Control-Logic Deviation Affecting Feedback Integrity

**Evidence basis:** Field behavior + diagnostic analysis

Observed process behavior was consistent with a control-logic path that
disabled or bypassed expected vision-system feedback under defined production
conditions.

### Security Relevance

The security issue is not simply that a bypass exists.

Industrial systems legitimately use bypasses during maintenance,
commissioning, and degraded operation.

The risk appears when bypass logic is:

- undocumented;
- insufficiently authorized;
- persistent beyond its intended window;
- not visible in normal operational monitoring;
- not reconciled against an approved program baseline.

### Potential Consequences

- degraded closed-loop integrity;
- reduced process visibility;
- hidden failure states;
- incorrect operational assumptions;
- difficult forensic reconstruction after an incident.

### Framework Relevance

- ISA/IEC 62443-3-3: FR 3 — System Integrity
- ISA/IEC 62443-3-3: SR 3.4 — Software and Information Integrity
- ISA/IEC 62443-3-3: SR 3.6 — Deterministic Output
- NIST SP 800-82 Rev. 3: configuration management and controller integrity

### Recommended Controls

- approved PLC baseline;
- version-controlled logic;
- change authorization;
- checksum / hash-based change detection where technically appropriate;
- alarm or event visibility for maintenance bypass states;
- periodic reconciliation of active logic against approved versions.

---

## Finding 11 — Engineering Workstation Physical & Session Exposure

**Evidence basis:** Direct observation + limited verification

Mobile or field engineering endpoints operated in areas with significant
personnel circulation.

### Security Relevance

Engineering workstations are high-value OT assets because they may contain:

- controller engineering software;
- configuration files;
- credentials or certificates;
- project backups;
- access paths to industrial systems.

Risk increases when physical access, session locking, user attribution, or
screen privacy are weak.

### Verification Limitation

Enterprise password policy and central endpoint controls were not available for
administrative verification.

### Framework Relevance

- ISA/IEC 62443-3-3: SR 1.1 — Human User Identification and Authentication
- ISA/IEC 62443-3-3: SR 1.5 — Authenticator Management
- ISA/IEC 62443-3-3: SR 2.5 — Session Lock

### Recommended Controls

- automatic session locking;
- individual user identities;
- least privilege;
- physical endpoint protection;
- privacy controls where appropriate;
- privileged access restricted to maintenance need.

---

## Finding 12 — Shared Credentials & Weak Accountability

**Evidence basis:** Direct observation

Authentication credentials were verbally shared during technical activity.

### Security Relevance

Shared credentials weaken:

- individual accountability;
- audit attribution;
- non-repudiation;
- incident investigation;
- access revocation.

The key issue is not the communication medium itself, but the loss of
identity-to-action traceability.

### Framework Relevance

- ISA/IEC 62443-3-3: SR 1.3 — Account Management
- ISA/IEC 62443-3-3: SR 1.5 — Authenticator Management
- ISA/IEC 62443-3-3: SR 2.12 — Non-Repudiation

### Recommended Controls

- unique user accounts;
- managed privileged identities;
- password vaulting where feasible;
- stronger authentication for engineering access;
- removal of shared engineering credentials;
- security awareness tailored to OT maintenance workflows.

---

## Finding 13 — Data-at-Rest Protection on Mobile Engineering Assets Required Verification

**Evidence basis:** Verification gap

Mobile engineering workstations can leave the protected industrial perimeter,
making data-at-rest protection important.

Under operator-level visibility, full-disk encryption status could not be
authoritatively verified.

### Security Relevance

If portable engineering assets are lost or stolen and storage is not
cryptographically protected, sensitive data may be exposed.

Potentially sensitive content can include:

- PLC project backups;
- configuration exports;
- network documentation;
- VPN configuration;
- engineering software data;
- operational documentation.

### Framework Relevance

- ISA/IEC 62443-3-3: SR 4.1 — Information Confidentiality
- ISA/IEC 62443-3-3: SR 4.2 — Information Persistence
- NIST SP 800-82 Rev. 3: protection of portable and engineering assets

### Recommended Controls

- enterprise-managed full-disk encryption;
- TPM-backed key protection where appropriate;
- secure recovery-key management;
- remote device-management capability;
- minimized local storage of OT-sensitive data.

---

# 6. Risk Prioritization

This portfolio uses **engineering priority**, not certification Security Level,
as the primary ranking mechanism.

ISA/IEC 62443 Security Levels are treated as design objectives derived from
risk assessment and threat assumptions — not as vulnerability severity scores.

| # | Finding | Evidence | Potential Impact | Priority |
|:--|:--|:--:|:--:|:--:|
| 10 | Undocumented PLC logic deviation | Observed / analyzed | Critical | **P1** |
| 05 | IT/OT segmentation requires verification | Inferred | Critical if confirmed | **P1** |
| 12 | Shared credentials / weak accountability | Observed | High | **P2** |
| 01 | Exposed HMI peripheral interfaces | Observed | High | **P2** |
| 02 | Legacy / lifecycle-constrained endpoints | Observed / inferred | High | **P2** |
| 03 | Weak HMI application confinement | Observed | High | **P2** |
| 09 | Zone/conduit architecture opacity | Observed / inferred | High | **P2** |
| 11 | Engineering workstation session exposure | Observed | High | **P2** |
| 13 | Mobile asset data-at-rest protection | Not verified | High if absent | **P3** |
| 04 | Uncontrolled technical information channels | Observed | Medium | **P3** |
| 08 | Reduced maintenance diagnostic fidelity | Observed | Medium | **P3** |
| 06 | Paper-based auditability limitations | Observed | Medium | **P4** |
| 07 | Optical maintenance degradation | Observed / analyzed | Operational / integrity | **P4** |

Priority reflects a combination of:

- potential safety or production consequence;
- process-integrity impact;
- exploitability or exposure;
- detection difficulty;
- recovery complexity;
- confidence in the available evidence.

---

# 7. Defense-in-Depth Remediation Architecture

## Pillar I — Identity, Endpoint & Engineering Workstation Hardening

**Addresses:** 01, 02, 03, 11, 12, 13

Recommended control families:

- unique operator and engineering identities;
- privileged-access separation;
- secure session locking;
- endpoint application confinement;
- device-control policy;
- full-disk encryption for portable assets;
- application allowlisting where vendor-supported;
- lifecycle and patch governance;
- controlled removable-media workflow.

All endpoint controls should be validated against:

- OEM support requirements;
- deterministic process behavior;
- maintenance procedures;
- production availability;
- recovery capability.

---

## Pillar II — Zones, Conduits & Industrial Boundary Protection

**Addresses:** 05, 09

Recommended architecture:

```text
Enterprise IT
     |
[Enterprise Security Boundary]
     |
    IDMZ
     |
[Industrial Security Boundary]
     |
OT Operations / SCADA
     |
Cell / Area Zones
     |
Controllers / HMIs / Robotics
```

Principles:

- no implicit trust between IT and OT;
- documented zones and conduits;
- default-deny inter-zone policy where operationally feasible;
- protocol-specific allowlisting;
- controlled engineering access;
- dedicated monitoring points;
- passive discovery preferred for fragile OT assets.

---

## Pillar III — Process Integrity, Logging & Change Governance

**Addresses:** 06, 08, 10

Recommended controls:

- preservation of native controller and alarm identifiers;
- timestamped event collection;
- authenticated digital records;
- PLC project version control;
- approved program baseline;
- monitored bypass states;
- formal change authorization;
- configuration backup and restoration procedures;
- integrity monitoring appropriate to vendor and process constraints.

---

## Pillar IV — Maintenance Engineering & Cyber-Physical Resilience

**Addresses:** 07

Recommended controls:

- manufacturer-compatible maintenance procedures;
- documented material compatibility;
- condition-based inspection;
- validation after maintenance;
- separation between physical root cause and logical workaround;
- engineering review before persistent control-logic bypasses are accepted.

---

# 8. Lab Validation — Defensive Proof of Concept

The production findings above were field-derived.

The following technical controls were validated separately in an isolated
Debian Linux laboratory environment.

These tests demonstrate **defensive engineering concepts only** and are not
presented as production deployment evidence.

## 8.1 Stateful Filtering for Industrial TCP Services

A lab firewall policy was used to validate a default-deny model with explicit
allowlisting for an authorized engineering source.

```nftables
table inet ot_security {
    chain input {
        type filter hook input priority 0; policy drop;

        iif lo accept
        ct state established,related accept

        # Example lab allowlist only.
        ip saddr 192.168.10.15 tcp dport 102 accept
    }
}
```

### Validation Objective

Demonstrate that:

- established traffic remains statefully tracked;
- unsolicited inbound traffic is denied by default;
- industrial service access can be restricted to explicitly authorized
  engineering sources.

### Production Caveat

A Linux nftables proof of concept is **not** a substitute for a validated
industrial firewall architecture.

Production controls must account for:

- vendor support;
- protocol inspection capability;
- redundancy;
- fail-safe / fail-open requirements;
- environmental rating;
- latency;
- maintenance access;
- process availability.

---

## 8.2 Passive Industrial Traffic Analysis

Wireshark, TShark, and Scapy were used in a controlled environment to inspect
industrial packet structures and validate protocol-level visibility.

Analysis focused on:

- endpoint identification;
- protocol recognition;
- service exposure;
- payload structure;
- command/function identification;
- communication baselining.

The purpose is to demonstrate passive OT traffic-analysis capability without
implying that confidential production PCAP data is distributed in this
repository.

---

# 9. Engineering Decision Model

Every proposed control is evaluated through the following sequence:

```text
Field Observation
      ↓
Evidence Classification
      ↓
Operational Consequence
      ↓
Security Consequence
      ↓
Risk Hypothesis
      ↓
62443 / NIST Mapping
      ↓
Control Design
      ↓
Production Impact Review
      ↓
Validation Plan
```

The control is considered viable only when it can reduce risk without creating
an unacceptable impact on:

- personnel safety;
- process safety;
- deterministic control;
- production availability;
- maintainability;
- recovery capability.

---

# 10. What This Project Demonstrates

This case study is intended to demonstrate practical capability in:

### OT Field Analysis

- industrial troubleshooting;
- operator-level diagnostics;
- cyber-physical reasoning;
- process-integrity analysis;
- constrained-environment investigation.

### OT Cybersecurity

- ISA/IEC 62443 interpretation;
- NIST SP 800-82 application;
- zones and conduits;
- endpoint hardening;
- identity and access control;
- industrial network segmentation;
- change governance;
- security monitoring concepts.

### Technical Security

- Wireshark / TShark;
- Python / Scapy;
- passive PCAP analysis;
- Linux networking;
- nftables;
- industrial protocol inspection.

### Governance

- evidence classification;
- risk prioritization;
- security-control mapping;
- operational constraints;
- remediation planning;
- distinction between observation, inference, and verification.

---

# 11. Disclosure & Confidentiality

This public case study is a reconstructed professional portfolio artifact.

It does **not** contain or distribute:

- employer-identifying information;
- credentials;
- internal screenshots;
- production packet captures;
- proprietary network topology;
- PLC source code;
- confidential recipes;
- production IP addressing;
- internal logs;
- restricted technical documents.

Where exact configuration evidence was unavailable, conclusions are explicitly
identified as engineering inference or verification gaps.

Framework references are used for educational and engineering mapping.
This document is **not** an ISA/IEC 62443 certification assessment and does not
claim formal organizational non-compliance.

---

## Related Project

For the detailed cyber-physical investigation involving computer vision,
process feedback, optical degradation, and PLC logic integrity:

→ [`project-01.md`](project-01.md)
