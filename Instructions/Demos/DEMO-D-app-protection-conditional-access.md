# Demo D: App Protection and Conditional Access

**Module**: Module 4 - Protect data and control access  
**Duration**: 10-12 minutes  
**Difficulty**: Intermediate  
**Demo Type**: Instructor-led hands-on

## Learning Objectives

After this demonstration, learners will understand how to:
- Create app protection policies (MAM) to prevent data leakage
- Configure conditional access policies that enforce device compliance
- Understand the difference between MAM (Mobile Application Management) and MDM (Mobile Device Management)
- Test app protection and conditional access enforcement
- Monitor policy effectiveness and user experience

## Prerequisites

### Instructor Requirements
- Intune Administrator and Conditional Access Administrator roles
- Completion of Demos A-C (device enrolled, compliance policy configured)

### Environment Requirements
- Windows device enrolled in Intune with compliance policy assigned
- Mobile device (iOS or Android) for MAM demo (optional but recommended)
- Microsoft Outlook or Microsoft Teams app installed on mobile device
- Test user with Microsoft 365 E5 license

### Licenses Required
- Microsoft 365 E5 or E3 + EMS E5 (includes conditional access)

## Demo Scenario

**Context**: Contoso Healthcare wants to prevent corporate data leakage on employee devices. They need to protect Microsoft 365 data in mobile apps (even on personal devices) and ensure only compliant devices can access sensitive resources like SharePoint and Exchange.

**Narrative**: "Device management alone isn't enough - we need to protect corporate data even on unmanaged personal devices. We'll create app protection policies to prevent data leaks and conditional access policies to block noncompliant devices from accessing corporate resources."

## Step-by-Step Instructions

### Part 1: Create an app protection policy (4-5 minutes)

#### Step 1.1: Navigate to app protection policies

**Action**: Access MAM policies in Intune

1. Navigate to **https://intune.microsoft.com**
2. Go to **Apps** → **Manage apps** → **Protection**
3. Click **+ Create policy** → Select **iOS/iPadOS**

**Talking points**:
- "App protection policies work WITHOUT enrolling the device - perfect for BYOD scenarios"
- "These policies protect data in managed apps like Outlook, Teams, OneDrive"
- "Even on personal devices, we can prevent copy/paste of corporate data to personal apps"

#### Step 1.2: Configure policy basics and apps

**Action**: Name policy and select protected apps

1. **Basics** page:
   - Name: `iOS App Protection - Corporate Data`
   - Description: `Prevents data leakage from Microsoft 365 apps on iOS devices`
2. Click **Next**
3. **Apps** page:
   - Select **Public apps**
   - Add these apps:
     - Microsoft Outlook
     - Microsoft Teams
     - Microsoft OneDrive
     - Microsoft Word
     - Microsoft Excel
4. Click **Next**

**Talking points**:
- "We're protecting the core Microsoft 365 productivity apps"
- "Only these apps will have access to corporate data"
- "Data cannot be copied from these apps to unprotected apps"

![App selection page](media/microsoft-intune-admin-center-app-protection-policy-ios.png)

#### Step 1.3: Configure data protection settings

**Action**: Set data transfer restrictions

1. **Data protection** page, configure:
   - **Data Transfer**:
     - Send org data to other apps: **Policy managed apps**
     - Receive data from other apps: **Policy managed apps**
     - Save copies of org data: **Block**
     - Restric cut, copy and paste between apps: **Policy managed apps with paste in**
   - **Encryption**:
     - Encrypt org data: **Require**
   - **Functionality**:
     - Printing org data: **Block**
     - Screen capture and Genmoji: **Block**
2. Click **Next**

**Talking points**:
- "Policy managed apps means data can only move between protected Microsoft apps"
- "Users can't save corporate emails to personal cloud storage or photo gallery"
- "Encryption ensures data is protected at rest on the device"
- "Blocking screenshot prevents accidental or malicious data leakage"

![Data protection settings](media/microsoft-intune-admin-center-app-protection-policy-ios-access-reqs.png)

#### Step 1.4: Configure access requirements

**Action**: Set PIN and authentication requirements

1. **Access requirements** page:
   - PIN for access: **Require**
   - PIN type: **Numeric**
   - Simple PIN: **Block**
   - Minimum PIN length: **6**
   - Touch ID/Face ID instead of PIN: **Allow**
   - Override biometrics with PIN after timeout: **Require** (30 minutes)
   - Work or school account credentials for access: **Require**
   - Recheck access requirements after (minutes): **30**
2. Click **Next**

**Talking points**:
- "Users must enter a PIN to access corporate data in protected apps"
- "Biometric (fingerprint/face) can be used for convenience"
- "PIN times out after 30 minutes of inactivity for security"
- "Users must re-authenticate with work credentials periodically"



#### Step 1.5: Assign and create policy

**Action**: Target policy to users

1. **Assignments** page:
   - Include: **All users** (or select specific groups)
   - Exclude: None
2. Click **Next**
3. Review and click **Create**

**Talking points**:
- "App protection policies target USERS, not devices"
- "When users sign into protected apps on ANY device, policy applies"
- "Policies apply within 5-10 minutes of user signing into app"

![App protection policy assignments](media/microsoft-intune-admin-center-new-configuration-profile-assignments.png)

---

### Part 2: Create a conditional access policy (4-5 minutes)

#### Step 2.1: Navigate to conditional access

**Action**: Access conditional access in Entra admin center

1. Navigate to **https://entra.microsoft.com**
2. Go to **ID Protection** → **Risk-based Conditional Access** → **Policies**
3. Click **+ New policy**

**Talking points**:
- "Conditional access is the enforcement layer - it's the 'bouncer' that checks compliance"
- "CA policies answer: 'Should this user/device be allowed to access this resource?'"
- "Based on conditions (device compliance, location, risk), grant or block access"

![Conditional access policies list](media/microsoft-entra-admin-center-conditional-access.png)

#### Step 2.2: Configure policy basics and assignments

**Action**: Name policy and select users

1. **Name**: `Require compliant device for Exchange Online`
2. **Assignments**:
   - **Users**: 
     - Include: **All users** (or select pilot group)
     - Exclude: **Break glass admin account** (critical - always exclude emergency access account)
   - **Target resources**:
     - Choose: **Select resources** > **Select specific resources** > **Office 365 Exchange Online**
3. Leave other assignments at default

**Talking points**:
- "This policy requires devices to be compliant before accessing Exchange (email)"
- "ALWAYS exclude break glass/emergency access accounts to prevent lockout"
- "Targeting Exchange Online means: 'To read email, your device must be compliant'"

<!-- **TODO**: Screenshot of CA policy assignments -->

#### Step 2.3: Configure access controls

**Action**: Set compliance requirement

1. **Access controls** → **Grant**:
   - Select **Grant access**
   - Check: **Require device to be marked as compliant**
   - Check: **Require approved client app** (optional but recommended)
   - For multiple controls: **Require all the selected controls**
2. **Session**: Leave at defaults
3. **Enable policy**: **Report-only** (for testing, then change to **On** when ready)
4. Click **Create**

**Talking points**:
- "Device must be compliant (from our compliance policy in Demo C) to access email"
- "Approved client app ensures users use Outlook app, not browser or third-party apps"
- "Report-only mode lets us test without impacting users - review sign-ins before enforcing"
- "When confident, switch to On to start enforcement"

![CA policy grant controls](media/microsoft-entra-admin-center-conditional-access-policy-exchange-online.png)

---

### Part 3: Test policies (2-3 minutes)

#### Step 3.1: Test app protection policy (if mobile device available)

**Action**: Open protected app on mobile device

1. On iOS/Android device, open **Microsoft Outlook** app
2. Sign in with test user credentials if not already signed in
3. After sign-in, app should prompt for PIN setup
4. Set a 6-digit PIN
5. Verify:
   - Corporate email loads successfully
   - Try to take screenshot - should be blocked
   - Try to copy email text and paste into personal app (e.g., Notes) - should be blocked or show warning

**Talking points**:
- "PIN protection kicks in immediately after signing in"
- "Screenshot block prevents data leakage via screen capture"
- "Copy/paste restrictions prevent moving corporate data to personal apps"
- "End user experience: slight inconvenience for significant security gain"

<!-- **TODO**: Screenshot of PIN setup prompt in Outlook -->
<!-- **TODO**: Screenshot of blocked screenshot message -->

#### Step 3.2: Test conditional access (desktop)

**Action**: Show conditional access evaluation

1. On enrolled Windows device, open browser to **https://outlook.office.com**
2. Sign in with test user credentials
3. If device is compliant:
   - Access is granted, email loads
4. If device is noncompliant (or simulate by marking device noncompliant):
   - Access is blocked with message: "You can't get there from here"
   - Message explains: Device doesn't comply with security policies

**Talking points**:
- "Compliant devices get seamless access - users don't even notice CA policy"
- "Noncompliant devices are blocked with clear message explaining why"
- "Users are directed to contact IT or fix compliance issues"
- "This protects corporate resources from insecure devices"

<!-- **TODO**: Screenshot of successful access (compliant device) -->
<!-- **TODO**: Screenshot of blocked access with compliance message -->

#### Step 3.3: Review conditional access sign-in logs

**Action**: Validate policy enforcement

1. In Entra admin center, go to **Entra ID** → **Monitoring & health** → **Sign-in logs**
2. Find recent sign-in for test user
3. Click on the sign-in event
4. Review **Conditional Access** tab:
   - Policy name: Require compliant device for Exchange Online
   - Result: Success (if compliant) or Failure (if noncompliant)
   - Controls applied: Require compliant device (satisfied or not satisfied)

**Talking points**:
- "Sign-in logs show exactly which CA policies were evaluated and results"
- "Success means all controls were satisfied - user got access"
- "Failure shows which control failed - helps troubleshooting"
- "Use these logs to verify policies work before switching from Report-only to On"

<!-- **TODO**: Screenshot of sign-in log with CA evaluation results -->

---

## Demo Summary

**Recap key steps**:
1. ✅ Created app protection policy (MAM) to prevent data leakage on mobile apps
2. ✅ Configured data protection settings: restrict copy/paste, block screenshots, require encryption
3. ✅ Set access requirements: PIN, biometrics, periodic re-authentication
4. ✅ Created conditional access policy requiring device compliance for Exchange Online
5. ✅ Configured grant controls: compliant device + approved client app
6. ✅ Tested both policies and reviewed sign-in logs for validation

**Key takeaways**:
- "MAM protects data on ANY device, even unmanaged personal devices - perfect for BYOD"
- "Conditional access is the enforcement layer that blocks noncompliant devices"
- "Together: MAM protects app data, CA blocks resource access based on compliance"
- "Report-only mode in CA allows safe testing before full enforcement"
- "Sign-in logs provide visibility into policy evaluation and troubleshooting"

**Transition to next module**:
"We've now protected data and enforced compliance-based access. In Module 5, we'll go deeper into device hardening: deploying security baselines, onboarding to Defender for Endpoint, and enabling advanced threat protection."

---

## Common Issues and Troubleshooting

### Issue: App protection policy not applying to mobile app
**Cause**: User not signed in with work account, or policy propagation delay  
**Solution**: 
- Ensure user signs into app with work account (user@company.com)
- Wait 10-15 minutes for policy to propagate
- Sign out and back into app to force policy refresh

### Issue: Conditional access blocks all users including admins
**Cause**: Excluded emergency access account not configured correctly  
**Solution**: 
- ALWAYS test CA policies with Report-only first
- Exclude dedicated break glass admin accounts from all CA policies
- Have backup browser/incognito window with emergency admin signed in before testing

### Issue: Users report "You can't get there from here" but device shows compliant
**Cause**: Compliance evaluation delay, or device not synced recently  
**Solution**: 
- Force device sync in Intune: Device page → Sync
- Wait 15 minutes for compliance evaluation
- Check device last check-in time - must be recent
- Review sign-in logs to see exact reason for block

### Issue: Cannot copy/paste in protected apps even to other protected apps
**Cause**: Data protection setting too restrictive  
**Solution**: 
- Review app protection policy: Data Transfer → "Cut, copy and paste between apps"
- Change to "Policy managed apps with paste in" to allow copy/paste between protected apps
- Save policy and wait for propagation

---

## MAM vs. MDM Comparison

**Important concept to explain**:

| Aspect | MAM (App Protection) | MDM (Device Management) |
|--------|---------------------|----------------------|
| **Target** | Apps and app data | Entire device |
| **Enrollment** | Not required | Required |
| **Device ownership** | Personal (BYOD) friendly | Corporate devices |
| **Control scope** | Only managed apps | Full device settings |
| **Data protection** | App-level encryption, copy/paste restrictions | Device-level encryption, firewall, password |
| **User privacy** | High - only work apps controlled | Lower - IT sees device info |
| **Use case** | BYOD, personal devices | Corporate-owned, fully managed |

**Combined approach**: "Best practice: Use MAM for personal devices, MDM for corporate devices, and conditional access for both to enforce compliance."

---

## Additional Resources

- [App protection policies overview](https://learn.microsoft.com/mem/intune/apps/app-protection-policy)
- [Create app protection policies](https://learn.microsoft.com/mem/intune/apps/app-protection-policies)
- [What is Conditional Access?](https://learn.microsoft.com/entra/identity/conditional-access/overview)
- [Common Conditional Access policies](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-policy-common)
- [Troubleshoot Conditional Access](https://learn.microsoft.com/entra/identity/conditional-access/troubleshoot-conditional-access)

---

**Demo Status**: ✅ Ready for delivery  
**Last Updated**: November 11, 2025  
**Next Demo**: Demo E - Security Baseline and Defender Onboarding
