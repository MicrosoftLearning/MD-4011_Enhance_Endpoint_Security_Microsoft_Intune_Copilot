---
lab:
  title: 'Lab 02: Enroll and validate devices'
  type: Answer Key
  module: 'Module 02: Enroll and validate devices with Microsoft Intune'
  description: In this lab, you will enroll a Windows 11 device into Microsoft Intune using Entra join, validate the enrollment in both the Entra ID and Intune portals, and verify device properties, compliance status, and group membership. You will also perform device synchronization from both the portal and the device itself.
  duration: 30 minutes
  level: 200
  islab: true
  primarytopics:
    - Windows
    - Windows 11
---

# Lab 02: Enroll and validate devices
# Student lab answer key

> **Abstract:**  
> In this lab, you will enroll a Windows 11 device into Microsoft Intune using Entra join, validate the enrollment in both the Entra ID and Intune portals, and verify device properties, compliance status, and group membership. You will also perform device synchronization from both the portal and the device itself.

## Lab scenario

Continuing your role as **Diego Sicilliani**, Contoso Healthcare's Modern Endpoint Administrator, you have successfully configured the Microsoft 365 tenant for device management in Lab 01. Now you are ready to begin enrolling devices into Intune.

For the pilot project, you will enroll a Windows 11 device using Entra join, which provides seamless single sign-on and automatic Intune enrollment. After enrollment, you will validate the device appears in both Entra ID and Intune portals, review device properties and compliance status, and verify that the device was automatically added to the "All Windows Devices" dynamic group you created in Lab 01.

## Lab Duration

  - **Estimated Time to complete**: 30 minutes

## Instructions

### Before You Begin

> [!IMPORTANT]
> **Prerequisites**: You must complete **Lab 01: Configure tenant for device management** before starting this lab. Lab 01 configured automatic MDM enrollment, which is required for devices to enroll in Intune.

> [!IMPORTANT]
> **Administrative Account**: Continue using **Diego Siciliani's** account (DiegoS@yourtenant.onmicrosoft.com) for all administrative tasks. In Lab 01, you assigned Diego the necessary roles (Intune Administrator, Cloud Device Administrator) and signed out of the Global Administrator account. Use Diego's account throughout this lab and all subsequent labs.

## Exercise 1: Enroll Windows device using Entra join

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will join a Windows 11 device to Entra ID, which will automatically trigger MDM enrollment in Intune (thanks to the automatic enrollment configuration you completed in Lab 01).

### Task 1 - Join Windows device to Entra ID

In this task, you will connect your Windows device to your work or school account using Entra join.

1. In the lab interface, open **SEA-WS1** and confirm that you are working in that workstation before continuing.

1. On **SEA-WS1**, open **Settings** by pressing **Windows key + I** (or right-click Start and select **Settings**).

1. In the Settings app, select **Accounts** from the left navigation pane.

1. Select **Access work or school**.

1. On the **Access work or school** page, you should see "No work or school accounts connected."

1. Select the **Connect** button.

1. On the **Set up a work or school account** window, enter **Alex Wilber's email address**: `AlexW@yourtenant.onmicrosoft.com`

    > [!IMPORTANT]
    > Use Alex Wilber for the first device (SEA-WS1). You will use Allan Deyoung for the second device in Exercise 3.

1. Select **Next**.

1. You will be redirected to the Microsoft sign-in page. Enter the **password** for the user account.

1. If prompted, complete **multi-factor authentication** (MFA) if it is enabled for your tenant.

1. On the **You're all set!** screen, review the message:
    - "Your device has been joined to your organization's network."
    - "Your organization might control some settings and apps on this device."

1. Select **Done**.

1. You are returned to the **Access work or school** page. You should now see a connection listed:
    - **Connected to [Your Organization]'s Entra ID**
    - User account: **AlexW@yourtenant.onmicrosoft.com**
    - Status: **Connected**

1. Below the connection, you may see an **Info** button. Select it to view connection details:
    - **Device state**: Entra ID joined
    - **Management**: Enrolled in MDM (Microsoft Intune)

    > [!NOTE]
    > If "Management" shows "Pending" or "Not enrolled," wait 1-2 minutes and refresh. Automatic MDM enrollment can take a moment to complete.

1. **Close** the Settings app.

    > [!TIP]
    > You may see a notification in the Windows taskbar: "Your organization is managing this device." This confirms Intune enrollment is active.

1. Leave the device powered on and connected to the internet.

You have successfully joined the Windows device to Entra ID and automatically enrolled it in Microsoft Intune.

> [!NOTE]
> This device will be referred to as **SEA-WS1** and is enrolled with **Alex Wilber's** account throughout the remaining labs.

## Exercise 2: Validate device enrollment in Entra ID

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this exercise, you will validate that the enrolled device appears in the Microsoft Entra admin center and review its properties.

### Task 1 - Locate enrolled device in Entra ID

In this task, you will find your newly enrolled device in the Entra ID device inventory.

1. Open **Microsoft Edge** and navigate to the **Microsoft Entra admin center** at [**https://entra.microsoft.com**](https://entra.microsoft.com/).

1. You are still signed in with **Diego Siciliani's** credentials (DiegoS@yourtenant.onmicrosoft.com).

    > [!NOTE]
    > You assigned Diego the **Intune Administrator** and **Cloud Device Administrator** roles in Lab 01. These roles provide the necessary permissions for device management tasks.

1. In the left navigation pane, expand **Entra ID** → **Devices** and select **All devices**.

1. On the **All devices** page, locate your newly enrolled device in the list.

    > [!NOTE]
    > If you don't see the device immediately, wait 2-3 minutes and refresh the page. Device registration can take a few moments to appear.

1. Select the **device name** to open the device details page.

1. Leave the browser window open for the next task.

You have successfully located the enrolled device in the Entra ID device inventory.

### Task 2 - Review device properties in Entra ID

In this task, you will review the device properties to understand how Entra ID tracks the device.

1. You are viewing the device details page in the **Microsoft Entra admin center**.

1. On the **Overview** tab, review the following device properties:

    | Property | Description |
    |----------|-------------|
    | **Name** | Device name (e.g., DESKTOP-ABC123) |
    | **Device ID** | Unique identifier assigned by Entra ID (GUID) |
    | **Object ID** | Entra ID object identifier (GUID) |
    | **Enabled** | Yes (device is active) |
    | **OS** | Windows 11 (or Windows 10) |
    | **Version** | Full OS version (e.g., 10.0.22621.0) |
    | **Join Type** | Should show **Azure AD Joined** ✅ |
    | **User principal name** | AlexW@yourtenant.onmicrosoft.com |
    | **MDM** | Microsoft Intune ✅ (confirms MDM enrollment) |
    | **Compliant** | Yes |
    | **Activity** | Timestamp of most recent device activity |

1. Leave the browser window open for the next exercise.

You have successfully reviewed device properties in the Microsoft Entra admin center and confirmed the device is Entra joined and enrolled in Intune.

## Exercise 3: Enroll second Windows device (SEA-WS2)

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will enroll a second Windows 11 device (SEA-WS2) into Intune using **Allan Deyoung's** account. This will allow you to test multi-device scenarios, user-based policy targeting, and assignment filters in later labs.

### Task 1 - Join SEA-WS2 to Entra ID with Allan Deyoung

In this task, you will join the second workstation to Entra ID using **Allan Deyoung's** account.

1. In the lab interface, switch from **SEA-WS1** to **SEA-WS2** using the available resource selector, workstation tab, or virtual-machine list. Confirm that **SEA-WS2** is selected.

1. On **SEA-WS2**, open **Settings** by pressing **Windows key + I**.

1. In the Settings app, select **Accounts** from the left navigation pane.

1. Select **Access work or school**.

1. On the **Access work or school** page, select the **Connect** button.

1. On the **Set up a work or school account** window, enter **Allan Deyoung's email address**: `AllanD@yourtenant.onmicrosoft.com`

    > [!IMPORTANT]
    > Use Allan Deyoung for the second device (SEA-WS2) to test multi-user scenarios in later labs.

1. Select **Next**.

1. Enter the **password** for **Allan Deyoung's** account.

1. If prompted, complete **multi-factor authentication** (MFA).

1. On the **You're all set!** screen, review the confirmation message.

1. Select **Done**.

1. Verify the connection shows:
    - **Connected to [Your Organization]'s Azure AD**
    - User account: `AllanD@yourtenant.onmicrosoft.com`
    - Status: **Connected**

1. Select the **Info** button and verify:
    - **Device state**: Azure AD joined
    - **Management**: Enrolled in MDM (Microsoft Intune)

1. **Close** the Settings app.

You have successfully enrolled SEA-WS2 with Allan Deyoung's account. You now have two enrolled devices for testing multi-device scenarios.

### Task 2 - Verify both devices in Intune admin center

In this task, you will confirm both devices appear in the Intune device inventory.

1. In the lab interface, switch back to **SEA-WS1** and confirm that workstation is selected.

1. On **SEA-WS1**, navigate to the **Microsoft Intune admin center** at [**https://intune.microsoft.com**](https://intune.microsoft.com/).

1. In the left navigation pane, expand **Devices** and select **All devices**.

1. On the **All devices** page, verify you now see **two enrolled devices**:
    - **SEA-WS1** (enrolled by AlexW@...)
    - **SEA-WS2** (enrolled by AllanD@...)

1. Select **SEA-WS2** to view its device details.

1. On the Overview tab, verify:
    - **Primary user**: Allan Deyoung
    - **Operating System**: Windows
    - **Compliance state**: Not evaluated (no policies assigned yet)
    - **Last check-in**: Recent timestamp

1. In the left menu, select **Group membership**.

1. Verify SEA-WS2 is also a member of the **All Windows Devices** dynamic group.

1. Leave the browser window open for the next exercise.

You have successfully enrolled two devices with different users, setting up the foundation for multi-device policy testing in upcoming labs.

## Exercise 4: Perform device synchronization

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this exercise, you will manually trigger device synchronization from both the Intune portal and the Windows device to force the device to check in with Intune immediately.

### Task 1 - Sync device from Intune portal

In this task, you will initiate a manual sync from the Intune admin center.

1. In the left navigation pane, expand **Devices** and select **All devices**.

1. Select **SEA-WS1** to open its device details page.

1. At the top of the device details page, locate the toolbar with device actions.

1. Select **Sync** (or the ellipsis **...** → **Sync** if the button is collapsed).

1. A confirmation message appears: **"Sync intiated."**

1. The device will receive a notification to check in with Intune immediately (instead of waiting for the scheduled 8-hour sync interval).

1. Note the **Last check-in** timestamp on the device overview page. After 1-2 minutes, refresh the page and the timestamp should update to show the recent sync.

    > [!NOTE]
    > Manual sync is useful for testing policy deployment or forcing immediate compliance evaluation.

1. Leave the browser window open for the next task.

You have successfully triggered a manual sync from the Intune admin center.

### Task 2 - Sync device from Windows Settings (optional)

In this task, you will initiate a sync from the Windows device itself.

1. On your **enrolled Windows 11 device**, open **Settings** (Windows key + I).

1. Select **Accounts** → **Access work or school**.

1. Select your work or school account connection (e.g., **Connected to [Your Organization]'s Azure AD**).

1. Select the **Info** button.

1. On the **Managed by [Your Organization]** page, scroll down to the **Device sync status** section.

1. Review the sync information:
    - **Last sync**: Timestamp of most recent sync
    - **Sync status**: Success or In progress

1. Select the **Sync** button.

1. A sync operation begins. You should see:
    - "Sync is in progress"
    - After 10-30 seconds: "Sync completed successfully"

1. The **Last sync** timestamp updates to show the current time.

1. Close the Settings app.

    > [!TIP]
    > Users can manually sync their devices to receive policy updates immediately. This is helpful when troubleshooting policy deployment issues.

You have successfully initiated a manual sync from the Windows device.

## Lab Completion

Congratulations! You have successfully completed Lab 02: Enroll and validate devices.

### Summary of what you accomplished

In this lab, you:
- ✅ Joined a Windows 11 device (SEA-WS1) to Entra ID using "Access work or school" with **Alex Wilber's** account
- ✅ Automatically enrolled SEA-WS1 in Microsoft Intune via automatic MDM enrollment
- ✅ Enrolled a second device (SEA-WS2) with **Allan Deyoung's** account
- ✅ Located and viewed both devices in Microsoft Entra admin center
- ✅ Reviewed device properties in Entra ID (join type, OS, owner, MDM status)
- ✅ Located and viewed both devices in Microsoft Intune admin center
- ✅ Reviewed device overview, properties, compliance status, and configuration profiles
- ✅ Verified both devices were automatically added to the "All Windows Devices" dynamic group
- ✅ Performed manual device synchronization from both the Intune portal and the device
