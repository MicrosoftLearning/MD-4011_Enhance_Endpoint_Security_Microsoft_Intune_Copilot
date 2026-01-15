# Demo A: Tenant Readiness and License Assignment

**Module**: Module 1 - Prepare identity and onboard devices  
**Duration**: 10-12 minutes  
**Difficulty**: Beginner  
**Demo Type**: Instructor-led walkthrough

## Learning Objectives

After this demonstration, learners will understand how to:
- Configure Microsoft Entra ID for device management
- Assign appropriate licenses for Intune and endpoint security
- Set up organizational units (groups) for device management
- Configure automatic MDM enrollment
- Verify tenant readiness for device onboarding

## Prerequisites

### Instructor Requirements
- Global Administrator or Intune Administrator role
- User Administrator role (for user/group management)
- Access to Microsoft 365 admin center and Entra admin center

### Environment Requirements
- Microsoft 365 tenant (E3, E5, or EMS E5)
- At least 2 test user accounts (one for device enrollment, one for admin)
- No existing Intune configuration (or ability to show configuration steps)

### Licenses Required
- Microsoft 365 E5, E3 + EMS E5, or standalone Intune licenses
- Licenses must be available for assignment (not all consumed)

## Demo Scenario

**Context**: You are Contoso Healthcare's IT administrator preparing the Microsoft 365 tenant for modern device management. Before enrolling devices, you need to ensure proper licensing, permissions, and automatic enrollment configuration.

**Narrative**: "Before we can start enrolling devices in Intune, we need to prepare our tenant. This involves three key steps: assigning the right licenses, setting up groups for device management, and configuring automatic MDM enrollment. Let's walk through each of these."

## Step-by-Step Instructions

### Part 1: Verify and assign licenses (3-4 minutes)

#### Step 1.1: Check available licenses

**Action**: Navigate to Microsoft 365 admin center

1. Open browser and go to **https://admin.microsoft.com**
2. Sign in with Global Administrator credentials
3. In the left navigation, expand **Billing** → Select **Licenses**
4. Review the licenses available in your tenant

**What to show**:
- Total licenses purchased vs. assigned
- License types available: Microsoft 365 E5, EMS E5, Intune Plan 1
- Identify which licenses include Intune (E5, EMS E5, standalone Intune)

![Licenses page showing available license inventory](media/microsoft-365-admin-center-licenses.png)

#### Step 1.2: Assign license to test user

**Action**: Assign Intune license to a test user

1. In Microsoft 365 admin center, navigate to **Users** → **Active users**
2. Search for and select a test user (e.g., "Alex Wilber" or your test user)
3. Click **Licenses and apps** tab
4. Check the box next to **Microsoft 365 E5** (or appropriate license)
5. Expand the license to view included services
6. Verify **Microsoft Intune** is checked under included services
7. Click **Save changes**

**What to show**:
- License assignment UI
- Specific Intune service toggle within the license
- Confirmation message after assignment

![User license assignment showing Intune service enabled](media/microsoft-365-admin-center-user-licenses.png)

#### Step 1.3: Verify Intune subscription is active

**Action**: Confirm Intune appears in tenant subscriptions

1. In Microsoft 365 admin center, go to **Billing** → **Your products**

**What to show**:
- Active Intune subscription in the list of products

![Subscriptions showing active Intune subscription](media/microsoft-365-admin-center-product-details.png)

---

### Part 2: Configure Microsoft Entra ID for device management (4-5 minutes)

#### Step 2.1: Navigate to Entra admin center

**Action**: Switch to Microsoft Entra admin center

1. Open a new browser tab and navigate to **https://entra.microsoft.com**
2. Sign in with the same admin credentials
3. In the left navigation, expand **Entra ID** → Select **Devices**
4. Select **Overview** to see current device enrollment state

**Talking points**:
- "Entra ID (formerly Azure AD) is the identity foundation for device management"
- "Devices join or register to Entra ID, then enroll in Intune for management"
- "We need to configure settings that allow device enrollment"

**What to show**:
- Devices overview page (likely shows zero devices if new tenant)
- Navigation structure of Entra admin center

![Device overview page](media\microsoft-entra-admin-center-devices-overview.png)

#### Step 2.2: Configure device settings

**Action**: Set device enrollment permissions

1. In **Devices**, select **Device settings**
2. Review the following settings:
   - **Users may join devices to Azure AD**: Verify set to **All** or **Selected** (with appropriate groups)
   - **Users may register their devices with Azure AD**: Verify set to **All** or **Selected**
   - **Require Multi-Factor Authentication to register or join devices**: Note current setting (recommended: Enabled for production)
3. For demo purposes, ensure **All** is selected for both join and register options
4. Click **Save** if any changes were made

**Talking points**:
- "This controls which users can join devices to Entra ID"
- "In production, you might limit this to specific groups or require MFA"
- "For our demo, we'll allow all users so enrollment works smoothly"
- "Joining a device to Entra ID is the first step before Intune enrollment"

**What to show**:
- Device settings configuration options
- Explanation of "Join" (corporate-owned, fully managed) vs. "Register" (BYOD, lighter management)

![Device settings page with options highlighted](media/microsoft-entra-admin-center-device-settings.png)

#### Step 2.3: Verify MDM authority and configure automatic enrollment

**Action**: Confirm MDM authority is set and enable automatic enrollment into Intune

1. Open a new browser tab and navigate to **https://intune.microsoft.com**
2. Sign in with the same admin credentials
3. Go to **Tenant administration** → **Tenant status**
4. Under **Tenant details**, verify **MDM authority** shows **Microsoft Intune**
   - If you see an orange banner indicating MDM authority isn't set, select the banner and choose **Intune MDM Authority**
   - This is typically already configured for new tenants
5. Navigate to **Devices** > **Enrollment** → **Automatic Enrollment**
6. Review **MDM user scope**:
   - If set to **None**: Change to **All** or **Some** (with selected groups)
   - If already configured: Review current scope
7. Select **All** for demo purposes
8. Review **MDM terms of use URL** (should auto-populate with Intune URL)
9. Click **Save**

**Talking points**:
- "The MDM authority is automatically set to Intune when you create a new tenant or trial"
- "We're verifying it shows Microsoft Intune as the management authority for devices"
- "Automatic enrollment means when users join devices to Entra ID, they automatically enroll in Intune"
- "This eliminates a manual step and ensures devices are managed immediately upon joining"
- "MDM user scope controls who can auto-enroll - All users, specific groups, or none"
- "In production, you might scope this to pilot groups first before enabling for all users"

**What to show**:
- MDM authority value showing "Microsoft Intune" in Tenant status
- Automatic Enrollment settings page
- MDM user scope dropdown options
- Save confirmation message

**Note for instructors**: If learners encounter an orange banner about MDM authority not being set (rare in new tenants), this is the only time they need to manually configure it. Most modern Intune tenants have this pre-configured.

![Automatic Enrollment configuration with MDM scope set to All](media/microsoft-intune-admin-center-automatic-enrollment.png)

---

### Part 3: Create groups for device management (3-4 minutes)

#### Step 3.1: Create a dynamic device group

**Action**: Create a dynamic group for Windows devices

1. In Entra admin center, navigate to **Groups** → **All groups**
2. Click **New group**
3. Configure the group:
   - **Group type**: Security
   - **Group name**: `All Windows Devices`
   - **Group description**: `Dynamic group containing all Windows devices managed by Intune`
   - **Membership type**: Dynamic Device
4. Click **Add dynamic query**
5. In the **Rule syntax** editor, enter this query:

```
(device.deviceOSType -eq "Windows")
```

6. Click **Save** to save the query
7. Click **Create** to create the group

**Talking points**:
- "Dynamic groups automatically populate based on device or user attributes"
- "This Windows devices group will auto-populate as we enroll Windows devices"
- "We'll use this group to target policies to all Windows devices later"
- "Dynamic groups update automatically - no manual membership management needed"

**What to show**:
- Group creation interface
- Dynamic query builder
- Query syntax for device OS type filtering

![Dynamic group creation with query visible](media/microsoft-entra-admin-center-new-dynamic-group.png)

#### Step 3.2: Create a static test group

**Action**: Create a manual group for pilot testing

1. Click **New group** again
2. Configure the group:
   - **Group type**: Security
   - **Group name**: `Device Management Pilot Users`
   - **Group description**: `Users participating in the device management pilot`
   - **Membership type**: Assigned
3. Click **No members selected** under **Members**
4. Search for and select the test user you licensed earlier
5. Click **Select**
6. Click **Create**

**Talking points**:
- "Static (assigned) groups are useful for pilot deployments or special groups"
- "We'll use this pilot group to test policies on specific users before broad deployment"
- "Best practice: Start with pilot groups, validate, then expand to broader groups"
- "This mimics real-world deployment patterns - never deploy directly to all users"

**What to show**:
- Assigned membership group creation
- Member selection process
- Final group summary

![Assigned group with members selected](media/microsoft-entra-admin-center-new-static-group.png)

---

### Part 4: Verify Intune tenant status (1-2 minutes)

#### Step 4.1: Check Intune tenant connection

**Action**: Verify Intune admin center access

1. Open a new browser tab and navigate to **https://intune.microsoft.com**
2. Sign in with the same admin credentials
3. Review the **Home** page dashboard
4. In the left navigation, go to **Tenant administration** → **Tenant status**
5. Review the following sections:
   - **Tenant details**: Verify tenant name and MDM authority (should show Microsoft Intune)
   - **Connector status**: Verify status (should be mostly empty in new tenant)
   - **Intune service health**: Check for any incidents or advisories

**Talking points**:
- "The Intune admin center is where we'll manage all device policies, apps, and compliance settings"
- "Tenant status confirms Intune is properly configured and connected to our Entra ID"
- "MDM authority should always show Microsoft Intune - if it shows something else, enrollment won't work"
- "Service health shows if Microsoft is experiencing any Intune service issues"

**What to show**:
- Intune admin center home dashboard
- Tenant status page with MDM authority highlighted
- Clean service health (or explain any current issues)

![Intune tenant status page showing active status](media/microsoft-intune-admin-center-tenant-status.png)

---

## Demo Summary

**Recap key steps**:
1. ✅ Assigned appropriate licenses (M365 E5 or Intune licenses) to test users
2. ✅ Configured Entra ID device settings to allow device joining and registration
3. ✅ Enabled automatic MDM enrollment so devices enroll in Intune automatically
4. ✅ Created dynamic and static groups for device targeting and policy assignment
5. ✅ Verified Intune tenant status and MDM authority

**Key takeaways**:
- "Licensing is the foundation - users need licenses before devices can enroll"
- "Automatic enrollment eliminates manual steps and ensures compliance"
- "Groups enable targeted policy deployment and phased rollouts"
- "Always verify tenant readiness before enrolling devices"

**Transition to next module**:
"Now that our tenant is ready, we can start enrolling devices. In Module 2, we'll walk through enrolling a Windows device and validating it appears in both Entra ID and Intune."

---

## Common Issues and Troubleshooting

### Issue: "Intune doesn't appear in license services"
**Cause**: License SKU doesn't include Intune  
**Solution**: Verify you're using E5, EMS E5, or standalone Intune licenses. E3 alone doesn't include Intune.

### Issue: "Cannot enable automatic MDM enrollment"
**Cause**: Intune MDM authority not configured  
**Solution**: Navigate to **Entra admin center** → **Devices** → **Enroll** → **Mobile Device Management** and add Microsoft Intune.

### Issue: "Dynamic group query doesn't work"
**Cause**: Syntax error in query  
**Solution**: Use the query builder UI instead of manual entry. Verify property names exactly match Microsoft documentation.

### Issue: "User license assignment not showing immediately"
**Cause**: License propagation delay  
**Solution**: Wait 15-30 minutes for license changes to propagate across services. Check M365 admin center → Users → Licenses to confirm assignment.

---

## Cleanup Steps

If demonstrating in a production-like environment and need to reset:

1. **Remove test user licenses**: Go to M365 admin center → Users → Select user → Licenses tab → Uncheck licenses
2. **Delete test groups**: Go to Entra admin center → Groups → Select group → Delete
3. **Reset MDM enrollment scope**: Go to Entra admin center → Devices → Enroll → Automatic Enrollment → Set to None

**Warning**: Do NOT clean up in a live tenant being used for actual device management.

---

## Additional Resources

- [Set up Intune enrollment for Windows devices](https://learn.microsoft.com/mem/intune/enrollment/windows-enrollment-methods)
- [Assign licenses to users in Microsoft 365](https://learn.microsoft.com/microsoft-365/admin/manage/assign-licenses-to-users)
- [Configure automatic MDM enrollment](https://learn.microsoft.com/mem/intune/enrollment/windows-enroll#enable-windows-automatic-enrollment)
- [Create dynamic groups in Entra ID](https://learn.microsoft.com/entra/identity/users/groups-create-rule)

---

**Demo Status**: ✅ Ready for delivery  
**Last Updated**: November 11, 2025  
**Next Demo**: Demo B - Device Enrollment and Validation
