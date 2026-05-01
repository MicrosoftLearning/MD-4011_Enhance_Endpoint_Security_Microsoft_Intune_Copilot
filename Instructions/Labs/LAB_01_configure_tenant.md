---
lab:
  title: 'Lab 01: Configure tenant for device management'
  type: Answer Key
  module: 'Module 01: Prepare Microsoft Entra ID and Intune for device management'
  description: In this lab, you will configure the foundational Microsoft Intune environment for Contoso Healthcare, including licensing, user accounts, permissions, and Entra ID settings to support device management. The scenario guides you through preparing the tenant for device enrollment by setting up automatic MDM enrollment, creating dynamic device groups, and verifying Intune tenant status.
  duration: 38 minutes
  level: 200
  islab: true
  primarytopics:
    - Microsoft Intune
---

# Lab 01: Configure tenant for device management
# Student lab answer key

> **Abstract:**  
> In this lab, you will configure the foundational Microsoft Intune environment for Contoso Healthcare, including licensing, user accounts, permissions, and Entra ID settings to support device management. The scenario guides you through preparing the tenant for device enrollment by setting up automatic MDM enrollment, creating dynamic device groups, and verifying Intune tenant status.

## Lab scenario

In the labs for this course, you are taking on the role of **Deigo Sicilliani**, Contoso Healthcare's Modern Endpoint Administrator. Contoso Healthcare is a mid-sized healthcare organization that has deployed Microsoft 365 E5 and is now ready to implement modern endpoint management with Microsoft Intune.

You have been tasked with completing a pilot project that tests device management, security, and compliance features in Microsoft Intune as they relate to Contoso's healthcare industry requirements. The organization needs to ensure all endpoints are secure, compliant, and meet regulatory requirements while maintaining user productivity.

You have just started the pilot project. In this first lab, you will prepare the Microsoft 365 tenant for device management by verifying licenses, configuring Entra ID for automatic device enrollment, creating organizational groups, and validating Intune tenant readiness. These foundational configurations will enable device enrollment and policy management in subsequent labs.

## Lab Duration

  - **Estimated Time to complete**: 38 minutes

## Instructions

### Before You Begin - Administrative roles and zero-trust principles

> [!IMPORTANT]
> **Zero-Trust and Least Privilege**: Following security best practices, you will assign specific administrative roles and use those throughout all labs rather than Global Administrator. This demonstrates proper role-based access control (RBAC) as recommended by Microsoft.

> [!NOTE]
> **Roles you will assign and use**:
> - **Intune Administrator**: For managing devices, policies, and apps in Intune
> - **Cloud Device Administrator**: For managing device settings in Entra ID
> - **Groups Administrator**: For creating and managing groups in Entra ID
> - **Conditional Access Administrator**: For creating conditional access policies (Lab 04)
> - **Security Administrator**: For Microsoft Defender for Endpoint and security baselines (Lab 05)
> 
> In Exercise 1, you will assign these roles to **Diego Siciliani** who will serve as the Intune administrator for all labs.

### WWL Tenants - Terms of Use

> [!IMPORTANT]
> If you are being provided with a tenant as a part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training.
> 
> Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and is not eligible for extension.
> 
> Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time.

## Exercise 1: Verify licensing and identify pilot users

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will verify that the Microsoft 365 tenant has the appropriate licenses for Intune device management and confirm that licenses are already assigned to the four pilot users who will participate in testing throughout all labs.

> [!NOTE]
> You will use **Global Administrator** credentials for this exercise to access billing and licensing information. After verifying licenses, you will assign administrative roles to Diego Siciliani in Exercise 2.

### Task 1 - Sign in to Microsoft 365 admin center

In this task, you will sign in with Global Administrator to review licensing.

1. Open **Microsoft Edge** and browse to the **Microsoft 365 admin center** at [**https://admin.microsoft.com**](https://admin.microsoft.com/).

1. On the **Sign in** screen, enter the credentials of your **Global Administrator** account (or the MOD Administrator account provided in your lab environment).

1. If prompted, complete multi-factor authentication (MFA).

1. On the **Stay signed in?** prompt, select **No**.

1. In the left navigation pane, expand **Billing** and select **Licenses**.

1. Review the available licenses in your tenant. You should see the following licenses:
    - **Microsoft 365 E5 (no Teams)**
    - **Microsoft Power Apps for Developer**
    - **Microsoft Teams Enterprise**

1. Note the **Total licenses** and **Available licenses** for each subscription.

1. Leave the browser window open for the next task.

You have successfully reviewed the licensing status of your Microsoft 365 tenant and confirmed Intune licensing is available.

### Task 2 - Verify licenses are assigned to pilot users

In this task, you will verify that Intune/EMS licenses are already assigned to the four specific users who will participate in the device management pilot.

1. You are still signed in to the **Microsoft 365 admin center** as **Global Administrator**.

1. In the left navigation pane, expand **Users** and select **Active users**.

1. Review the list of users. You should see several precreated users.

1. Locate and note the following **four specific pilot users**:
    - **Alex Wilber**
    - **Allan Deyoung**
    - **Diego Siciliani**
    - **Joni Sherman**

    > [!IMPORTANT]
    > These four users will be used consistently throughout all labs. Make note of their names and email addresses.

1. Select **Alex Wilber** from the user list to view their details.

1. In the user details pane, select **Licenses and apps**.

1. Verify that Alex Wilber has **all three** of the following licenses assigned:
    - ✅ **Microsoft 365 E5 (no Teams)**
    - ✅ **Microsoft Power Apps for Developer**
    - ✅ **Microsoft Teams Enterprise**

1. Expand the **Microsoft 365 E5 (no Teams)** license details and verify the following services are enabled:
    - ✅ **Microsoft Intune**
    - ✅ **Microsoft Entra ID P2**

1. Close the user details pane.

    > [!NOTE]
    > All four pilot users should have the same three licenses assigned. If any user is missing licenses, notify your instructor.

1. Leave the browser window open for the next exercise.

You have successfully verified that Intune/EMS licenses are assigned to all four pilot users, enabling them to enroll devices and access Intune services.

## Exercise 2: Assign administrative roles (Zero-Trust)

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will assign the necessary administrative roles to **Diego Siciliani**, who will serve as the Intune administrator for all labs. Following zero-trust and least privilege principles, Diego will have specific roles rather than Global Administrator access.

### Task 1 - Navigate to Entra admin center

In this task, you will navigate to the Entra admin center to assign roles.

1. You should still be signed in as **Global Administrator** from Exercise 1.

1. Open a new browser tab and navigate to the **Microsoft Entra admin center** at [**https://entra.microsoft.com**](https://entra.microsoft.com/).

1. If prompted to sign in, use the same **Global Administrator** credentials.

You are now ready to assign administrative roles.

### Task 2 - Assign administrative roles to Diego Siciliani

In this task, you will assign the necessary Intune and security administrative roles to Diego Siciliani.

1. In the **Microsoft Entra admin center**, expand **Entra ID** and select **Users** → **All users**.

1. In the user list, search for and select **Diego Siciliani**.

1. In Diego's user profile, select **Assigned roles** in the left navigation.

1. At the top of the page, select **+ Add assignments**.

1. In the **Add assignments** pane, search for and select the following roles one-by-one and then select **Next**:
    - **Intune Administrator**
    - **Cloud Device Administrator**
    - **Groups Administrator**
    - **Conditional Access Administrator**
    - **Security Administrator**

1. On the **Setting** tab, ensure **Active** is selected under **Assignment type** (default).

1. Enter the following as business justification:

    ```text
    We're using Active assignments so Diego has immediate access throughout all labs. Eligible assignments would require activation through Privileged Identity Management (PIM) each time, which adds unnecessary complexity for a training environment.
    ```

1. Select **Assign** to assign the selected role.

1. Repeat for all the other roles mentioned.

1. Verify that all five roles now appear in Diego's **Assigned roles** list:
    - ✅ Intune Administrator
    - ✅ Cloud Device Administrator
    - ✅ Groups Administrator
    - ✅ Conditional Access Administrator
    - ✅ Security Administrator

    > [!IMPORTANT]
    > Diego Siciliani will be your administrative account for all remaining labs. Make note of his credentials.

1. Leave the browser window open.

You have successfully assigned administrative roles to Diego Siciliani following least privilege principles.

### Task 3 - Sign out and sign in as Diego Siciliani

In this task, you will sign out of the Global Administrator account and sign in with Diego Siciliani's account to begin using proper role-based access.

1. In the **Microsoft Entra admin center**, select your account name or profile icon in the upper-right corner.

1. Select **Sign out**.

1. Close all browser windows completely to clear the session.

1. Open a new **Microsoft Edge** window.

1. Navigate to the **Microsoft 365 admin center** at [**https://admin.microsoft.com**](https://admin.microsoft.com/).

1. On the **Sign in** screen, enter **Diego Siciliani's** email address: `DiegoS@yourtenant.onmicrosoft.com`

1. Enter Diego's password.

1. If prompted, complete multi-factor authentication (MFA).

1. On the **Stay signed in?** prompt, select **Yes** (you'll use Diego's account throughout all labs).

    > [!IMPORTANT]
    > From this point forward, all lab exercises will use **Diego Siciliani's** account unless explicitly stated otherwise. Do not use Global Administrator again.

1. Leave the browser window open for the next exercise.

You have successfully signed in with Diego Siciliani's role-based administrative account. This account will be used for all remaining lab exercises.

## Exercise 3: Configure Entra ID for device management

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will configure Microsoft Entra ID (formerly Azure Active Directory) settings to enable device join, device registration, and automatic Mobile Device Management (MDM) enrollment.

### Task 1 - Configure device join and registration settings

In this task, you will configure Entra ID to allow users to join and register their devices.

1. You should still be signed in to the **Microsoft Entra admin center** as **Diego Siciliani** from Exercise 2.

1. If needed, navigate to [**https://entra.microsoft.com**](https://entra.microsoft.com/).

1. In the left navigation pane, expand **Entra ID** → **Devices** and select **Overview**.

1. Review the current device statistics (you will see 0 devices at this point).

1. In the **Devices** menu, select **Device settings**.

1. On the **Device settings** page, configure the following:

    | Setting | Value |
    |---------|-------|
    | **Users may join devices to Microsoft Entra** | **All** |
    | **Users may register their devices with Microsoft Entra** | **All** |
    | **Require Multi-Factor Authentication to register or join devices with Microsoft Entra** | **No** (for lab purposes; enable in production) |
    | **Maximum number of devices per user** | **50** (default; adjust based on your requirements) |
    | **Global administrator role is added as local administrator on the device during Microsoft Entra join** | **Yes** (default) |
    | **Registering user is added as local administrator on the device during Microsoft Entra join** | **All** (default) |

    > [!TIP]
    > In a production environment, you would typically restrict device join/registration to specific groups and require MFA for enhanced security.

1. At the top of the page, select **Save**.

1. Wait for the notification: "Successfully updated device settings."

1. Leave this browser tab open for the next task.

You have successfully configured Entra ID device settings to allow users to join and register devices.

## Exercise 4: Create organizational groups

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will create a static security group for your pilot users and a dynamic device group that will be used to assign policies and applications in later labs.

> [!NOTE]
> We are creating the pilot users group first so that it can be used when configuring automatic enrollment in Exercise 5.

### Task 1 - Create a static group for pilot users

In this task, you will create a static security group for the four pilot users who will participate in the device management pilot.

1. You should still be in the **Microsoft Entra admin center** as **Diego Siciliani**.

1. If needed, navigate to [**https://entra.microsoft.com**](https://entra.microsoft.com/).

1. In the left navigation pane, expand **Entra ID** → **Groups** and select **All groups**.

1. At the top of the page, select **New group**.

1. On the **New Group** page, configure the following settings:

    | Setting | Value |
    |---------|-------|
    | **Group type** | **Security** |
    | **Group name** | **Device Management Pilot Users** |
    | **Group description** | **Static group of users participating in the Intune device management pilot** |
    | **Membership type** | **Assigned** |

1. Under **Members**, select **No members selected**.

1. On the **Add members** page, search for and select the **four pilot users** you verified earlier:
    - **Alex Wilber**
    - **Allan Deyoung**
    - **Diego Siciliani**
    - **Joni Sherman**

1. Select **Select** at the bottom of the page.

1. Back on the **New Group** page, select **Create**.

1. Wait for the notification: "Group created successfully."

1. Leave the browser window open for the next task.

You have successfully created a static group for pilot users. This group will be used to configure automatic enrollment in Exercise 5.

### Task 2 - Create a dynamic device group for all Windows devices

In this task, you will create a dynamic device group that automatically includes all Windows devices enrolled in Intune.

1. You are still in the **Microsoft Entra admin center** as **Diego Siciliani**.

1. In the left navigation pane, expand **Entra ID** → **Groups** and select **All groups**.

1. At the top of the **All groups** page, select **New group**.

1. On the **New Group** page, configure the following settings:

    | Setting | Value |
    |---------|-------|
    | **Group type** | **Security** |
    | **Group name** | **All Windows Devices** |
    | **Group description** | **Dynamic group containing all Windows devices managed by Intune** |
    | **Membership type** | **Dynamic Device** |

1. Under **Dynamic device members**, select **Add dynamic query**.

1. On the **Dynamic membership rules** page, configure the rule:

    | Field | Value |
    |-------|-------|
    | **Property** | **deviceOSType** |
    | **Operator** | **Equals** |
    | **Value** | **Windows** |

1. The rule syntax should appear as: `(device.deviceOSType -eq "Windows")`

1. Select **Save** at the top of the page to save the dynamic query.

1. You are returned to the **New Group** page. Select **Create** at the bottom.

1. Wait for the notification: "Group created successfully."

    > [!NOTE]
    > The dynamic group will automatically evaluate and populate with devices as they enroll. This may take a few minutes after devices are enrolled in Lab 02.

1. Leave the browser window open for the next task.

You have successfully created a dynamic device group that will automatically include all Windows devices.

## Exercise 5: Configure automatic enrollment

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will enable automatic enrollment in Microsoft Intune for your pilot users so that their devices automatically enroll when they join them to Entra ID.

### Task 1 - Configure automatic enrollment for pilot users

In this task, you will enable automatic enrollment in Microsoft Intune for your pilot users so that their devices automatically enroll when they join them to Entra ID.

1. Open a new browser tab and navigate to the **Microsoft Intune admin center** at [**https://intune.microsoft.com**](https://intune.microsoft.com/).

1. Sign in with **Diego Siciliani's** credentials (DiegoS@yourtenant.onmicrosoft.com) if prompted.

1. In the left navigation pane, expand **Devices > Device onboarding ** and select **Enrollment**.

1. On the **Enrollment** page, select the **Windows** tab at the top.

1. Under **Enrollment options**, select **Automatic Enrollment**.

1. Set the **MDM user scope**:
    - Select **Some**
    - Select **+ Select groups**
    - Search for and select **Device Management Pilot Users**
    - Select **Select**

    > [!NOTE]
    > For this lab, we're scoping automatic enrollment to our pilot users group. In production, you might use **All** or different pilot groups.

1. Set the **WIP user scope** to **None**.

1. Review the pre-populated URLs:
    - **MDM Terms of Use URL**: `https://portal.manage.microsoft.com/TermsofUse.aspx`
    - **MDM Discovery URL**: `https://enrollment.manage.microsoft.com/enrollmentserver/discovery.svc`
    - **MDM Compliance URL**: `https://portal.manage.microsoft.com/?portalAction=Compliance`

    > [!NOTE]
    > These URLs are pre-populated by Microsoft and should not be changed unless you are using a third-party MDM provider.

1. Select **Save**.

1. Wait for the notification confirming the configuration was saved.

    > [!IMPORTANT]
    > With automatic enrollment enabled for the pilot users group, any device that these users join to Entra ID will automatically enroll in Intune without additional user action.

1. Leave this browser tab open for the next exercise.

You have successfully configured automatic enrollment for the pilot users group.

## Exercise 6: Verify Intune tenant status

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this exercise, you will access the Microsoft Intune admin center and verify that the Intune tenant is properly configured and ready for device enrollment.

### Task 1 - Access Intune admin center and review tenant status

In this task, you will verify the tenant configuration.

1. You should still be in the **Microsoft Intune admin center** as **Diego Siciliani**.

1. In the left navigation pane, expand **Tenant administration** and select **Tenant status**.

1. On the **Tenant status** page, review the following information:

    **Tenant details**:
    - **Tenant name**: Your organization's name
    - **Tenant location**: Geographic location (e.g., North America, Europe)
    - **MDM authority**: Should show **Microsoft Intune** ✅

    > [!IMPORTANT]
    > The **MDM authority** must be set to **Microsoft Intune** for device management. If it shows "Not set" or "Configuration Manager", Intune is not properly configured.

1. Leave the browser window open.

You have successfully accessed the Microsoft Intune admin center and verified that the tenant is configured with Microsoft Intune as the MDM authority.

### Task 2 - Review Intune subscription and service health

In this task, you will verify the Intune subscription is active.

1. You are still in the **Microsoft Intune admin center** as **Diego Siciliani**.

1. In the left navigation pane, select **Home** (or select **Dashboard** if available).

1. Review the dashboard showing:
    - **Device enrollment status**: Should show 0 devices (we'll enroll devices in Lab 02)
    - **Device compliance status**: No data yet
    - **Configuration profile status**: No data yet
    - **App installation status**: No data yet

    > [!NOTE]
    > The dashboard will populate with data as you enroll devices and assign policies in later labs.

You have successfully verified that the Intune subscription is active and working.

## Exercise 7: Initialize Microsoft Defender for Endpoint

### Exercise Duration

  - **Estimated Time to complete**: 8 minutes

In this exercise, you will initialize Microsoft Defender for Endpoint in your tenant. This is a prerequisite for connecting Defender for Endpoint to Intune in Lab 05, and completing it now prevents interruptions during later security configuration labs.

### Task 1 - Initialize Defender for Endpoint portal

In this task, you will access the Microsoft Defender portal for the first time to trigger tenant provisioning.

1. Open a new browser tab and navigate to the **Microsoft Defender portal** at [**https://security.microsoft.com**](https://security.microsoft.com/).

1. Sign in with **Diego Siciliani's** credentials if prompted.

1. If you see a **Welcome to Microsoft Defender for Endpoint** screen or setup wizard:
    - Review the welcome message
    - Select **Start using Microsoft Defender for Endpoint** (or similar button)
    - Follow any prompts to complete the initial setup

1. Wait a few moments while the portal initializes. You should see the main Defender dashboard load with sections for:
    - **Incidents & alerts**
    - **Assets** (Devices, Identities, Apps)
    - **Exposure management**
    - **Threat intelligence**

    > [!NOTE]
    > The portal will show empty dashboards at this point since no devices are onboarded yet. This is expected.

1. In the left navigation pane, expand **Assets** and select **Devices**.

1. You should see an empty **Device inventory** page with the message "No devices onboarded yet."

    > [!NOTE]
    > This confirms the Defender for Endpoint service is provisioned and ready. You will onboard devices in Lab 05 after deploying security baselines.

1. Leave this browser tab open for the next task.

You have successfully initialized Microsoft Defender for Endpoint in your tenant.

### Task 2 - Enable Microsoft Intune connection in Defender portal

In this task, you will enable the bidirectional connection between Defender for Endpoint and Intune.

1. You are still in the **Microsoft Defender portal** at [**https://security.microsoft.com**](https://security.microsoft.com/).

1. In the left navigation pane (at the bottom), select the **Settings** gear icon, or navigate to **Settings**.

1. On the **Settings** page, select **Endpoints** from the left menu.

1. Under **General**, select **Advanced features**.

1. On the **Advanced features** page, scroll down and locate **Microsoft Intune connection**.

1. Toggle **Microsoft Intune connection** to **On**.

    > [!NOTE]
    > This enables Defender for Endpoint to share device information with Intune and allows Intune to enforce security policies on managed devices.

1. Review the description: "Connects to Microsoft Intune to enable sharing of device information and enhanced policy enforcement."

1. At the bottom of the page, select **Save preferences**.

1. Wait for the notification confirming the settings were saved.

You have successfully enabled the Microsoft Intune connection from the Defender for Endpoint side.

### Task 3 - Verify Defender for Endpoint connector readiness in Intune

In this task, you will verify that the Defender for Endpoint connector in Intune is now ready for configuration.

1. Return to the **Microsoft Intune admin center** tab where you are signed in as **Diego Siciliani**.

1. In the left navigation pane, expand **Tenant administration** and select **Connectors and tokens**.

1. On the **Connectors and tokens** page, locate **Microsoft Defender for Endpoint** and select it.

1. On the **Microsoft Defender for Endpoint** connector page, verify that:
    - **Connection status** shows "Not set up" (this is expected - we'll configure the connection in Lab 05)
    - The toggle switches for **Windows**, **Android**, and **iOS** device connections are now **enabled** (not grayed out)

    > [!IMPORTANT]
    > If the toggles are still grayed out, wait 5 minutes and refresh the page. The Defender for Endpoint service may still be provisioning.

    > [!NOTE]
    > The connection is now ready from both sides: you enabled the "Microsoft Intune connection" in Defender portal, and the Intune connector toggles are enabled. In Lab 05, you'll complete the configuration by turning on these toggles and creating the onboarding profile.

1. **Do not configure any settings yet** - you will complete the connector configuration in Lab 05.

1. Close this page and return to the Intune dashboard.

You have successfully verified that Microsoft Defender for Endpoint is initialized and the bidirectional connection with Intune is ready. The connector will be fully configured in Lab 05 when you deploy security baselines.

## Lab Completion

Congratulations! You have successfully completed Lab 01: Configure tenant for device management.

### Summary of what you accomplished

In this lab, you:

- ✅ Signed in with Global Administrator and reviewed available licenses in the Microsoft 365 tenant
- ✅ Verified Intune/EMS licenses are assigned to the four pilot users (Alex Wilber, Allan Deyoung, Diego Siciliani, Joni Sherman)
- ✅ Assigned administrative roles to Diego Siciliani following zero-trust and least privilege principles
- ✅ Signed out of Global Administrator and signed in with Diego Siciliani's role-based administrative account (Intune Administrator)
- ✅ Configured Entra ID device settings to allow device join and registration
- ✅ Created a static security group for pilot users
- ✅ Created a dynamic device group for all Windows devices
- ✅ Enabled automatic enrollment in Intune for the pilot users group
- ✅ Verified Intune tenant status and MDM authority
- ✅ Initialized Microsoft Defender for Endpoint portal
- ✅ Enabled Microsoft Intune connection in Defender portal (bidirectional integration)
- ✅ Verified Intune connector toggles are enabled and ready for configuration
- ✅ Confirmed all configurations are in place for device enrollment

> [!IMPORTANT]
> **For all remaining labs**: Continue using **Diego Siciliani's** account (Intune Administrator) for all administrative tasks. Do not use Global Administrator.