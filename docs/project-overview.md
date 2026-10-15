# SecureSchool — School Cybersecurity Architecture

## Problem Statement
Kwara Academy faces unauthorized access, weak passwords, excessive privileges, and lack of monitoring. This project designs a practical Identity & Access Management system to address these threats.

## Objectives
- Implement secure identity and authentication
- Enforce Role-Based Access Control (RBAC)
- Apply Least Privilege and Separation of Duties
- Establish logging, monitoring, and incident response

## Core Security Principles
| Principle | Why It Matters |
| :--- | :--- |
| Least Privilege | Users only access resources required for their role |
| RBAC | Access is granted based on job function, not individual preference |
| Separation of Duties | No single user controls an entire sensitive workflow |
| Defense in Depth | Multiple layers protect against control failure |

## Technologies Used
- Linux Server (Kali/Ubuntu)
- PAM Authentication
- rsyslog Monitoring
- Bash Scripting for Account Lifecycle
- Markdown Documentation

## Limitations
- MFA is conceptual only (no hardware tokens)
- Network segmentation simulated via iptables (not physical VLANs)
- Application layer is CLI-based (no web frontend)
