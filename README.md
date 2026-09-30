# ISSO / IAM Home Lab

A self-built lab environment for developing Information System Security Officer (ISSO) and Identity & Access Management (IAM) skills, documented using NIST SP 800-53 Rev 5 controls and DoD RMF practices.

## Purpose

Build and operate a small Windows/Linux enclave the way a DoD system is authorized and maintained: hardened to DISA STIGs, scanned, monitored, with identities managed under least privilege, and every configuration backed by documented evidence mapped to security controls.

## Environment

Windows 11 Pro host running Hyper-V, with four VMs on an isolated NAT network:

| VM | OS | Role |
|---|---|---|
| DC01 | Windows Server 2025 | Active Directory, DNS, PKI |
| WS01 | Windows 11 Enterprise | Domain workstation |
| LNX01 | Rocky Linux 9 | Linux server, SSO (Keycloak) |
| SEC01 | Ubuntu Server 24.04 | SIEM (Wazuh), vulnerability scanning (Nessus) |

## Roadmap

- [x] Phase 0: Host and network setup, media integrity verification
- [ ] Phase 1: Domain build
- [ ] Phase 2: IAM fundamentals (RBAC, admin separation, LAPS, account lifecycle)
- [ ] Phase 3: DISA STIG hardening and SCAP compliance scanning
- [ ] Phase 4: Vulnerability management and POA&M tracking
- [ ] Phase 5: Audit logging and monitoring
- [ ] Phase 6: PKI and SSO/MFA
- [ ] Phase 7: RMF authorization package (SSP, POA&M, SAR, risk assessment)

## Evidence

All evidence is indexed in [evidence-register.csv](/evidence-register.csv) and organized by control family. Each item includes a timestamped artifact and an evidence note documenting objective, method, results, and limitations.

**Example:** [SI-7-001](evidence/SI/SI-7-001_evidence-note_2026-09-30.md) covers SHA-256 integrity verification of all installation media against vendor and community-published checksums, with live source retrieval and documented limitations.
