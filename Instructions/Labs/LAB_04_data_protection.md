---
lab:
  title: 'Lab 04: Protect data with MAM and conditional access'
  type: Answer Key
  module: 'Module 04: Protect data and control access with Microsoft Intune and Conditional Access'
  description: In this lab, you will create Mobile Application Management (MAM) policies to protect corporate data in apps on managed and unmanaged devices, configure conditional access policies to enforce device compliance requirements for accessing corporate resources, and test data protection and access control scenarios.
  duration: 30 minutes
  level: 300
  islab: true
---

# Lab 04: Protect data with MAM and conditional access
# Student lab answer key

> **Abstract:**  
> In this lab, you will create Mobile Application Management (MAM) policies to protect corporate data in apps on managed and unmanaged devices, configure conditional access policies to enforce device compliance requirements for accessing corporate resources, and test data protection and access control scenarios.

## Lab scenario

Continuing as **Diego Siciliani**, Contoso Healthcare's Modern Endpoint Administrator, you have successfully configured device policies and compliance in Lab 03. Now you need to protect corporate data in Microsoft 365 apps and enforce access controls based on device compliance.

In this lab, you will create app protection policies (MAM) to prevent data leakage from mobile apps, configure conditional access policies that require compliant devices to access Exchange Online, and test these policies on mobile and desktop devices to ensure data protection and access control are working as expected.

## Lab Duration

  - **Estimated Time to complete**: 30 minutes

## Instructions

### Before You Begin

> [!IMPORTANT]
> **Prerequisites**: You must complete **Lab 01-03** before starting this lab.

> [!IMPORTANT]
> **Administrative Account**: Continue using **Diego Siciliani's** account (DiegoS@yourtenant.onmicrosoft.com) for all administrative tasks. Diego has the **Intune Administrator** and **Conditional Access Administrator** roles from Lab 01, which provide the necessary permissions for app protection and conditional access policies.

> [!NOTE]
> **Optional**: For full testing, you will need an iOS or Android device with Microsoft Outlook, Teams, or OneDrive installed. If you don't have a mobile device, you can still complete most tasks using your Windows device.

## Exercise 1: Create app protection policies (MAM)

### Exercise Duration

  - **Estimated Time to complete**: 15 minutes

In this exercise, you will create Mobile Application Management (MAM) policies to protect corporate data in Microsoft 365 apps on iOS and Android devices. You will configure data transfer restrictions, encryption requirements, and access controls to prevent data leakage on mobile devices.

> [!NOTE]
> **What about Windows?** Windows does not support MAM/App Protection Policies like iOS and Android. Windows devices must be enrolled (MDM) to apply data protection policies. Windows Information Protection (WIP) was deprecated by Microsoft and is no longer recommended.

### Task 1 - Create an iOS/iPadOS app protection policy

In this task, you will create an app protection policy for iOS/iPadOS devices to secure Microsoft 365 apps.

1. Navigate to the **Microsoft Intune admin center** at [**https://intune.microsoft.com**](https://intune.microsoft.com/).

1. Sign in with **Diego Siciliani's** credentials (DiegoS@yourtenant.onmicrosoft.com) if prompted.

    > [!NOTE]
    > Diego has the **Intune Administrator** and **Conditional Access Administrator** roles from Lab 01, which provide the necessary permissions for app protection and conditional access policies.

1. In the left navigation pane, select **Apps**.

1. On the **Apps | Overview** page, under **Manage apps**, select **Protection**.

1. On the **Apps | Protection** page, select **+ Create** and then select **iOS/iPadOS**.

1. On the **Basics** tab, configure the following and select **Next**:
    - **Name**: `iOS App Protection - Corporate Data`
    - **Description**: `Protects corporate data in Microsoft 365 apps on iOS/iPadOS devices - prevents data leakage and unauthorized access`

1. On the **Apps** tab, select **+ Select public apps**.

1. On the **Select apps to target** page, in the search box, type **Microsoft** to filter the app list.

1. Select the following apps by clicking the checkbox next to each:
    - **Microsoft Outlook**
    - **Microsoft Teams**
    - **Microsoft OneDrive**
    - **Microsoft Word**
    - **Microsoft Excel**
    - **Microsoft PowerPoint**
    - **Microsoft 365 Copilot**

1. Select **Select** at the bottom of the page.

1. Verify the selected apps are listed and then select **Next**.

1. On the **Data protection** tab, configure the following settings:

    **Data Transfer**:
    - **Backup org data to iTunes and iCloud backups**: **Block**
    - **Send org data to other apps**: **Policy managed apps**
    - **Receive data from other apps**: **Policy managed apps**
    - **Save copies of org data**: **Block**
    - **Allow user to save copies to selected services**: Select **OneDrive for Business** and **SharePoint**
    - **Restrict cut, copy, and paste between other apps**: **Policy managed apps with paste in**
    - **Third party keyboards**: **Block**

    **Encryption**:
    - **Encrypt org data**: **Require**

    **Functionality**:
    - **Printing org data**: **Block**
    - **Restrict web content transfer with other apps**: **Microsoft Edge**
    - **Screen capture**: **Block**

1. Select **Next**.

1. On the **Access requirements** tab, configure the following settings:

    - **PIN for access**: **Require**
    - **PIN type**: **Numeric**
    - **Simple PIN**: **Block**
    - **Select minimum PIN length**: **6**
    - **Touch ID instead of PIN for access (iOS 8+/iPadOS)**: **Allow**
    - **Override biometrics with PIN after timeout**: **Require**
    - **Timeout (minutes of inactivity)**: **30**
    - **Work or school account credentials for access**: **Require**
    - **Recheck the access requirements after (minutes of inactivity)**: **30**

1. Select **Next**.

1. On the **Conditional launch** tab, review the default settings:
    - **Max PIN attempts**: 5 (Action: **Reset PIN**)
    - **Offline grace period**: 720 minutes (Action: **Block access**)
    - **Offline grace period**: 90 days (Action: **Wipe data**)
    - **Jailbroken/rooted devices**: (Action: **Block access**)

1. Select **Next**.

1. On the **Assignments** tab, configure:
    - Under **Included groups**, select **+ Add groups**
    - Search for and select **Device Management Pilot Users** (created in Lab 01)
    - Select **Select**

1. Select **Next**.

1. On the **Review + create** page, review all your settings carefully.

1. Select **Create** to create the policy.

You have successfully created an iOS/iPadOS app protection policy.

### Task 2 - Create an Android app protection policy

In this task, you will create an app protection policy for Android devices with similar settings to iOS to ensure consistent data protection across mobile platforms.

1. You are still in the **Microsoft Intune admin center** → **Apps** → **Protection**.

1. Select **+ Create policy** and then select **Android**.

1. On the **Basics** tab, configure the following and select **Next**:
    - **Name**: `Android App Protection - Corporate Data`
    - **Description**: `Protects corporate data in Microsoft 365 apps on Android devices - prevents data leakage and unauthorized access`

1. On the **Apps** tab, select **+ Select public apps**.

1. In the search box, type **Microsoft** and select the same apps as iOS:
    - **Microsoft Outlook**
    - **Microsoft Teams**
    - **Microsoft OneDrive**
    - **Microsoft Word**
    - **Microsoft Excel**
    - **Microsoft PowerPoint**
    - **Microsoft 365 Copilot**

1. Select **Select** and then **Next**.

1. On the **Data protection** tab, configure settings similar to iOS:

    **Data Transfer**:
    - **Backup org data to Android backup services**: **Block**
    - **Send org data to other apps**: **Policy managed apps**
    - **Receive data from other apps**: **Policy managed apps**
    - **Save copies of org data**: **Block**
    - **Allow user to save copies to selected services**: Select **OneDrive for Business** and **SharePoint**
    - **Restrict cut, copy, and paste between other apps**: **Policy managed apps with paste in**
    - **Screen capture and Google Assistant**: **Block** 
    - **Approved keyboards**: **Not required**

    **Encryption**:
    - **Encrypt org data**: **Require**
    - **Encrypt org data on enrolled devices**: **Require**

    **Functionality**:
    - **Sync policy managed app data with native apps or add-ins**: **Block**
    - **Printing org data**: **Block**
    - **Restrict web content transfer with other apps**: **Microsoft Edge**
    - **Start Microsoft Tunnel connection on app-launch**: **No**

1. Select **Next**.

1. On the **Access requirements** tab, configure the same settings as iOS:
    - PIN: **Require**, **Numeric**, minimum **6** digits, **Block** simple PIN
    - Biometric: **Allow**
    - Override biometrics after **30** minutes
    - Credentials: **Require**
    - Recheck after: **30** minutes

1. Select **Next**.

1. On the **Conditional launch** tab, accept the default settings (same as iOS).

1. Select **Next**.

1. On the **Assignments** tab, assign to **Device Management Pilot Users**.

1. Select **Next** and then **Create**.

You have successfully created app protection policies for both iOS and Android devices, ensuring consistent data protection across mobile platforms.

## Exercise 2: Create conditional access policies

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will create a conditional access policy that requires devices to be compliant before accessing Exchange Online (Outlook).

### Task 1 - Create a conditional access policy requiring compliant devices

1. Open a new browser tab and navigate to the **Microsoft Entra admin center** at [**https://entra.microsoft.com**](https://entra.microsoft.com/).

1. In the left navigation pane, expand **Entra ID** and select **Conditional Access**.

1. Select **Policies** and then **+ New policy**.

1. On the **New Conditional Access policy** page:

    **Name**: `Require compliant device for Exchange Online`

    **Assignments**:
    - **Users**: Select **All users** (or select specific pilot group)

    > [!TIP]
    > **Understanding Policy Exclusions**: While this lab applies the policy to all users, in production environments you may need to exclude certain service accounts such as Microsoft Teams Rooms devices, conference room resource accounts, or automated service principals that cannot support MFA or device compliance. Always document exclusions with business justification and review them regularly as part of your security posture management.

    **Target resources**:
    - **Select what this policy applies to**: Cloud apps
    - **Include**: Select **Select apps**
    - Search for and select: **Office 365 Exchange Online**

    **Conditions**:
    - **Device platforms**: Not configured (applies to all platforms)
    - **Client apps**: Not configured (applies to all apps)

    **Access controls**:
    - **Grant**: Select **Grant access**
    - Check: **Require device to be marked as compliant**

    **Enable policy**: Report-only (for initial testing)

1. Select **Create**.

    > [!NOTE]
    > "Report-only" mode allows you to test the policy without blocking users. You can review sign-in logs to see how the policy would behave before enforcing it.

You have successfully created a conditional access policy requiring compliant devices for Exchange Online access.

### Task 2 - Test conditional access policy in report-only mode

> [!NOTE]
> The **Insights and reporting** workbook requires a Log Analytics workspace and Security Reader role, which may not be available in this lab environment. You will use sign-in logs to verify policy behavior instead.

1. You are still in the **Microsoft Entra admin center**.

1. In the left navigation pane, expand **Entra ID** → **Monitoring & health** and select **Sign-in logs**.

1. After a pilot user signs in, locate their sign-in entry in the logs.

1. Select the sign-in entry to view details, then select the **Conditional Access** tab.

1. Review the policy evaluation results:
    - **Policy name**: `Require compliant device for Exchange Online`
    - **Result**: **Report-only: Failure** or **Report-only: Success** (depending on device compliance)

    > [!NOTE]
    > In report-only mode, the policy evaluates but does not enforce. "Report-only: Failure" means the policy *would have* blocked access if enforced.

1. If satisfied with the policy behavior, return to **Entra ID** → **Conditional Access** → **Policies**, select the policy, and change **Enable policy** from **Report-only** to **On** to enforce it.

1. Leave the browser window open for the next exercise.

## Exercise 3: Test data protection and access control

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this exercise, you will test app protection policies on a mobile device and conditional access policies on a desktop device.

### Task 1 - Test app protection policy on mobile device (optional)

> [!NOTE]
> This task requires an iOS or Android device. If you don't have one, you can skip to Task 2.

1. On your **iOS or Android device**, install **Microsoft Outlook** from the App Store (iOS) or Play Store (Android).

1. Open the Outlook app.

1. Sign in with one of your **pilot user accounts** (e.g., AlexW@yourtenant.onmicrosoft.com).

1. You should be prompted to **set up a PIN** (6 digits) as required by the app protection policy.

1. After setting the PIN, you are signed into Outlook and can view your email.

1. Try the following to test data protection:
    - **Screenshot**: Try to take a screenshot of an email → Should be blocked with a message: "Your organization doesn't allow screen captures"
    - **Copy/Paste**: Try to copy email text and paste into an unmanaged app (like Notes) → Should be blocked or show warning
    - **Print**: Try to print an email → Should be blocked
    - **Save attachment**: Try to save an email attachment → Should only allow saving to OneDrive for Business, not local storage

1. Close the Outlook app and reopen it after 30 minutes → You should be prompted to re-enter your PIN or use biometrics.

You have successfully tested the app protection policy on a mobile device.

### Task 2 - Test conditional access policy on compliant device (SEA-WS1)

1. On your **SEA-WS1** (corporate-owned, compliant device from Lab 03), open **Microsoft Edge**.

1. Navigate to **Outlook on the web**: [**https://outlook.office.com**](https://outlook.office.com).

1. Sign in with **Alex Wilber's** account (AlexW@yourtenant.onmicrosoft.com).

1. Since SEA-WS1 is **compliant** (from Lab 03), you should be **granted access** to Outlook on the web.

1. Verify you can:
    - Read emails
    - Send emails
    - Access calendar and contacts

    > [!TIP]
    > This demonstrates that compliant devices can access corporate resources protected by conditional access.

1. Leave Outlook on the web open.

You have successfully accessed Outlook on a compliant device.

### Task 3 - Test conditional access policy on noncompliant device (SEA-WS2)

In this task, you will test the conditional access policy using SEA-WS2, which should be blocked if it's not compliant.

1. On your **SEA-WS2** (personal device), open **Microsoft Edge**.

1. Navigate to **Outlook on the web**: [**https://outlook.office.com**](https://outlook.office.com).

1. Sign in with **Allan Deyoung's** account (AllanD@yourtenant.onmicrosoft.com).

1. If SEA-WS2 is **not compliant** (or not evaluated yet), you should see an error message:
    - "You can't get there from here"
    - "Your sign-in was successful, but your admin requires your device to be managed to access this resource"
    - "Your device must be managed by your organization to access this resource"
    - Option to enroll the device or contact your admin

    > [!NOTE]
    > If SEA-WS2 is compliant, access will be granted. To test the blocked scenario, you can temporarily make it noncompliant by disabling Windows Firewall or Defender on SEA-WS2, then syncing the device.

1. **Optional**: To force noncompliant state on SEA-WS2:
    - On SEA-WS2, open **Windows Security** → **Firewall & network protection**
    - Turn **off** the firewall for the active network profile
    - In the **Microsoft Intune admin center**, sync SEA-WS2 (Devices → All devices → SEA-WS2 → Sync)
    - Wait 5-10 minutes for compliance re-evaluation
    - Try accessing Outlook on the web again → Should now be blocked

1. **Restore compliance** (if you disabled firewall):
    - Re-enable Windows Firewall on SEA-WS2
    - Sync the device in Intune
    - Wait for compliance re-evaluation

You have successfully tested the conditional access policy on both compliant and noncompliant devices.

### Task 4 - Review sign-in logs for both devices

1. In the **Microsoft Entra admin center**, navigate to **Identity** → **Monitoring & health** → **Sign-in logs**.

1. Review recent sign-in events for both **Alex Wilber** and **Allan Deyoung**.

1. Select Alex Wilber's sign-in event (from SEA-WS1) to view details.

1. On the sign-in details page, select the **Conditional Access** tab.

1. Review the conditional access policy evaluation:
    - **Policy name**: Require compliant device for Exchange Online
    - **Result**: Success (device was compliant)
    - **Controls satisfied**: Require device to be marked as compliant ✅

1. Go back to the sign-in logs and select Allan Deyoung's sign-in event (from SEA-WS2).

1. On the sign-in details page, select the **Conditional Access** tab.

1. Review the policy evaluation:
    - **Policy name**: Require compliant device for Exchange Online
    - **Result**: Success (if compliant) or Failure (if noncompliant)
    - **Controls satisfied**: Require device to be marked as compliant (✅ or ❌)

1. Compare the two sign-in events to see how conditional access policies evaluate differently based on device compliance state.

    > [!TIP]
    > Sign-in logs are essential for troubleshooting conditional access policies. They show exactly why users are being granted or denied access, which policies applied, and which controls were evaluated.

You have successfully reviewed sign-in logs to understand conditional access policy enforcement across multiple devices.

## Lab Completion

Congratulations! You have successfully completed Lab 04: Protect data with MAM and conditional access.

### Summary of what you accomplished

In this lab, you:
- ✅ Created iOS app protection policy to protect corporate data in Microsoft 365 apps
- ✅ Configured data protection settings (block copy/paste, screen capture, printing, require encryption)
- ✅ Configured access requirements (PIN, biometrics, work credentials)
- ✅ Created Android app protection policy with similar protection settings
- ✅ Created conditional access policy requiring compliant devices for Exchange Online
- ✅ Tested app protection policy on mobile device (PIN enforcement, data protection)
- ✅ Tested conditional access policy on SEA-WS1 (compliant device - access granted)
- ✅ Tested conditional access policy on SEA-WS2 (noncompliant device - access blocked)
- ✅ Reviewed sign-in logs to understand conditional access policy evaluation across multiple devices

### Next steps

In **Lab 05: Harden devices with security baselines**, you will:
- Deploy Windows security baselines to enforce 100+ security settings
- Onboard devices to Microsoft Defender for Endpoint
- Configure Attack Surface Reduction (ASR) rules
- Monitor security posture and vulnerabilities

---

**Lab Status**: ✅ Complete  
**Next Lab**: Lab 05 - Harden devices with security baselines  
**Estimated Time for Next Lab**: 45 minutes
