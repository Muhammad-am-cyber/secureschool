# SecureSchool — Kwara Academy Cybersecurity Architecture

## Problem
Kwara Academy faces risks including unauthorized access, weak passwords, excessive privileges, and lack of monitoring. This project designs and implements a practical security lab to address these threats through Identity & Access Management (IAM), Network Segmentation, and Application Security.

## Objectives
- Implement RBAC with Least Privilege and Separation of Duties
- Demonstrate secure authentication and account lifecycle management
- Provide evidence-based security testing and logging
- Document architecture, threats, and incident response

## Architecture
![Architecture Diagram](architecture/network-diagram.png)
*(Insert your diagram here)*

## Technologies Used
- Linux (Kali/Ubuntu)
- Bash Scripting
- PAM Authentication
- Syslog Monitoring
- Git/GitHub

## Security Controls Implemented (Student 1 - IAM)
| Control | Implementation | Evidence |
|---------|---------------|----------|
| RBAC | Linux Groups + File Permissions | `security/access-control-matrix.md` |
| Least Privilege | Directory-level ACLs | `evidence/test-b-unauthorized-access.png` |
| Account Lifecycle | usermod -L/-U + passwd -S | `evidence/test-c-account-lockout.png` |
| Separation of Duties | IT Admin ≠ Finance Access | `evidence/test-d-sod-enforcement.png` |
| Logging | rsyslog + grep analysis | `evidence/logs/auth-events.log` |

## Testing Summary
- ✅ Authorized access verified (Teacher → Grades)
- ✅ Unauthorized access blocked (Student → Payroll)
- ✅ Locked accounts rejected despite valid credentials
- ✅ Privileged separation enforced (IT Admin → Finance)
- ✅ Authentication events logged and traceable

## Team
- **Student 1:** Identity & Access Security Engineer *(You)*
- **Student 2:** Network & Infrastructure Security Engineer
- **Student 3:** Application Security & Incident Response Engineer

## Limitations & Future Work
- MFA implemented conceptually; production deployment requires TOTP integration
- Application layer is simulated via OS permissions; future work includes web app with session management
- Network segmentation is logical; physical VLAN implementation pending Student 2's infrastructure build
