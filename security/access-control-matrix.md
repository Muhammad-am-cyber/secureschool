# Access Control Policy & Matrix

## 1. Overview
This document defines the Role-Based Access Control (RBAC) model for Kwara Academy. 
It enforces the principles of Least Privilege (Section 11) and Separation of Duties (Section 12).

## 2. User Roles
| Role | Description | Authentication Strength |
|------|-------------|------------------------|
| Student | Enrolled learners | Standard Password |
| Teacher | Academic staff | Standard Password + MFA (Recommended) |
| Finance Officer | Financial staff | Strong Password + MFA (Mandatory) |
| Principal | School leadership | Strong Password + MFA (Mandatory) |
| IT Admin | System maintenance | Strong Password + MFA + IP Restriction |
| Guest | Visitors | Captive Portal / No Internal Access |

## 3. Access Control Matrix
| Resource / Action | Student | Teacher | Finance | Principal | IT Admin | Justification |
|---|---|---|---|---|---|---|
| View Own Grades | ✅ |  | ❌ | ✅ | ❌ | Need-to-Know: Students only see own data |
| Input Grades | ❌ | ✅ (Assigned) |  | ❌ | ❌ | Role-Specific: Only assigned teachers |
| View Payroll | ❌ | ❌ | ✅ | ✅ | ❌ | SoD: IT Admin manages systems, not salaries |
| Manage Users | ❌ | ❌ | ❌ | Limited | ✅ | Privileged Access: Only IT creates accounts |
| View Security Logs | ❌ | ❌ | ❌ | Limited | ✅ | Accountability: Admins monitor threats |
| Approve Transactions |  | ❌ | ❌ | ✅ | ❌ | SoD: Finance creates, Principal approves |

## 4. Implementation Evidence
- **Authorized Access:** Teacher001 successfully accessed `/srv/kwara_academy/grades` (See `evidence/test-a.png`)
- **Unauthorized Access:** Student001 denied access to `/srv/kwara_academy/payroll` (See `evidence/test-b.png`)
- **Account Lifecycle:** Locked account (teacher001) rejected despite valid credentials (See `evidence/test-c.png`)
- **Separation of Duties:** IT Admin blocked from Finance data (See `evidence/test-d.png`)

## 5. Security Principles Applied
1. **Least Privilege:** Users granted minimum permissions necessary for their role.
2. **Separation of Duties:** Critical workflows (e.g., payroll) require multiple roles.
3. **Defense in Depth:** Access controlled at OS level (groups/permissions) AND application level.
