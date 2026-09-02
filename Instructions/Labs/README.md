# MD-4011 Hands-On Labs

This folder contains 6 hands-on lab exercises for the MD-4011 course: **Deploy, manage, and secure endpoints with Microsoft Intune**.

## Lab Overview

These labs provide learners with practical, guided experience implementing modern endpoint management and security using Microsoft Intune, Microsoft Entra ID, Microsoft Defender for Endpoint, and Microsoft Security Copilot. Each lab corresponds to a module in the course and builds upon the previous lab, creating a comprehensive learning journey from initial tenant setup through AI-powered security operations.

| Lab | Title | Module | Duration | Focus |
|-----|-------|--------|----------|-------|
| **Lab 01** | Configure tenant for device management | Module 1 | 30 min | Licensing, Entra ID, enrollment, groups |
| **Lab 02** | Enroll and validate devices | Module 2 | 30 min | Device enrollment, portal validation |
| **Lab 03** | Implement policy layering and compliance | Module 3 | 45 min | Configuration profiles, compliance policies |
| **Lab 04** | Protect data with MAM and conditional access | Module 4 | 30 min | App protection policies, conditional access |
| **Lab 05** | Harden devices with security baselines | Module 5 | 45 min | Security baselines, Defender onboarding |
| **Total** | | | **3.5 hours** | Complete endpoint management lifecycle |

## Lab Scenario

Throughout these labs, you take on the role of **Diego Siciliani**, a Modern Endpoint Administrator for **Contoso Healthcare**, a mid-sized healthcare organization. Contoso is modernizing its endpoint management strategy to improve security, compliance, and user productivity while meeting healthcare industry regulations.

Your objectives:
- Deploy Microsoft Intune as the primary endpoint management solution
- Enroll Windows devices and configure automated enrollment
- Implement security policies and compliance requirements
- Protect corporate data on managed and unmanaged devices
- Harden endpoints against security threats
- Investigate and respond to security incidents using AI

## Prerequisites

### Required for All Labs

**Microsoft 365 Environment**:
- Microsoft 365 E5 trial or production tenant
- OR Microsoft 365 E3 + Enterprise Mobility + Security E5
- Global Administrator access (for Lab 01 initial setup)
- Intune Administrator or Endpoint Security Manager role

**Devices**:
- **Windows 11 device** (required for Labs 01-06)
  - Must NOT be currently enrolled in Intune
  - Local administrator access
  - Internet connectivity
- **iOS or Android device** (optional for Lab 04)
  - For testing mobile app protection policies

**Accounts**:
- Admin account with appropriate licenses
- 2-3 test user accounts with Intune/EMS licenses assigned

### Additional Requirements by Lab

**Lab 05**:
- Microsoft Defender for Endpoint Plan 2 license (included in M365 E5)

**Lab 06**:
- Microsoft Security Copilot license with SCUs provisioned (minimum 1 SCU)
- Security Copilot Contributor or Security Administrator role
- Security Copilot plugins enabled (Defender, Intune)

### Software Requirements

- Modern web browser (Microsoft Edge or Chrome)
- Windows 11 22H2 or later on test device
- Microsoft 365 Apps installed (optional but recommended)

## Lab Environment Setup

Before starting Lab 01, ensure you have:

1. ✅ **Microsoft 365 tenant** with appropriate licenses
2. ✅ **Test user accounts** created in Microsoft 365 admin center
3. ✅ **Windows 11 device** ready for enrollment (not currently managed)
4. ✅ **Admin credentials** for Global Administrator (Lab 01) and Intune Administrator (Labs 02-06)
5. ✅ **Internet connectivity** on all devices

### Important Notes

> [!IMPORTANT]
> **WWL Tenants - Terms of Use**  
> If you are being provided with a tenant as part of instructor-led training, the tenant is available for supporting hands-on labs only. Tenants should not be shared or used outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class ends and is not eligible for extension. Tenants must not be converted to a paid subscription. Tenants obtained as part of this course remain the property of Microsoft Corporation, and we reserve the right to obtain access and repossess at any time.

> [!WARNING]
> **Do not use production environments** for these labs unless specifically designed for training purposes. Some configurations (especially in Labs 05-06) implement security hardening that may impact device functionality.

> [!TIP]
> **Save your progress**: Take screenshots of key configurations and note down group names, policy names, and settings as you progress through the labs. You'll reference these in later labs.

### Switching between lab workstations

Some exercises use two hosted Windows workstations: **SEA-WS1** and **SEA-WS2**. When an instruction tells you to switch workstations, use your lab environment's resource selector, workstation tabs, or virtual-machine list to open the named workstation. The exact control varies by lab provider.

Before continuing after a switch, confirm the workstation name shown by the lab interface or Windows. Keep both workstation sessions running unless an exercise explicitly tells you to sign out or shut one down.

## Lab Delivery Modes

These labs support multiple delivery approaches:

### 1. Self-Paced Learning
- Learners complete labs independently at their own pace
- Ideal for online training, self-study, or Microsoft Learn integration
- Each lab includes detailed step-by-step instructions with screenshots

### 2. Instructor-Led Training
- Instructor demonstrates (using instructor demos), then learners practice
- Use labs after corresponding module delivery
- Instructor available for troubleshooting and questions

### 3. Guided Practice
- Instructor walks through lab steps with learners following along
- Pause at decision points for discussion
- Ideal for complex labs (Labs 05-06)

## Lab Files

| File | Description |
|------|-------------|
| `LAB_01_configure_tenant.md` | Lab 01: Configure tenant for device management |
| `LAB_02_enroll_validate_devices.md` | Lab 02: Enroll and validate devices |
| `LAB_03_policy_layering_compliance.md` | Lab 03: Implement policy layering and compliance |
| `LAB_04_data_protection.md` | Lab 04: Protect data with MAM and conditional access |
| `LAB_05_security_hardening.md` | Lab 05: Harden devices with security baselines |

## Common Troubleshooting

### Issue: Cannot sign in to portals
**Solution**: Verify credentials, check MFA requirements, ensure licenses are assigned

### Issue: Device enrollment fails
**Solution**: Check automatic MDM enrollment is enabled, verify user has license, ensure device meets requirements

### Issue: Policies don't apply
**Solution**: Wait 8 hours for policy sync, manually sync device, check group membership and policy assignment

### Issue: Compliance shows "Not evaluated"
**Solution**: Force device sync, wait 24 hours for initial compliance evaluation, check policy configuration

### Issue: Cannot access Security Copilot (Lab 06)
**Solution**: Verify SCUs are provisioned, check Security Copilot role assignment, enable plugins

## Additional Resources

- [Microsoft Intune documentation](https://learn.microsoft.com/mem/intune/)
- [Microsoft Entra ID documentation](https://learn.microsoft.com/entra/identity/)
- [Microsoft Defender for Endpoint documentation](https://learn.microsoft.com/defender-endpoint/)
- [Microsoft Security Copilot documentation](https://learn.microsoft.com/security-copilot/)
- [Microsoft Learn: Endpoint Administrator learning path](https://learn.microsoft.com/training/paths/endpoint-administrator/)

## Feedback

For feedback on these labs, please contact your instructor or submit feedback through your training platform.

---

**Course**: MD-4011 - Deploy, manage, and secure endpoints with Microsoft Intune  
**Version**: 1.0  
**Last Updated**: November 11, 2025
