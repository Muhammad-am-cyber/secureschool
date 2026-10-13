# Integration Handoff Notes — Student 1 (Identity & Access Security Engineer)

## Overview
This document defines the IAM constraints and interfaces that Student 2 (Network) and Student 3 (Application) must integrate with. All network segmentation and application authorization logic MUST align with the RBAC model defined here.

---

## For Student 2: Network & Infrastructure Security Engineer

### User Groups ↔ VLAN Mapping
Your firewall rules and VLAN assignments must map directly to these OS-level groups:

| OS Group | Suggested VLAN | Network Policy Requirement |
|----------|----------------|----------------------------|
| `students` | VLAN 40 | Block access to Server VLAN (VLAN 50) except Port 80/443 |
| `teachers` | VLAN 20 | Allow access to App Server + Database (Port 3306) |
| `finance` | VLAN 30 | Allow access to App Server ONLY; block direct DB access |
| `admins` | VLAN 60 | Full management access; isolated from Guest VLAN |
| `guests` | VLAN 70 | Internet only; BLOCKED from ALL internal VLANs |

### Logging Integration
- Syslog is active at `/var/log/syslog`
- Authentication events include: LOGIN_SUCCESS, LOGIN_FAILURE, ACCESS_DENIED, ACCOUNT_LOCKED
- Forward these logs to your SIEM/monitoring dashboard
- Test: Run `sudo grep "ACCESS_DENIED" /var/log/syslog` to verify denied events are captured

### Hardening Baseline
- SSH root login disabled (`PermitRootLogin no` in `/etc/ssh/sshd_config`)
- Password hashing: SHA512/Yescrypt (verify via `/etc/login.defs`)
- Account lockout policy: Accounts locked via `usermod -L` remain locked until explicitly unlocked

---

## For Student 3: Application Security & Incident Response Engineer

### RBAC Role Mapping
Your application's role-checking logic MUST correspond to these OS groups:

| App Role | OS Group | Permission Scope |
|----------|----------|------------------|
| `student` | `students` | Read-only own records |
| `teacher` | `teachers` | Write grades (assigned classes only) |
| `finance_officer` | `finance` | Read/write payroll; read fees |
| `principal` | `admins` | Read-all reports; approve transactions |
| `it_admin` | `admins` | Manage users/systems; NO finance data access |

### Authentication Integration
- Use PAM or LDAP for backend authentication against OS accounts
- Session timeout: 30 minutes inactivity (enforce at app layer)
- Failed login threshold: Lock account after 5 consecutive failures → call `sudo usermod -L <username>`
- MFA: Conceptually required for `finance`, `principal`, `it_admin` roles

### Incident Response Triggers
If any of these events occur in `/var/log/syslog`, initiate IR procedure:
1. `ACCESS_DENIED` repeated >10 times in 1 minute → Potential brute force
2. `LOGIN_SUCCESS` from unexpected IP → Possible credential theft
3. `ACCOUNT_LOCKED` followed by `LOGIN_SUCCESS` → Account re-enabled without authorization
4. Finance role accessing non-finance resources → Insider threat indicator

### Shared Evidence Standards
- All test screenshots MUST include timestamp (`date` command before test)
- Log evidence must show BOTH success AND denial events
- NEVER commit passwords, keys, or credentials to GitHub
- Reference evidence files as: `evidence/screenshots/test-X-description.png`

---

## Change Management
Any changes to user groups, permissions, or authentication methods MUST be documented here and communicated to both Student 2 and Student 3 BEFORE implementation.

Last Updated: $(date '+%Y-%m-%d')
Author: Student 1 — Identity & Access Security Engineer
