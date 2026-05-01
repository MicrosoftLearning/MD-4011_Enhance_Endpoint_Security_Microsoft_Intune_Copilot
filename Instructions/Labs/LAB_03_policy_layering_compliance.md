---
lab:
  title: 'Lab 03: Implement policy layering and compliance'
  type: Answer Key
  module: 'Module 03: Configure and secure devices with Microsoft Intune policies'
  description: In this lab, you will create and deploy configuration profiles to manage device settings, create compliance policies to enforce security requirements, use filters to target specific devices, and validate policy application on enrolled devices. You will learn how Intune applies policies and evaluates device compliance against organizational security standards.
  duration: 45 minutes
  level: 300
  islab: true
---

# Lab 03: Implement policy layering and compliance
# Student lab answer key

> **Abstract:**  
> In this lab, you will create and deploy configuration profiles to manage device settings, create compliance policies to enforce security requirements, use filters to target specific devices, and validate policy application on enrolled devices. You will learn how Intune applies policies and evaluates device compliance against organizational security standards.

## Lab scenario

Continuing as **Diego Sicilliani**, Contoso Healthcare's Modern Endpoint Administrator, you have successfully enrolled Windows devices into Intune in Lab 02. Now you need to implement security policies to ensure devices meet Contoso's healthcare industry compliance requirements.

In this lab, you will create configuration profiles to enforce security settings like BitLocker encryption and firewall configuration, create compliance policies to define minimum security requirements, use filters to target policies to corporate-owned devices only, and validate that policies are applied successfully and devices are evaluated for compliance.

## Lab Duration

  - **Estimated Time to complete**: 45 minutes

## Instructions

### Before You Begin

> [!IMPORTANT]
> **Prerequisites**: You must complete **Lab 01** and **Lab 02** before starting this lab. You need at least one enrolled Windows device to apply policies to.

> [!IMPORTANT]
> **Administrative Account**: Continue using **Diego Siciliani's** account (DiegoS@yourtenant.onmicrosoft.com) for all administrative tasks. Diego has the **Intune Administrator** role assigned in Lab 01, which provides the necessary permissions for policy and compliance management.

## Exercise 1: Create configuration profiles

### Exercise Duration

  - **Estimated Time to complete**: 15 minutes

In this exercise, you will create a configuration profile using the Settings Catalog to configure BitLocker encryption settings on Windows devices.

### Task 1 - Create a Settings Catalog configuration profile for BitLocker

1. Navigate to the **Microsoft Intune admin center** at [**https://intune.microsoft.com**](https://intune.microsoft.com/).

1. Sign in with **Diego Siciliani's** credentials (DiegoS@yourtenant.onmicrosoft.com) if prompted.

    > [!NOTE]
    > You assigned Diego the **Intune Administrator** role in Lab 01, which provides the necessary permissions for policy and compliance management.

1. In the left navigation pane, go to the Devices page and then expand **Manage devices** and select **Configuration**.

1. On the **Configuration** page, select the **Policies** tab.

1. Select **+ Create** → **+ New policy**.

1. On the **Create a profile** pane, configure:
    - **Platform**: Windows 10 and later
    - **Profile type**: Settings catalog

1. Select **Create**.

1. On the **Basics** page:
    - **Name**: `Windows Security Settings - Corporate Devices`
    - **Description**: `Enforces BitLocker encryption and security settings on corporate Windows devices`

1. Select **Next**.

1. On the **Configuration settings** page, select **+ Add settings**.

1. In the **Settings picker**, use the search box and search for: `BitLocker`

1. Expand **BitLocker** and select the following settings by checking the boxes:
    - **Require Device Encryption**

1. Search for `Windows Hello for Business` and select:
    - **Minimum PIN Length**

1. Select **Close** to return to the configuration settings page.

1. Configure the selected settings:
    - **Require Device Encryption**: Yes
    - **Minimum PIN Length**: 6

1. Select **Next** and skip the **Scope tags** page.

1. On the **Assignments** page, under **Included groups**, select **+ Add groups**.

1. Search for and select **All Windows Devices** (the dynamic group created in Lab 01).

1. Select **Next**.

1. On the **Review + create** page, review your configuration and select **Create**.

You have successfully created a configuration profile to enforce BitLocker encryption and minimum PIN length on Windows devices.

### Task 2 - Monitor configuration profile deployment

1. After creating the profile, you are returned to the **Policies** list.

1. Select the **Windows Security Settings - Corporate Devices** profile you just created (Choose **Refresh** if it doesn't show right away).

1. On the profile overview page, review the deployment status:
    - **Assignment status**: Shows how many devices the policy is assigned to
    - **Device status**: Success, Pending, Error, Not applicable

    > [!NOTE]
    > Initial status may show "Pending" as devices have not yet checked in. Policy deployment can take 8 hours for the scheduled sync, or you can manually sync devices.

1. Select **Device status** in the left menu to see per-device deployment status.

1. Leave the browser window open for the next exercise.

## Exercise 2: Create compliance policies

### Exercise Duration

  - **Estimated Time to complete**: 15 minutes

In this exercise, you will create a compliance policy that defines security requirements devices must meet to be considered compliant.

### Task 1 - Create notification message templates

In this task, you will create notification message templates that will be sent to users when their devices become noncompliant.

1. You are in the **Microsoft Intune admin center**.

1. In the left navigation pane, go to the Devices page and then expand **Manage devices** and select **Compliance**.

1. Select the **Notifications** tab. 

1. Select **+ Create notification** under **Compliance notifications**.

1. On the **Basics** page, fill out the following and select **Next**:
    - **Name**: `Device Non-Compliance Notification`

1. Leave the default values on the **Header and footer settings** page and Select **Next**.

1. On the **Notification message templates** page, choose **+ add** and configure the default message:
    - **Locale**: `English (United States)` or your choice
    - **Subject**: `ACTION NEEDED: Your device is non-compliant`
    - **Message**: 
    ```
    Your device {{DeviceName}} does not meet Contoso Healthcare's security requirements.
    
    Please take action to resolve the following compliance issues:
    {{ComplianceIssues}}
    
    If your device remains noncompliant for 30 days, it will be retired from management.
    
    For assistance, contact IT Support.
    ```

1. Select **Save** and then **Next**.

1. On the **Review + create** page, select **Create**.

1. Repeat the steps to create another **Compliance notification** with these properties:
    - **Name**: `Device Retirement Warning`
    - **Locale**: `English (United States)` or your choice
    - **Subject**: `ACTION REQUIRED: Your device will be retired soon`
    - **Message**: 
    ```
    Your device {{DeviceName}} does not meet Contoso Healthcare's security requirements and has been out of compliance for 27 days.
    
    Please take action to resolve the following compliance issues or your device will be automatically retired in 3 days:
    {{ComplianceIssues}}
    
    If your device remains noncompliant, it will be retired from management and wiped.
    
    For assistance, contact IT Support.
    ```

You have successfully created notification message templates for compliance actions.

### Task 2 - Create a Windows compliance policy

1. You are in the **Microsoft Intune admin center**.

1. In the left navigation pane, go to the Devices page and then expand **Manage devices** and select **Compliance**.

1. Select the **Policies** tab.

1. Select **+ Create policy**.

1. On the **Create a policy** pane:
    - **Platform**: Windows 10 and later
    - **Profile type**: Windows 10/11 compliance policy

1. Select **Create**.

1. On the **Basics** page:
    - **Name**: `Windows Compliance - Security Requirements`
    - **Description**: `Defines minimum security requirements for Windows devices including BitLocker, Secure Boot, firewall, and antivirus`

1. Select **Next**.

1. On the **Compliance settings** page, expand and configure the following sections:

    **Device Health**:
    - **BitLocker**: Require
    - **Secure Boot**: Require
    - **Code integrity**: Not configured

    **Device Properties**:
    - **Minimum OS version**: 10.0.19041 (Windows 10 20H1 or Windows 11)

    **System Security**:
    - **Require a password to unlock mobile devices**: Require
    - **Simple passwords**: Block
    - **Password type**: Alphanumeric
    - **Password complexity**: require digits, lowercase, uppercase, and special characters
    - **Minimum password length**: 8
    - **Maximum minutes of inactivity before password is required**: 15
    - **Password expiration (days)**: 90
    - **Number of previous passwords to prevent reuse**: 5
    - **Require encryption of data storage on device**: Require
    - **Require password when device returns from idle state**: Require
    - **Firewall**: Require
    - **Antivirus**: Require
    - **Antispyware**: Require
    - **Microsoft Defender Antimalware**: Require
    - **Microsoft Defender Antimalware minimum version**: Leave blank
    - **Microsoft Defender Antimalware security intelligence up-to-date**: Require

1. Select **Next**.

1. On the **Actions for noncompliance** page, review the default action:
    - **Action**: Mark device noncompliant
    - **Schedule (days after noncompliance)**: 0 (immediately)

1. Select the dropdown below the **default** action to add additional actions:
    - **Action**: Send email to end user
    - **Schedule**: 3 days after noncompliance
    - **Message template**: Select **Device Non-Compliance Notification**

1. Add another action:
    - **Action**: Send email to end user
    - **Schedule**: 27 days after noncompliance
    - **Message template**: Select **Device Retirement Warning**

1. Add another action:
    - **Action**: Retire the noncompliant device
    - **Schedule**: 30 days after noncompliance

    > [!NOTE]
    > This gives users 30 days to remediate compliance issues before the device is retired (unenrolled) from Intune.

1. Select **Next**.

1. On the **Assignments** page, under **Included groups**, select **+ Add groups**.

1. Select **All Windows Devices**.

1. On the **Review + create** page, review your configuration and select **Create**.

You have successfully created a compliance policy that enforces security requirements on Windows devices.

### Task 3 - Monitor compliance policy deployment

1. After creating the policy, you are returned to the **Compliance policies** list.

1. Select the **Windows Compliance - Security Requirements** policy.

1. On the policy overview page, review:
    - **Assignment status**: Number of assigned devices
    - **Device compliance status**: Compliant, Not compliant, Other, Total

    > [!NOTE]
    > Compliance evaluation occurs every 24 hours or when a device syncs. Initial evaluation can take several hours.

1. Select **View Report** to see per-device compliance results.

1. If devices show "Error" or "Not evaluated," wait for the next sync or manually sync devices from the device details page.

1. Leave the browser window open for the next exercise.

## Exercise 3: Use filters to target policies

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will create a filter to target policies to specific devices based on device properties like ownership.

### Task 1 - Create a device filter for corporate-owned devices

1. You are in the **Microsoft Intune admin center**.

1. In the left navigation pane, expand **Tenant administration** and select **Assignment filters**.

1. Select **+ Create** → **Managed devices**.

1. On the **Basics** page:
    - **Filter name**: `Corporate-Owned Devices Only`
    - **Description**: `Filter to include only corporate-owned devices`
    - **Platform**: Windows and later

1. Select **Next**.

1. On the **Rules** page, configure the rule:
    - **Property**: Select **deviceOwnership**
    - **Operator**: Select **Equals**
    - **Value**: Select **Corporate**

1. The rule syntax should display: `(device.deviceOwnership -eq "Corporate")`

1. Select **Preview devices** to see which devices match this filter (optional), and you'll notice the list is empty.

1. Select **Next**.

1. On the **Review + create** page, review and select **Create**.

You have successfully created a device filter for corporate-owned devices.

### Task 2 - Mark devices as corporate vs. personal

In this task, you will manually mark one device as corporate-owned and one as personal to test the filter.

1. Navigate to **Devices** → **All devices**.

1. Select **SEA-WS1** from the device list.

1. On the device overview page, select **Properties** in the left menu.

1. Change the **Ownership** field:
    - **Ownership**: **Corporate**

1. Check the box at the bottom that says **I acknowledge that I understand the results of this ownership change**

1. Select **Save** at the top.

    > [!NOTE]
    > SEA-WS1 is now marked as corporate-owned and SEA-WS2 is already set as personal. The filter will target only SEA-WS1.

You have successfully configured device ownership for filter testing.

### Task 3 - Apply filter to a configuration profile

1. Navigate to **Devices** → **Configuration** → **Policies**.

1. Select the **Windows Security Settings - Corporate Devices** profile created earlier.

1. Under **Assignments**, select **Edit**.

1. Under the **All Windows Devices** group assignment, you should see an option to **Edit filter**:
    
1. In the **Assignment filters** pane, choose **Include filtered devices in assignment**
    - Search for the filter you just create and choose **Corporate-Owned Devices Only**

1. Select **Review + save** and then **Save**.

    > [!TIP]
    > The policy now applies only to SEA-WS1 (corporate-owned). SEA-WS2 (personal) is excluded even though it's in the "All Windows Devices" group.

1. Leave the browser window open for the next exercise.

## Exercise 4: Validate policy application

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this exercise, you will validate that policies are applied to your enrolled device and review compliance status.

### Task 1 - Sync devices and check configuration profile status

1. In the **Microsoft Intune admin center**, navigate to **Devices** → **All devices**.

1. Select **SEA-WS1** (corporate-owned device).

1. At the top of the device page, select **Sync** to force an immediate policy check-in.

1. Wait for the sync to complete (30-60 seconds).

1. In the left menu, select **Device configuration**.

1. On the **Device configuration** page, you should see:
    - **Windows Security Settings - Corporate Devices**: Status = Succeeded, Pending, or Error

    > [!NOTE]
    > If status is "Pending," the device is still processing the policy. Wait 5-10 minutes and check again. If status is "Error," select the profile to see detailed error messages.

1. Go back to **All devices** and select **SEA-WS2** (personal device).

1. Select **Sync** to refresh the device.

1. In the left menu, select **Device configuration**.

1. Verify that the **Windows Security Settings - Corporate Devices** profile does **NOT** appear for SEA-WS2.

    > [!TIP]
    > This confirms the filter is working correctly - the policy only applies to corporate-owned devices (SEA-WS1), not personal devices (SEA-WS2).

1. Leave the browser window open for the next task.

### Task 2 - Check device compliance status

1. You are still viewing your enrolled device in the **Microsoft Intune admin center**.

1. In the left menu, select **Manage devices** and then **Compliance**.

1. Select the **Windows Compliance - Security Requirements** policy.

1. Select  **Per-setting status** under **Additional monitoring reports**.

1. Review the list of devices and note which settings failed. You would remediate these on the device to bring it into compliance.
    - Notice that two devices are noncompliant with the **BitLocker** setting.

1. Leave the browser window open.

## Lab Completion

Congratulations! You have successfully completed Lab 03: Implement policy layering and compliance.

### Summary of what you accomplished

In this lab, you:
- ✅ Created a Settings Catalog configuration profile to enforce BitLocker encryption
- ✅ Assigned the configuration profile to the "All Windows Devices" dynamic group
- ✅ Created a compliance policy defining security requirements (BitLocker, Secure Boot, firewall, password, antivirus)
- ✅ Configured actions for noncompliance (mark noncompliant, send email, retire device)
- ✅ Created a device filter to target corporate-owned devices only
- ✅ Marked SEA-WS1 as corporate and SEA-WS2 as personal for filter testing
- ✅ Applied the filter to a configuration profile to exclude personal devices
- ✅ Validated configuration profile deployment status on both devices
- ✅ Verified the filter correctly excluded SEA-WS2 from the policy
- ✅ Checked device compliance status and reviewed compliance evaluation results

### Next steps

In **Lab 04: Protect data with MAM and conditional access**, you will:
- Create app protection policies (MAM) for mobile apps
- Configure conditional access policies to enforce device compliance
- Test data protection and access control on mobile and desktop devices

---

**Lab Status**: ✅ Complete  
**Next Lab**: Lab 04 - Protect data with MAM and conditional access  
**Estimated Time for Next Lab**: 30 minutes
