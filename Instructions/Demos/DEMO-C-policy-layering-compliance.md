# Demo C: Policy Layering and Compliance

**Module**: Module 3 - Configure and secure devices with policy  
**Duration**: 12-15 minutes  
**Difficulty**: Intermediate  
**Demo Type**: Instructor-led hands-on

## Learning Objectives

After this demonstration, learners will understand how to:
- Create and assign configuration profiles for device settings
- Create and assign compliance policies to define security requirements
- Use dynamic groups for automated policy targeting
- Use filters for conditional policy assignment
- Understand policy precedence and conflict resolution
- Validate policy application on enrolled devices

## Prerequisites

### Instructor Requirements
- Intune Administrator or Global Administrator role
- Completion of Demo B (device enrolled in Intune)

### Environment Requirements
- At least one Windows device enrolled in Intune (from Demo B)
- Dynamic group "All Windows Devices" created (from Demo A)
- Test user with Intune license

### Licenses Required
- Microsoft 365 E5, E3 + EMS E5, or Intune licenses

## Demo Scenario

**Context**: Contoso Healthcare needs to apply security settings to Alex's Windows device. They want to enforce BitLocker encryption, configure Windows Update policies, and ensure devices meet minimum security requirements before accessing corporate resources.

**Narrative**: "We have Alex's device enrolled, but it doesn't have any security settings applied yet. Let's create configuration profiles to enforce settings and compliance policies to verify the device meets our standards. We'll use dynamic groups and filters to ensure these policies apply automatically to the right devices."

## Step-by-Step Instructions

### Part 1: Create a configuration profile (4-5 minutes)

#### Step 1.1: Navigate to configuration profiles

**Action**: Access Intune configuration policies

1. Open browser and navigate to **https://intune.microsoft.com**
2. Navigate to **Devices** → **Manage devices** → **Configuration**
3. Select **+ Create** → **+ New policy**
4. In the Create a profile blade:
   - **Platform**: Windows 10 and later
   - **Profile type**: Settings catalog
5. Click **Create**

**Talking points**:
- "Configuration profiles let us apply settings to devices - Wi-Fi, VPN, security, restrictions, etc."
- "Settings catalog is the modern approach - it contains all available Windows settings in one place"
- "Templates (older approach) provide predefined setting groups, but Settings catalog offers more control"

**What to show**:
- Configuration profiles list (empty or with existing policies)
- Profile type options: Settings catalog vs. Templates

![Create policy with platform and profile type selection](media/microsoft-intune-admin-center-new-configuration-profile.png)

---

#### Step 1.2: Configure basic profile information

**Action**: Name and describe the profile

1. On the **Basics** page:
   - **Name**: `Windows Security Settings - Corporate Devices`
   - **Description**: `Enforces BitLocker encryption, firewall, and security settings for corporate Windows devices`
2. Click **Next**

**Talking points**:
- "Use descriptive names - in production, you'll have many policies"
- "Include the platform and purpose in the name for easy identification"
- "Description helps document the policy's intent for other admins"

**What to show**:
- Basics page with name and description fields

![Configuration profile basics page](media/microsoft-intune-admin-center-new-configuration-profile-basic-details.png)

---

#### Step 1.3: Add settings to the profile

**Action**: Configure BitLocker encryption settings

1. On the **Configuration settings** page, click **+ Add settings**
2. In the Settings picker, search for "**BitLocker**"
3. Expand **BitLocker** category
4. Check the following settings:
   - **Require Device Encryption** → Set to **Enabled**
   - **Removable Drives Exluded From Encryption** → Set to **Enabled**
5. Close the settings picker.
6. Review configured settings in the profile, set **Require Device Encryption** to **Enabled**
7. Click **Next**

**Talking points**:
- "BitLocker encrypts the device's hard drive - critical for lost/stolen devices"
- "Require Device Encryption ensures all corporate Windows devices are encrypted"
- "We're setting a minimum PIN length of 6 characters for added security"
- "Recovery keys are stored in Entra ID so IT can help users who forget their PIN"
- "In production, you'd add more settings: firewall rules, Windows Defender, password policies, etc."

**What to show**:
- Settings picker with BitLocker options
- Configured BitLocker settings in profile

![Settings picker with BitLocker options](media/microsoft-intune-admin-center-create-baseline-profile-settings.png)

---

#### Step 1.4: Assign the profile to a group

**Action**: Target the profile to Windows devices

1. On the **Assignments** page, under **Included groups**, click **Add groups**
2. Search for and select **All Windows Devices** (dynamic group from Demo A)
3. Click **Select**
4. Leave **Excluded groups** empty (or demonstrate exclusion if desired)
5. Click **Next**

**Talking points**:
- "We're assigning to the dynamic group that auto-populates with all Windows devices"
- "As new Windows devices enroll, they'll automatically receive this policy"
- "You can exclude specific groups if needed - useful for pilots or exceptions"
- "In enterprise scenarios, you might have different policies for different departments"

**What to show**:
- Group selection interface
- Selected group appearing in included groups
- Exclusion option

![Assignments page with group selected](media/microsoft-intune-admin-center-new-configuration-profile-assignments.png)

#### Step 1.5: Review and create

**Action**: Finalize the configuration profile

1. On the **Review + create** page, review all settings
2. Verify:
   - Profile name is correct
   - BitLocker settings are configured
   - Assigned to All Windows Devices group
3. Click **Create**
4. Wait for "Successfully created the profile" confirmation

**Talking points**:
- "Always review before creating - mistakes can impact many devices"
- "Once created, the policy will deploy to devices within 8 hours (or on next sync)"
- "Policy deployment is asynchronous - doesn't happen instantly"

**What to show**:
- Review page with all configuration details
- Success confirmation message

![Review + create page](media/microsoft-intune-admin-center-new-configuration-profile-final.png)

---

### Part 2: Create a compliance policy (4-5 minutes)

#### Step 2.1: Navigate to compliance policies

**Action**: Access Intune compliance policies

1. In Intune admin center, navigate to **Devices** → **Compliance**
2. Select **+ Create policy**
3. In the Create a policy blade:
   - **Platform**: Windows 10 and later
   - **Profile type**: Windows 10/11 compliance policy
4. Click **Create**

**Talking points**:
- "Compliance policies define security requirements - devices must meet these to be considered compliant"
- "Unlike configuration profiles (which APPLY settings), compliance policies CHECK settings"
- "Compliance status is used by conditional access to block/allow resource access"

**What to show**:
- Compliance policies list
- Platform selection for new policy

---

#### Step 2.2: Configure policy basics

**Action**: Name the compliance policy

1. On the **Basics** page:
   - **Name**: `Windows Compliance - Security Requirements`
   - **Description**: `Defines minimum security requirements for Windows devices: BitLocker, firewall, antivirus, password`
2. Click **Next**

**Talking points**:
- "Compliance policy names should clearly indicate what they check for"
- "These policies answer: 'Is this device secure enough to access our data?'"

**What to show**:
- Basics page with name and description

![Compliance policy basics page](media/microsoft-intune-admin-center-new-compliance-policy-basic-details.png)

#### Step 2.3: Configure compliance settings

**Action**: Define security requirements

1. On the **Compliance settings** page, expand and configure the following:

   **Device Health**:
   - **Require BitLocker**: **Require**
   - **Secure Boot**: **Require**

   **Device Properties**:
   - **Minimum OS version**: **10.0.19041** (Windows 10 20H1 minimum)

   **System Security**:
   - **Require a password to unlock mobile devices**: **Require**
   - **Minimum password length**: **8**
   - **Password type**: **Alphanumeric**
   - **Password complexity**: **Require digits, lowercase, uppercase, and special characters**
   - **Firewall**: **Require**
   - **Antivirus**: **Require**
   - **Antispyware**: **Require**

2. Leave other settings at default
3. Click **Next**

**Talking points**:
- "BitLocker requirement checks if encryption is enabled - matches our configuration profile"
- "Secure Boot prevents rootkits and boot-level malware"
- "Minimum OS version ensures devices aren't running old, vulnerable Windows versions"
- "Password, firewall, and antivirus are baseline security requirements"
- "If a device doesn't meet these requirements, it's marked noncompliant"

**What to show**:
- Device Health settings section
- System Security settings section
- How each requirement can be set to Require, Not configured, or specific values

![Compliance policy settings page](media/microsoft-intune-admin-center-new-compliance-policy-settings.png)

#### Step 2.4: Create notification message template

**Action**: Create a template for noncompliance email notifications

1. Before configuring actions, navigate to **Devices** → **Compliance** → **Notifications** tab
2. Click **+ Create notification**
3. On the **Basics** page:
   - **Name**: `Device Compliance Notification`
   - **Email header - Include company logo**: **Enabled** (optional)
   - **Email footer - Include company name**: **Enabled** (optional)
   - **Email footer - Include contact information**: **Enabled** (optional)
4. Click **Next**
5. On the **Notification message templates** page:
   - **Subject**: `Action Required: Your device is not compliant`
   - **Message**: 
     ```
     Hello {{UserName}},
     
     Your device {{DeviceName}} does not meet our organization's security requirements.
     
     Please update your device to maintain access to company resources. Common issues include:
     - BitLocker encryption not enabled
     - Missing required Windows updates
     - Firewall or antivirus disabled
     
     If you need assistance, please contact IT support.
     ```
6. Click **Next**, review, and click **Create**

**Talking points**:
- "Notification templates must be created before you can use them in compliance policies"
- "Templates can include variables like UserName and DeviceName for personalization"
- "You can create multiple templates for different scenarios or languages"
- "Users will receive this email when their device becomes noncompliant"
- "The message should include clear guidance on how to remediate issues"

**What to show**:
- Notifications tab in Compliance section
- Template creation with variable tokens
- Company branding options (header/footer)

<!-- **TODO**: Screenshot of notification template creation -->

#### Step 2.5: Configure actions for noncompliance

**Action**: Define what happens when devices are noncompliant

1. Navigate back to **Devices** → **Compliance** and continue with your compliance policy creation
2. On the **Actions for noncompliance** page, review the default action:
   - **Action**: Mark device noncompliant
   - **Schedule (days after noncompliance)**: Immediately (0 days)
3. Click **+ Add** to add a new action:
   - **Action**: **Send email to end user**
   - **Message template**: Select **Device Compliance Notification** (the template we just created)
   - **Schedule**: **3** days after noncompliance
   - Click **Add**
4. Optionally add another action:
   - **Action**: **Retire the noncompliant device**
   - **Schedule**: **30** days after noncompliance
   - Click **Add**
5. Click **Next**

**Talking points**:
- "Actions define consequences of noncompliance - escalating from warnings to blocking access"
- "Immediately mark noncompliant means conditional access can block right away"
- "Email notification at 3 days gives users a grace period to fix issues"
- "Retire action (extreme) removes corporate data after 30 days of continued noncompliance"
- "You can add multiple email reminders at different intervals if needed"
- "In production, tune these schedules to balance security and user experience"

**What to show**:
- Default action (mark noncompliant immediately)
- How to add additional escalating actions with the Add button
- Message template selection dropdown
- Schedule field for each action
- Multiple actions with different schedules

<!-- **TODO**: Screenshot of Actions for noncompliance with multiple actions configured -->

#### Step 2.6: Assign the compliance policy

**Action**: Target the policy to Windows devices

1. On the **Assignments** page, under **Included groups**, click **Add groups**
2. Select **All Windows Devices**
3. Click **Select**
4. Click **Next**

**Talking points**:
- "Assigning to the same dynamic group as our configuration profile"
- "Configuration profile enforces settings; compliance policy checks if device meets requirements"
- "Together, they ensure devices are both configured correctly and verified compliant"

**What to show**:
- Group assignment for compliance policy

<!--**TODO**: Screenshot of compliance policy assignments-->

#### Step 2.7: Review and create

**Action**: Create the compliance policy

1. On the **Review + create** page, review all settings
2. Click **Create**
3. Wait for success confirmation

**Talking points**:
- "Compliance policies evaluate on device sync - can take 8-24 hours for initial check"
- "Devices that don't meet requirements will show as noncompliant in Intune dashboard"

**What to show**:
- Review page with all compliance settings
- Success confirmation

<!--**TODO**: Screenshot of compliance policy review page-->

---

### Part 3: Demonstrate filters (2-3 minutes)

#### Step 3.1: Create a filter for corporate-owned devices

**Action**: Create a filter based on device ownership

1. In Intune admin center, navigate to **Tenant administration** → **Assignment filters**
2. Click **+ Create**
3. Select filter type: **Managed devices**
4. On the **Basics** page:
   - **Filter name**: `Corporate-Owned Devices Only`
   - **Description**: `Filter for devices with ownership type of Corporate`
   - **Platform**: `Windows 10 and later`
5. Click **Next**
6. On the **Rules** page, configure a new rule:
   - **Property**: **deviceOwnership**
   - **Operator**: **Equals**
   - **Value**: **Corporate**
7. Click **Next** and then **Create**

**Talking points**:
- "Filters provide additional targeting beyond group membership"
- "This filter ensures policies only apply to corporate-owned devices, not BYOD"
- "Filters are evaluated at assignment time - more dynamic than static groups"
- "Common filter scenarios: OS version, device manufacturer, ownership type"

**What to show**:
- Filter creation interface
- Rule builder with property, operator, value
- Preview of matching devices (if available)

![Filter rule configuration](media/microsoft-intune-admin-center-new-assignment-filter-rules.png)

#### Step 3.2: Apply filter to a policy assignment (demonstration only)

**Action**: Show how to use filter in policy assignment

1. Navigate back to **Devices** → **Configuration**
2. Select the **Windows Security Settings** profile created earlier
3. Under **Properties** → **Assignments**, select **Edit**
4. For the **All Windows Devices** group, expand **Edit filter**
5. Select **Include filtered devices in assignment**
6. Choose filter: **Corporate-Owned Devices Only**
7. **Do not save** - this is demonstration only (click **Cancel**)

**Talking points**:
- "Here's how filters apply: group membership PLUS filter condition"
- "This would mean: 'Apply policy to devices in All Windows Devices group that are also corporate-owned'"
- "Filters provide fine-grained control without creating many small groups"
- "You can include or exclude based on filter - very flexible"

**What to show**:
- Filter selection in policy assignment
- Include vs. Exclude filter option
- How filters combine with groups

<!-- **TODO**: Screenshot of applying filter to policy assignment -->

---

### Part 4: Validate policy application (2-3 minutes)

#### Step 4.1: Sync the test device

**Action**: Force device to check in and receive policies

1. Navigate to **Devices** → **All devices**
2. Select the enrolled Windows device from Demo B
3. Click **Sync** in the toolbar

**Talking points**:
- "Sync triggers immediate policy download - no need to wait 8 hours"
- "In production, policies deploy automatically, but manual sync is useful for testing"

**What to show**:
- Device sync action
- Last check-in timestamp updating

![Device sync button](media/microsoft-intune-admin-center-device-sync.png)

#### Step 4.2: Check configuration profile status

**Action**: Verify profile deployment status

1. On the device page, click **Device configuration** in the left menu
2. Look for **Windows Security Settings - Corporate Devices** profile
3. Check status:
   - **Success**: Profile applied successfully
   - **Pending**: Profile is deploying
   - **Error**: Profile failed to apply (investigate)

**Talking points**:
- "Success means BitLocker settings are now enforced on the device"
- "If status shows Pending, wait a few minutes and refresh"
- "Error status indicates a problem - click for details on what failed"

**What to show**:
- Configuration profile list on device page
- Status indicator (green check, yellow pending, red error)

![Device configuration profile status](media/microsoft-intune-admin-center-device-configuration-assignment-status.png)

#### Step 4.3: Check compliance policy status

**Action**: Verify compliance evaluation

1. On the device page, click **Device compliance** in the left menu
2. Look for **Windows Compliance - Security Requirements** policy
3. Check compliance state:
   - **Compliant**: Device meets all requirements
   - **Not compliant**: Device fails one or more requirements
   - **In grace period**: Noncompliant but within grace period
4. If not compliant, click the policy to see which settings failed

**Talking points**:
- "Compliance evaluation may take 15-30 minutes after policy assignment"
- "Compliant devices get a green check; noncompliant get red X"
- "Clicking the policy shows detailed pass/fail for each setting"
- "Noncompliant devices can be blocked from accessing resources via conditional access"

**What to show**:
- Compliance policy list with compliance status
- Detailed compliance check results (expand policy)

![Device compliance status](media/microsoft-intune-admin-center-device-compliance-status.png)

#### Step 4.4: View compliance dashboard

**Action**: Show organization-wide compliance view

1. Navigate to **Devices** → **Compliance** and select the **Windows Compliance - Security Settings** policy
2. Review the **Compliance status** dashboard:
   - Total devices
   - Compliant devices count
   - Noncompliant devices count
   - Devices in grace period
3. Click on **Noncompliant devices** to see list (if any)

**Talking points**:
- "This dashboard gives at-a-glance view of organizational compliance posture"
- "Security teams monitor this to ensure devices meet security standards"
- "Noncompliant devices need remediation before accessing sensitive resources"
- "In Module 4, we'll use compliance status to enforce conditional access"

**What to show**:
- Compliance dashboard with metrics
- Compliant vs. noncompliant breakdown
- List of noncompliant devices (if any exist)

<!-- **TODO**: Screenshot of compliance dashboard -->

---

## Demo Summary

**Recap key steps**:
1. ✅ Created a configuration profile (Settings catalog) to enforce BitLocker encryption and security settings
2. ✅ Assigned configuration profile to dynamic group "All Windows Devices"
3. ✅ Created a compliance policy defining minimum security requirements (BitLocker, firewall, antivirus, password)
4. ✅ Configured actions for noncompliance (mark, email, retire)
5. ✅ Demonstrated filters for conditional policy targeting based on device properties
6. ✅ Validated policy deployment and compliance evaluation on enrolled device

**Key takeaways**:
- "Configuration profiles APPLY settings; compliance policies CHECK if settings meet requirements"
- "Dynamic groups enable automatic policy targeting without manual device assignment"
- "Filters provide additional targeting control beyond group membership"
- "Policy deployment is asynchronous - sync devices for immediate testing, but production deployments take hours"
- "Compliance status is the foundation for conditional access - noncompliant devices can be blocked"

**Transition to next module**:
"Now that we can apply policies and check compliance, we'll add data protection. In Module 4, we'll create app protection policies to prevent data leakage and conditional access policies to enforce device compliance before allowing resource access."

---

## Common Issues and Troubleshooting

### Issue: Policy shows "Pending" status for more than 15 minutes
**Cause**: Device hasn't synced, policy conflict, or deployment delay  
**Solution**: 
- Manually sync device: Device page → Sync button
- Wait up to 8 hours for automatic sync
- Check for conflicting policies with higher priority

### Issue: Device shows "Not compliant" but settings appear correct
**Cause**: Compliance evaluation hasn't run yet, or setting doesn't exactly match requirement  
**Solution**: 
- Wait 30 minutes for compliance evaluation
- Manually sync device to trigger evaluation
- Click into compliance policy details to see exactly which setting failed
- Verify setting value exactly matches requirement (e.g., password length)

### Issue: Cannot find BitLocker setting in Settings catalog
**Cause**: Wrong category or search term  
**Solution**: 
- Use Settings picker search: Type "BitLocker" or "encryption"
- Check under categories: Security → BitLocker
- Alternative: Use Templates → Endpoint protection template for pre-configured BitLocker settings

### Issue: Filter doesn't seem to apply to policy
**Cause**: Filter logic incorrect, or device doesn't match filter criteria  
**Solution**: 
- Verify device meets filter criteria (check device properties: ownership, OS version, etc.)
- Test filter logic: Filters → Select filter → Preview matching devices
- Check filter is applied to correct group in policy assignment (Include vs. Exclude)

### Issue: Configuration profile and compliance policy conflict
**Cause**: Configuration profile sets value, compliance policy requires different value  
**Solution**: 
- Ensure configuration profiles and compliance policies align
- Example: Config sets minimum password to 10, compliance requires 8 - device will be compliant but users experience 10-char requirement
- Best practice: Configuration requirements should meet or exceed compliance requirements

---

## Policy Precedence and Conflict Resolution

**Important concept to mention**:

When multiple policies apply to the same device:
1. **Most restrictive wins**: If Policy A requires 8-char password and Policy B requires 10-char, device gets 10-char requirement
2. **Last applied**: For non-security settings, most recently assigned policy takes precedence
3. **Explicit vs. not configured**: Explicit setting beats "not configured"

**Best practices**:
- Avoid overlapping policies that configure the same settings
- Use clear naming to indicate policy purpose and scope
- Document policy intent in descriptions
- Test policies on pilot groups before broad deployment

---

## Additional Resources

- [Use the settings catalog in Intune](https://learn.microsoft.com/mem/intune/configuration/settings-catalog)
- [Create compliance policies in Intune](https://learn.microsoft.com/mem/intune/protect/create-compliance-policy)
- [Use filters when assigning policies](https://learn.microsoft.com/mem/intune/fundamentals/filters)
- [Monitor device compliance policies](https://learn.microsoft.com/mem/intune/protect/compliance-policy-monitor)

---

**Demo Status**: ✅ Ready for delivery  
**Last Updated**: November 11, 2025  
**Next Demo**: Demo D - App Protection and Conditional Access
