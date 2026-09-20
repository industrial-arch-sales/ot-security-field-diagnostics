# Industrial OT Cybersecurity Portfolio

Field-derived cyber-physical security case studies built from hands-on work in active industrial environments, combined with OT security engineering, protocol analysis, and ISA/IEC 62443 / NIST SP 800-82 practices.

My background sits at the intersection of **industrial automation, field diagnostics, control systems, and cybersecurity**.

The objective of this portfolio is to demonstrate the ability to connect:

**Physical Process → PLC Logic → Industrial Network → Security Risk → Security Requirement → Deployable Mitigation**

---

## Portfolio at a Glance

| Case | Focus | Environment | Core Skills |
|---|---|---|---|
| [01 — Computer Vision Failure & PLC Logic Bypass](project-01.md) | Cyber-physical root-cause analysis | Automotive OT | PLC diagnostics, robotics, computer vision, integrity, ISA/IEC 62443 |
| [02 — OT Security Assessment: Automated Painting Cell](project-02.md) | Security assessment under limited-access constraints | Automotive OT | HMI, network segmentation, identity, governance, ISA/IEC 62443-3-3 |

---

## Scope, Ethics & Confidentiality

The field-derived cases in this repository originated from legitimate operational, maintenance, troubleshooting, and diagnostic activities performed within the access boundaries of my assigned role.

This portfolio **does not claim formal penetration-testing, red-team, certification-audit, or commissioned security-assessment authorization** unless explicitly stated in the individual project.

To protect confidentiality, all public material has been reconstructed and sanitized. This repository does **not** publish:

- employer-identifying information;
- real credentials or authentication material;
- proprietary network diagrams or production topology;
- internal logs or production datasets;
- source files or confidential configuration exports;
- information that would enable reproduction of a real production environment.

Technical scenarios are generalized where necessary while preserving the engineering and cybersecurity reasoning.

---

## Technical Stack

### Standards & Frameworks

- ISA/IEC 62443-3-2 — Security Risk Assessment for System Design
- ISA/IEC 62443-3-3 — System Security Requirements and Security Levels
- ISA/IEC 62443-4-1 — Secure Product Development Lifecycle
- ISA/IEC 62443-4-2 — Technical Security Requirements for IACS Components
- NIST SP 800-82 Rev. 3 — Guide to Operational Technology Security
- Purdue Enterprise Reference Architecture
- ONS RO-CB.BR.01

### Industrial Automation & Control

- Siemens SIMATIC S7-300 / S7-1500
- Beckhoff / TwinCAT
- Industrial HMI / SCADA
- 6DOF industrial robotics
- Computer vision systems
- IEDs and RTUs
- Industrial instrumentation and process control

### OT Networks & Security

- Industrial DMZ / IDMZ
- Network segmentation and Zones & Conduits
- Stateful firewalling
- Linux nftables
- IEEE 802.1Q VLANs
- Modbus TCP
- S7Comm
- IEC 60870-5-104
- OPC UA
- PROFINET

### Traffic Analysis & Engineering

- Wireshark
- TShark
- Scapy
- Python 3
- Bash
- Debian Linux
- PCAP analysis
- Industrial protocol inspection

---

# Case Studies

## 01 — Cyber-Physical Failure Analysis
### Computer Vision Degradation & PLC Logic Bypass

`Field-derived case study | Automotive OT environment`

A production computer-vision system used for trajectory correction of multi-axis industrial robots developed recurring accuracy problems during normal operation.

The investigation required correlating **physical degradation, measurement behavior, PLC logic, production symptoms, and control-system integrity**.

### Field Findings

Diagnostic activities identified degradation of optical viewports associated with abrasive maintenance practices. The resulting haze reduced measurement quality and contributed to systematic trajectory-correction errors.

Observed production measurements during the analyzed condition showed deviations in the range of approximately **4.5–8.5 mm**, with an observed inaccuracy rate of approximately **46.1%**.

Further diagnostic review identified an **undocumented PLC logic path** that allowed the affected process to continue operating without the expected closed-loop correction behavior under specific production conditions.

### Cyber-Physical Risk Chain

```text
Physical degradation
        ↓
Measurement degradation
        ↓
Incorrect process feedback
        ↓
Compensating / undocumented PLC logic
        ↓
Reduced telemetry and control integrity
        ↓
Operational and governance risk
```

### Security Significance

The primary cybersecurity concern was not the maintenance defect by itself. It was the loss of **control integrity, traceability, and visibility** introduced by undocumented compensating logic.

The case was analyzed from the perspective of:

- control-system integrity;
- PLC logic change management;
- telemetry reliability;
- traceability and accountability;
- compensating controls;
- ISA/IEC 62443 foundational requirements.

A key lesson from the case is that an OT security problem does not have to begin with malware or network intrusion. **Physical-process degradation can drive operational workarounds that later become cybersecurity and governance risks.**

### Proposed Engineering Direction

A low-impact optical restoration approach was evaluated as an alternative to full hardware replacement, with the objective of restoring measurement quality while minimizing production disruption.

The proposal was documented as an engineering and governance case study. It was **not implemented during the employment period**, so no realized savings or production-impact claims are made.

→ **[Full technical case study](project-01.md)**

---

## 02 — OT Security Assessment
### Automated Industrial Painting Cell

`Field-derived case study | Automotive OT environment`

This case study documents security-relevant findings identified while performing normal operator-level troubleshooting and diagnostic activities in an automated industrial painting environment.

The assessment was developed under **black-box-style visibility constraints**:

- no administrative privileges;
- no privileged credentials;
- no network diagrams;
- no security architecture documentation;
- no pre-existing OT security monitoring platform.

The purpose of the case study is to demonstrate how security risk can be identified and modeled from legitimate field observations and limited operational visibility.

### Assessment Summary

A total of **13 security findings** were documented across five domains.

#### Physical & Peripheral Exposure

Examples included:

- accessible peripheral interfaces on field HMIs;
- insufficient restriction of interfaces not required for normal operation;
- opportunities for stronger removable-media and physical-access controls.

#### Application & Endpoint Security

Observations included:

- insufficient restriction of operator workstation interfaces;
- opportunities for stronger kiosk-mode enforcement;
- endpoint-hardening gaps.

#### Network Architecture

Architectural observations included:

- insufficient segmentation between security zones;
- weak separation between enterprise and industrial environments;
- opportunities for stronger Zones & Conduits design;
- need for stronger industrial DMZ / boundary-control architecture.

#### Identity & Human Factors

Findings included:

- shared credentials;
- weak accountability boundaries;
- reduced non-repudiation;
- operational practices capable of unintentionally exposing authentication information.

#### Governance & Process Integrity

Observations included:

- undocumented control-logic behavior;
- reduced telemetry visibility under specific operating conditions;
- insufficient change traceability;
- manual records limiting auditability.

### ISA/IEC 62443 Mapping

Applicable findings were mapped to relevant **ISA/IEC 62443-3-3 System Requirements (SRs)**.

Target Security Level considerations were treated separately as **risk-driven design objectives**, based on system exposure, consequence, threat assumptions, and required risk reduction — not as vulnerability severity labels.

The assessment uses the following engineering flow:

```text
Observation
    ↓
Security consequence
    ↓
Applicable ISA/IEC 62443 requirement
    ↓
Operational constraint
    ↓
Recommended compensating or permanent control
```

### Example Reasoning Pattern

```text
Observation:
A field HMI exposes interfaces not required for normal operator activity.

Security consequence:
Increased exposure to unauthorized software execution, removable media,
or unintended configuration changes.

Operational constraint:
The workstation cannot be removed from production or rebooted during
active manufacturing.

Security approach:
Endpoint hardening, interface restriction, removable-media controls,
physical protection, and implementation during an approved maintenance window.

Framework:
Mapped to applicable ISA/IEC 62443 system requirements.
```

### Status

**Security engineering case study derived from field diagnostics.**

This project is not presented as a commissioned penetration test, red-team engagement, or formal certification assessment.

→ **[Full technical report](project-02.md)**

---

# Engineering Principles

Industrial cybersecurity controls must coexist with:

- personnel and process safety;
- production availability;
- process integrity;
- deterministic control requirements;
- legacy equipment;
- maintenance constraints;
- operational continuity.

For that reason, security controls cannot be evaluated only by asking:

> **Does this improve security?**

The more useful OT engineering question is:

> **Can this reduce risk without introducing an unacceptable safety, availability, or operational consequence?**

The preferred reasoning sequence used throughout this portfolio is:

```text
Understand the process
        ↓
Understand the control logic
        ↓
Understand the communication paths
        ↓
Model the security risk
        ↓
Map applicable requirements
        ↓
Design the control
        ↓
Validate operational impact
```

---

# What This Portfolio Demonstrates

### OT Operations

- active industrial production environments;
- industrial maintenance and troubleshooting;
- HMI / SCADA interaction;
- PLC-based automation;
- process diagnostics and root-cause analysis.

### Cyber-Physical Analysis

- physical-process failure analysis;
- control-logic integrity;
- telemetry integrity;
- undocumented operational workarounds;
- security implications of process degradation.

### OT Cybersecurity

- ISA/IEC 62443;
- NIST SP 800-82;
- risk assessment;
- Zones & Conduits;
- network segmentation;
- compensating controls;
- endpoint hardening;
- OT governance and traceability.

### Technical Security

- PCAP analysis;
- industrial protocol inspection;
- Python / Scapy;
- Wireshark / TShark;
- Linux networking;
- nftables.

---

# Professional Focus

My professional focus is **OT / ICS Cybersecurity Engineering**, combining hands-on industrial experience with automation, field diagnostics, industrial networking, and security engineering.

Core positioning:

**Electromechanics + Industrial Automation + Field Diagnostics + OT Networking + Cybersecurity Engineering**

Target areas:

**OT Cybersecurity Engineering | ICS Security | ISA/IEC 62443 | NIST SP 800-82 | Industrial Network Security | Cyber-Physical Risk**

---

## Contact

**LinkedIn**  
https://www.linkedin.com/in/eurique-sales

**GitHub**  
https://github.com/industrial-arch-sales
