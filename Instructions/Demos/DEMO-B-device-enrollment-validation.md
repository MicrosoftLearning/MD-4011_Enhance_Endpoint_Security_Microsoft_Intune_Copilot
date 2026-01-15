# Demo B: Device Enrollment and Validation

**Module**: Module 2 - Enroll and validate devices  
**Duration**: 10-12 minutes  
**Difficulty**: Beginner to Intermediate  
**Demo Type**: Instructor-led hands-on

## Learning Objectives

After this demonstration, learners will understand how to:
- Enroll a Windows device using manual (user-driven) enrollment
- Validate device registration in Microsoft Entra ID
- Validate device enrollment in Microsoft Intune
- View device properties, compliance status, and assigned policies
- Understand the difference between device registration and enrollment
- Troubleshoot common enrollment issues

## Prerequisites

### Instructor Requirements
- Intune Administrator or Global Administrator role
- Physical Windows 11 device or Windows VM (not already enrolled)
- Test user account with Intune license assigned (from Demo A)

### Environment Requirements
- Completion of Demo A (tenant readiness, licensing, automatic enrollment)
- Windows 11 22H2 or later (or Windows 10 version 1903+)
- Device must be connected to the internet
- Device should NOT be joined to on-premises Active Directory
- Company Portal app installed (or ability to install from Microsoft Store)

### Licenses Required
- Test user must have Microsoft 365 E5, E3 + EMS E5, or Intune license assigned

## Demo Scenario

**Context**: Contoso Healthcare has prepared their tenant and is ready to start enrolling devices. Alex Wilber, a Finance department employee, received a new Windows 11 laptop and needs to set it up for corporate use.

**Narrative**: "Now that our tenant is configured, let's enroll Alex's Windows 11 device. We'll walk through the user experience of joining the device to Entra ID and enrolling it in Intune. Then we'll verify the device appears in our management portals."

## Step-by-Step Instructions

### Part 1: Enroll Windows device (manual enrollment) (4-5 minutes)

#### Step 1.1: Access work or school account settings

**Action**: Open Windows settings to add work account

1. On the Windows 11 device, open **Settings** (press Windows key + I)
2. In the left navigation, select **Accounts**
3. Select **Access work or school**
4. Click **Connect** button

**Talking points**:
- "This is the user-facing experience for enrolling a device"
- "Users with personal devices or new corporate devices will go through this process"
- "The Connect button initiates both Entra ID join and Intune enrollment"

**What to show**:
- Settings app navigation to Access work or school
- Connect button that initiates enrollment

![Access work or school page with Connect button highlighted](media/windows-11-account-school-status.png)

#### Step 1.2: Sign in with organizational account

**Action**: Enter test user credentials

1. In the **Set up a work or school account** window, enter the test user's email (e.g., AlexW@contoso.onmicrosoft.com)
2. Click **Next**
3. On the Microsoft sign-in page, enter the user's password
4. If prompted for MFA, complete the multi-factor authentication flow
5. Wait for the "You're all set!" message

**Talking points**:
- "The system detects this is a Microsoft 365 account and redirects to Microsoft sign-in"
- "If MFA is required (recommended for production), users complete that here"
- "Behind the scenes, two things are happening: device joins Entra ID and enrolls in Intune"
- "Because we configured automatic enrollment in Demo A, Intune enrollment happens automatically"

**What to show**:
- Microsoft sign-in page
- MFA prompt (if configured)
- Progress indicator during enrollment
- Success message

**Common pause point**: After clicking Next, pause for 15-30 seconds while device contacts Intune and downloads policies.

<!-- **TODO**: Screenshot of Microsoft sign-in page for work account

**TODO**: Screenshot of "You're all set!" success message-->

#### Step 1.3: Verify connection in Windows settings

**Action**: Confirm device shows as connected

1. Return to **Settings** → **Accounts** → **Access work or school**
2. You should now see your organization account listed:
   - Account name: AlexW@contoso.onmicrosoft.com
   - Organization name: Contoso Healthcare
   - Status: Connected
3. Click on the account to expand details
4. Click **Info** button to view device management details

**Talking points**:
- "Connected status means device successfully joined Entra ID and enrolled in Intune"
- "The Info page shows sync status, areas managed by the organization, and more details"
- "Users can manually sync their device from here if they need immediate policy updates"

**What to show**:
- Connected account with organization name
- Info page showing management areas (Security policies, Compliance policies, etc.)
- Last sync time

![Connected account in Access work or school](media/windows-11-account-school-status.png)
<!-- **TODO**: Screenshot of Info page showing managed areas -->

---

### Part 2: Validate device in Microsoft Entra ID (2-3 minutes)

#### Step 2.1: View device in Entra admin center

**Action**: Verify device registration in Entra ID

1. Switch to browser with **https://entra.microsoft.com** open
2. Navigate to **Entra ID** → **Devices** → **All devices**
3. Look for the newly enrolled device in the list (may take 1-2 minutes to appear)
4. Click on the device name to view device details

**Talking points**:
- "Entra ID Devices shows all devices registered or joined to our directory"
- "This device will show as 'Entra joined' - meaning it's corporate-owned and fully joined"
- "The Registered Owner is Alex Wilber - the user who enrolled it"

**What to show**:
- Devices list with newly enrolled device
- Device detail page showing:
  - Display name (e.g., DESKTOP-ABC1234)
  - Join type: Entra joined
  - Owner: Alex Wilber
  - Operating system: Windows
  - Compliance status

![All devices list with new device highlighted](media/microsoft-entra-admin-center-devices-overview.png)

#### Step 2.2: Review device properties

**Action**: Examine device attributes

1. On the device details page, review key properties:
   - **Operating System**: Windows
   - **Version**: Windows 11 (or specific version)
   - **Device ID**: Unique identifier in Entra ID
   - **MDM**: Microsoft Intune (confirms enrollment)
   - **Compliant**: Likely shows "Yes" if no compliance policies applied yet, or "Evaluating"
2. Click **Activity logs** tab to see recent device events (join, sync)

**Talking points**:
- "Device ID is the unique Entra ID identifier for this device"
- "MDM field confirms it's enrolled in Intune - this links identity and management"
- "Compliance status shows if device meets your security requirements"
- "Activity logs help troubleshoot if enrollment fails or device has issues"

**What to show**:
- Key device properties
- MDM field showing Microsoft Intune
- Compliance status

![Device properties with MDM and compliance fields highlighted](media/microsoft-entra-admin-center-demo-device-settings.png)

---

### Part 3: Validate device in Microsoft Intune (4-5 minutes)

#### Step 3.1: Locate device in Intune admin center

**Action**: Find the enrolled device in Intune

1. Switch to browser tab with **https://intune.microsoft.com** open
2. Navigate to **Devices** → **All devices**
3. Look for the newly enrolled device (use search if needed)
4. Click on the device name to open the device overview page

**Talking points**:
- "Intune Devices shows all managed devices - this is where we manage policies, apps, and compliance"
- "The same device appears in both Entra ID (for identity) and Intune (for management)"
- "Device may take 5-10 minutes to fully appear and sync initial status"

**What to show**:
- All devices list in Intune
- Device showing in list with platform (Windows), enrollment date, compliance status

<!--**TODO**: Screenshot of Intune All devices list with new device-->

#### Step 3.2: Review device overview and properties

**Action**: Examine device management details

1. On the device overview page, review the following sections:
   - **Device name**: Hostname of the Windows device
   - **Ownership**: Corporate or Personal (should show Corporate)
   - **Compliance state**: Compliant, Not compliant, or In grace period
   - **Operating system**: Windows 11 (or Virtual Machine)
   - **Last check-in**: Timestamp of last sync with Intune
   - **Primary user**: Alex Wilber
2. Click **Properties** in the left menu to see additional device details

**Talking points**:
- "Last check-in shows when the device last contacted Intune - should be recent"
- "Primary user is the enrolled user - this affects user-targeted policies"
- "Compliance state is critical - we'll use this for conditional access later"
- "Ownership determines what policies can be applied - corporate devices have more control"

**What to show**:
- Device overview with all key fields
- Compliance state indicator (green check or red X)
- Last check-in time
- Properties page with detailed information

![Device properties page](media/microsoft-intune-admin-center-demo-device-settings.png)

#### Step 3.3: View device compliance details

**Action**: Check compliance policy status

1. On the device page, click **Device compliance** in the left menu
2. Review compliance policy status:
   - If no compliance policies assigned: Shows "No compliance policies assigned"
   - If policies assigned: Shows policy name and compliance state
3. Click **Device configuration** in the left menu
4. Review configuration profile status:
   - Shows any assigned configuration profiles
   - Status: Pending, Success, Error, or Not applicable

**Talking points**:
- "We haven't assigned compliance policies yet, so device shows compliant by default"
- "In Module 3, we'll create compliance policies that devices must meet"
- "Configurations shows which configuration profiles are applied to this device"
- "Pending status means policy is deploying; Success means policy applied successfully"

**What to show**:
- Device compliance page (empty if no policies assigned)
- Configurations page showing any auto-assigned profiles (like Windows Update policies)

![Device compliance page](media/microsoft-intune-admin-center-demo-device-compliance.png)

![Configurations page](media/microsoft-intune-admin-center-device-configuration-profile.png)

#### Step 3.4: Review assigned policies and apps

**Action**: See what's deployed to the device

1. On the device page, click **Managed apps** in the left menu
2. View any apps assigned to the device (may be empty for new enrollment)
3. Under **Monitor**, select **Group memberships**
4. Verify device is a member of expected groups (e.g., "All Windows Devices" dynamic group from Demo A)

**Talking points**:
- "Managed apps shows apps deployed via Intune - could include Microsoft 365, LOB apps, or store apps"
- "Group memberships determine which policies and apps this device receives"
- "Remember the dynamic group we created? This device should automatically be a member now"
- "As we create policies in the next modules, they'll target these groups"

**What to show**:
- Managed apps page (even if empty, explain it will populate as apps are assigned)
- Group memberships showing dynamic group membership


![Group memberships](media/microsoft-intune-admin-center-demo-device-membership.png)

---

### Part 4: Demonstrate device synchronization (1-2 minutes)

#### Step 4.1: Manually trigger device sync from portal

**Action**: Force device to check in with Intune

1. On the device overview page in Intune, click the **Sync** button in the top toolbar
2. Confirm the sync action
3. Wait 10-15 seconds, then click **Refresh** in the browser
4. Review updated "Last check-in" timestamp

**Talking points**:
- "Devices sync automatically every 8 hours, but users or admins can force sync"
- "This is useful when you deploy a new policy and want immediate results"
- "In the real world, after creating a policy, you'd sync the device to receive it quickly"

**What to show**:
- Sync button location
- Last check-in updating to current time

![Sync button in device toolbar](media/microsoft-intune-admin-center-device-sync.png)

#### Step 4.2: View sync from end-user perspective (optional if time allows)

**Action**: Show user-initiated sync on the device

1. On the Windows device, open **Settings** → **Accounts** → **Access work or school**
2. Click on the connected work account
3. Click **Info**
4. Scroll down and click **Sync** button
5. Wait for "Sync completed successfully" message

**Talking points**:
- "End users can sync their devices if they experience policy issues or need immediate updates"
- "This is a common troubleshooting step for users - 'Have you tried syncing your device?'"
- "Sync takes 30-60 seconds depending on how many policies and apps are deployed"

**What to show**:
- User-facing sync button location
- Sync success message

![User-initiated sync in Windows settings](media/windows-11-device-sync.png)

---

## Demo Summary

**Recap key steps**:
1. ✅ Enrolled a Windows 11 device using work or school account connection
2. ✅ Verified device registration in Microsoft Entra ID (identity layer)
3. ✅ Validated device enrollment in Microsoft Intune (management layer)
4. ✅ Reviewed device properties, compliance status, and group memberships
5. ✅ Demonstrated manual device synchronization from portal and device

**Key takeaways**:
- "Device enrollment is a two-part process: Entra ID join (identity) + Intune enrollment (management)"
- "Automatic enrollment setting makes this seamless for users - one sign-in accomplishes both"
- "Devices appear in both Entra admin center and Intune admin center with linked information"
- "Group memberships (especially dynamic groups) determine which policies devices receive"

**Transition to next module**:
"Now that we have a managed device, we can start applying policies. In Module 3, we'll create configuration profiles and compliance policies to secure and configure this device."

---

## Common Issues and Troubleshooting

### Issue: "This device is already enrolled" error
**Cause**: Device was previously enrolled and not properly unenrolled  
**Solution**: 
- On device: Settings → Accounts → Access work or school → Select account → Disconnect
- In Intune: Delete the old device record
- Try enrollment again

### Issue: Device shows "Entra registered" instead of "Entra joined"
**Cause**: User chose "Set up for work or school" option instead of joining to Entra ID  
**Solution**: 
- Entra registered = BYOD/personal device (lighter management)
- Entra joined = corporate device (full management)
- To get full management, device needs to be Entra joined, not registered

### Issue: Device appears in Entra ID but not in Intune
**Cause**: Automatic MDM enrollment not configured or enrollment failed  
**Solution**: 
- Verify automatic enrollment is configured (Demo A, Part 2, Step 2.3)
- Check user has Intune license assigned
- Review enrollment status in Intune: Devices → Monitor → Enrollment failures

### Issue: Compliance shows "Not evaluated" or "In grace period"
**Cause**: No compliance policies assigned yet, or policies still deploying  
**Solution**: 
- This is normal for newly enrolled devices without compliance policies
- Assign a compliance policy (covered in Module 3)
- Wait 8-15 minutes for policy evaluation, or manually sync device

### Issue: "Last check-in" is more than 1 hour ago
**Cause**: Device sync issues or offline device  
**Solution**: 
- Verify device has internet connectivity
- Manually sync from device: Settings → Accounts → Info → Sync
- Check Intune service health: Intune admin center → Tenant administration → Service health

---

## Cleanup Steps

If demonstrating in a test environment and need to unenroll:

**From the device**:
1. Settings → Accounts → Access work or school
2. Select the connected work account
3. Click **Disconnect**
4. Confirm disconnection
5. Device will be removed from Entra ID and Intune

**From Intune admin center**:
1. Devices → All devices
2. Select the device
3. Click **Delete**
4. Confirm deletion

**Warning**: Disconnecting removes ALL corporate data, apps, and policies from the device. Don't do this on active user devices.

---

## Alternative Enrollment Methods

If time allows, briefly mention these other enrollment methods (full demos in separate sessions):

### Windows Autopilot (mentioned, not demonstrated)
- "Autopilot enables zero-touch deployment - devices come pre-registered from manufacturer"
- "Users sign in once, device automatically joins and configures"
- "Ideal for new device procurement and remote workers"

### Bulk enrollment (mentioned, not demonstrated)
- "IT admins can enroll multiple devices without user interaction"
- "Uses provisioning packages or Device Enrollment Manager accounts"
- "Useful for shared devices, kiosks, or classroom devices"

### Co-management with Configuration Manager (mentioned, not demonstrated)
- "For organizations with existing ConfigMgr, devices can be co-managed"
- "Some policies from Intune, others from ConfigMgr - phased transition"

---

## Additional Resources

- [Enroll Windows devices in Intune](https://learn.microsoft.com/mem/intune/enrollment/windows-enrollment-methods)
- [Troubleshoot Windows device enrollment](https://learn.microsoft.com/troubleshoot/mem/intune/device-enrollment/troubleshoot-windows-enrollment-errors)
- [View device details in Intune](https://learn.microsoft.com/mem/intune/remote-actions/device-inventory)
- [Sync devices in Intune](https://learn.microsoft.com/mem/intune/remote-actions/device-sync)

---

**Demo Status**: ✅ Ready for delivery  
**Last Updated**: November 11, 2025  
**Next Demo**: Demo C - Policy Layering and Compliance
