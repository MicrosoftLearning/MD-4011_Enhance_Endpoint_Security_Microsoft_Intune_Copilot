---
lab:
  title: 'Lab 05: Harden devices with security baselines'
  type: Answer Key
  module: 'Module 05: Harden endpoints and monitor security with Microsoft Intune and Defender for Endpoint'
  description: In this lab, you will deploy Windows security baselines to enforce comprehensive security settings, onboard devices to Microsoft Defender for Endpoint for advanced threat protection, configure Attack Surface Reduction (ASR) rules to block common attack vectors, and monitor security posture through the Defender portal.
  duration: 45 minutes
  level: 300
  islab: true
  primarytopics:
    - Windows
    - Windows 11
---

# Lab 05: Harden devices with security baselines
# Student lab answer key

> **Abstract:**  
> In this lab, you will deploy Windows security baselines to enforce comprehensive security settings, onboard devices to Microsoft Defender for Endpoint for advanced threat protection, configure Attack Surface Reduction (ASR) rules to block common attack vectors, and monitor security posture through the Defender portal.

## Lab scenario

Continuing as **Diego Siciliani**, Contoso Healthcare's Modern Endpoint Administrator, you have successfully protected data and enforced access controls in Lab 04. Now you need to harden devices against advanced threats by deploying security baselines, integrating with Microsoft Defender for Endpoint, and configuring proactive threat prevention.

In this lab, you will deploy the Windows 11 security baseline to enforce 100+ recommended security settings, onboard enrolled devices to Defender for Endpoint for advanced threat detection and response, configure ASR rules to block credential theft and malicious scripts, and monitor device security posture and vulnerabilities through the Defender portal.

## Lab Duration

  - **Estimated Time to complete**: 45 minutes

## Instructions

### Before You Begin

> [!IMPORTANT]
> **Prerequisites**: You must complete **Lab 01-04** before starting this lab. You need at least one enrolled Windows device.

> [!IMPORTANT]
> **Administrative Account**: Continue using **Diego Siciliani's** account (DiegoS@yourtenant.onmicrosoft.com) for all administrative tasks. Diego has the **Intune Administrator** and **Security Administrator** roles from Lab 01, which provide the necessary permissions for security baselines and Defender for Endpoint integration.

> [!NOTE]
> **License Requirements**: This lab requires **Microsoft Defender for Endpoint Plan 2** (included in Microsoft 365 E5 or standalone licenses).

## Exercise 1: Deploy Windows security baseline

### Exercise Duration

  - **Estimated Time to complete**: 15 minutes

In this exercise, you will deploy the Windows security baseline to enforce Microsoft-recommended security settings across your Windows devices.

### Task 1 - Create and deploy security baseline

1. Navigate to the **Microsoft Intune admin center** at [**https://intune.microsoft.com**](https://intune.microsoft.com/).

1. Sign in with **Diego Siciliani's** credentials (DiegoS@yourtenant.onmicrosoft.com) if prompted.

    > [!NOTE]
    > Diego has the **Intune Administrator** and **Security Administrator** roles from Lab 01, which provide the necessary permissions for security baselines and Defender for Endpoint integration.

1. In the left navigation pane, expand **Endpoint security** and select **Security baselines**.

1. On the **Security baselines** page, you should see several baseline options:
    - **Security Baseline for Windows 10 and later**
    - **Microsoft Defender for Endpoint Security baseline** (if Defender integration is enabled)
    - **Security Baseline for Microsoft Edge**
    - **Microsoft 365 Apps for Enterprise Security Baseline**

1. Select **Security Baseline for Windows 10 and later**.

1. Select **+ Create policy**. On the flyout, select **Create**.

1. On the **Basics** page:
    - **Name**: `Windows 11 Security Baseline - Corporate Devices`
    - **Description**: `Microsoft-recommended security baseline with 100+ security settings for Windows 11 devices`

1. Select **Next**.

1. On the **Configuration settings** page, you will see multiple categories of security settings. The most important categories include:
    - **Administrative Templates** (includes Network, System, Windows Components subcategories)
    - **Defender** (antivirus and threat protection)
    - **Device Guard** (code integrity and virtualization-based security)
    - **Device Lock** (password and authentication policies)
    - **Firewall** (network protection rules)
    - **Local Policies Security Options** (authentication and account policies)
    - **Smart Screen** (phishing and malware protection)
    - **User Rights Assignment** (privilege management)

    > [!NOTE]
    > The security baseline contains 100+ pre-configured settings based on Microsoft security team recommendations. Most settings should be left at their default (recommended) values.

1. Expand the **Defender** category to review specific Microsoft Defender settings:
    - **Cloud Extended Timeout**: `50` seconds (allows more time for cloud-based threat analysis)
    - **Enable Network Protection**: `Enabled (block mode)` (blocks malicious network connections)
    - **PUA Protection**: `Enabled` (detects potentially unwanted applications)
    - **Real Time Scan Direction**: `Monitor all files (bi-directional)`
    - **Submit Samples Consent**: `Send all samples automatically` (for threat analysis)

1. Collapse **Defender** and expand **Device Guard** to review:
    - **Credential Guard**: `Enabled with UEFI lock` (protects domain credentials)
    - **Enable Virtualization Based Security**: `Enabled` (hardware-based security features)

1. Collapse **Device Guard** and expand **Administrative Templates** → **Windows Components** → **BitLocker Drive Encryption** → **Removable Data Drives**:
    - **Deny write access to removable drives not protected by BitLocker**: `Enabled` (enforces encryption on USB drives)

    > [!TIP]
    > Notice how settings are organized hierarchically: Administrative Templates contains Windows Components, which contains BitLocker subcategories. Intune automatically configures all these settings to Microsoft-recommended values.

1. Review any other categories of interest, then leave all settings at their **default (recommended)** values unless you have specific organizational requirements.

1. Select **Next**.

1. Select **Next** through **Scope tags** (leave default).

1. On the **Assignments** page, under **Included groups**, select **+ Add groups**.

1. Select **All Windows Devices**.

1. Select **Select**.

1. On the **Review + create** page, review the configuration and select **Create**.

You have successfully deployed the Windows security baseline to your enrolled devices.

### Task 2 - Monitor security baseline deployment

1. After creating the baseline, you are returned to the **Security baselines** page.

1. Select **Security Baseline for Windows 10 and later** to view all profiles.

1. Select the **Windows 11 Security Baseline - Corporate Devices** profile.

1. On the profile overview page, review:
    - **Device status**: Success, Pending, Error, Conflict
    - **Assignment status**: Number of assigned devices

    > [!NOTE]
    > Baseline deployment can take several hours as devices sync and apply 100+ settings. Status may show "Pending" initially.

1. Select **Device status** in the left menu to view per-device deployment results.

1. If any devices show "Error" or "Conflict," select the device to view detailed error messages.

1. Leave the browser window open for the next exercise.

## Exercise 2: Onboard devices to Microsoft Defender for Endpoint

### Exercise Duration

  - **Estimated Time to complete**: 15 minutes

In this exercise, you will configure the Microsoft Defender for Endpoint connector in Intune and onboard your enrolled devices to the Defender service.

### Task 1 - Configure Defender for Endpoint connector

1. You are in the **Microsoft Intune admin center**.

1. In the left navigation pane, expand **Tenant administration** and select **Connectors and tokens**.

1. On the **Connectors and tokens** page, locate **Microsoft Defender for Endpoint** and select it.

1. On the **Microsoft Defender for Endpoint** connector page, you'll see **Connection status: Not set up**.

    > [!NOTE]
    > In Lab 01, you initialized Microsoft Defender for Endpoint and enabled the bidirectional connection between Defender and Intune. The connector toggles should now be enabled (not grayed out). If any toggles are still grayed out, wait a few minutes and refresh the page.

1. Configure the following settings:

    | Setting | Value |
    |---------|-------|
    | **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** | **On** (allows Defender to remediate vulnerabilities via Intune) |
    | **Connect Windows devices version 10.0.15063 and above to Microsoft Defender for Endpoint** | **On** |
    | **Connect Android devices to Microsoft Defender for Endpoint** | Optional (On if you have Android devices) |
    | **Connect iOS devices to Microsoft Defender for Endpoint** | Optional (On if you have iOS devices) |

1. Select **Save** at the top of the page.

1. Wait for the notification: "Successfully updated Microsoft Defender for Endpoint settings."

    > [!NOTE]
    > This completes the bidirectional integration between Intune and Defender for Endpoint. You enabled the connection from the Defender side in Lab 01, and now you've configured it from the Intune side. This allows device onboarding, security signal sharing, and policy enforcement.

1. Leave the browser window open for the next task.

### Task 2 - Create Defender for Endpoint onboarding profile

1. You are in the **Microsoft Intune admin center**.

1. In the left navigation pane, expand **Devices** and select **Configuration**.

1. Select the **Policies** tab.

1. Select **+ Create** → **+ New policy**.

1. On the **Create a profile** pane:
    - **Platform**: Windows 10 and later
    - **Profile type**: Templates
    - **Template name**: Select **Microsoft Defender for Endpoint**

1. Select **Create**.

1. On the **Basics** page:
    - **Name**: `Defender for Endpoint Onboarding - Windows`
    - **Description**: `Onboards Windows devices to Microsoft Defender for Endpoint for advanced threat protection`

1. Select **Next**.

1. On the **Configuration settings** page:
    - **Microsoft Defender for Endpoint client configuration package type**: **Onboard**
    - **Onboarding blob**: This field should auto-populate with the onboarding package from Defender. If blank, wait a moment and refresh.

    > [!NOTE]
    > The onboarding blob is automatically retrieved from the Defender for Endpoint tenant once the connector is enabled.

1. Select **Next**.

1. On the **Assignments** page, under **Included groups**, select **+ Add groups**.

1. Select **All Windows Devices**.

1. Select **Select**.

1. Select **Next** through **Scope tags** (leave default).

1. On the **Review + create** page, review and select **Create**.

You have successfully created the Defender for Endpoint onboarding profile.

### Task 3 - Verify device onboarding in Defender portal

1. Open a new browser tab and navigate to the **Microsoft Defender portal** at [**https://security.microsoft.com**](https://security.microsoft.com/).

1. Sign in with your **Security Administrator** or **Global Administrator** credentials.

1. In the left navigation pane, expand **Assets** and select **Devices**.

1. On the **Device inventory** page, wait 5-15 minutes for your enrolled devices to appear after the onboarding policy is applied.

    > [!NOTE]
    > Device onboarding can take 15-30 minutes after policy is applied. Devices must sync with Intune and then communicate with the Defender service.

1. Once your devices appear, you should see both **SEA-WS1** and **SEA-WS2** in the inventory.

1. Select **SEA-WS1** to view details:
    - **Onboarding status**: Active ✅
    - **Risk level**: Low, Medium, High (based on detected threats)
    - **Sensor health**: Active, Inactive, Misconfigured
    - **Last seen**: Timestamp of most recent check-in
    - **Threat detections**: Number of active alerts

1. Review the device details page showing:
    - **Timeline**: Security events and activities
    - **Security recommendations**: Actions to improve device security
    - **Installed software**: Detected applications
    - **Discovered vulnerabilities**: CVEs affecting installed software

1. Go back to the device inventory and select **SEA-WS2** to view its details.

1. Compare the security posture of both devices:
    - Risk levels
    - Security recommendations
    - Installed software inventory
    - Vulnerability counts

    > [!TIP]
    > Having multiple devices allows you to compare security postures, identify vulnerable devices, and prioritize remediation efforts across your fleet.

1. Leave the browser window open for the next exercise.

## Exercise 3: Configure Attack Surface Reduction rules

### Exercise Duration

  - **Estimated Time to complete**: 10 minutes

In this exercise, you will configure ASR rules to block common attack techniques like credential theft, malicious scripts, and Office macro exploits.

### Task 1 - Create ASR rules policy

1. Return to the **Microsoft Intune admin center** tab.

1. In the left navigation pane, expand **Endpoint security** and select **Attack surface reduction**.

1. Select **+ Create Policy**.

1. On the **Create a policy** pane:
    - **Platform**: Windows 10, Windows 11, and Windows Server
    - **Profile**: Attack Surface Reduction Rules

1. Select **Create**.

1. On the **Basics** page:
    - **Name**: `ASR Rules - Block Common Threats`
    - **Description**: `Blocks credential theft, Office macros, script execution, and other common attack vectors`

1. Select **Next**.

1. On the **Configuration settings** page, configure the following ASR rules (set to **Block** mode):

    | Rule | Setting |
    |------|---------|
    | **Block credential stealing from the Windows local security authority subsystem (lsass.exe)** | **Block** |
    | **Block executable content from email client and webmail** | **Block** |
    | **Block all Office applications from creating child processes** | **Block** |
    | **Block Office applications from creating executable content** | **Block** |
    | **Block Office applications from injecting code into other processes** | **Block** |
    | **Block JavaScript or VBScript from launching downloaded executable content** | **Block** |
    | **Block execution of potentially obfuscated scripts** | **Block** |
    | **Block Win32 API calls from Office macros** | **Block** |
    | **Use advanced protection against ransomware** | **Block** |
    | **Block executable files from running unless they meet a prevalence, age, or trusted list criterion** | **Audit** (test first to avoid breaking legitimate apps) |

    > [!TIP]
    > Start with **Audit** mode for rules that might impact legitimate applications. Review audit events in Defender portal, then switch to **Block** mode once you've validated there are no false positives.

1. Select **Next**.

1. On the **Assignments** page, under **Included groups**, select **+ Add groups**.

1. Select **All Windows Devices**.

1. Select **Select**.

1. Select **Next** through **Scope tags** (leave default).

1. On the **Review + create** page, review and select **Create**.

You have successfully configured ASR rules to protect against common attack techniques.

## Exercise 4: Monitor security posture

### Exercise Duration

  - **Estimated Time to complete**: 5 minutes

In this exercise, you will review the security posture of your devices in the Microsoft Defender portal.

### Task 1 - Review vulnerability management dashboard

1. You are in the **Microsoft Defender portal** at [**https://security.microsoft.com**](https://security.microsoft.com/).

1. In the left navigation pane, expand **Exposure management**.

1. Under **Vulnerability management**, select **Overview**.

1. On the **Vulnerability management** overview page, review the following metrics:

    **Exposure score** (0-100):
    - Measures overall organizational exposure to vulnerabilities
    - Lower score = better security posture
    - Based on discovered vulnerabilities, attack surface, and breach likelihood

    **Configuration score** (0-100%):
    - Measures alignment with Microsoft security recommendations
    - Higher score = better configuration compliance
    - Based on security baseline adoption and security control implementation

    **Top security recommendations**:
    - List of prioritized actions to improve security (e.g., "Update Microsoft Office to the latest version," "Enable tamper protection," "Enable controlled folder access")

    **Vulnerable devices**:
    - Number of devices with known vulnerabilities

1. Leave the browser window open for the next task.

### Task 2 - Review security recommendations

1. You are still in the **Microsoft Defender portal** → **Vulnerability management**.

1. In the left menu, select **Recommendations**.

1. On the **Security recommendations** page, you will see a prioritized list of security improvements:
    - **Recommendation name**: Action to take (e.g., "Install security updates for Microsoft Edge")
    - **Exposed devices**: Number of affected devices
    - **Impact**: Security benefit of implementing the recommendation
    - **Effort**: Implementation difficulty (Low, Medium, High)

1. Select a recommendation to view details:
    - **Description**: What the recommendation addresses
    - **Remediation**: How to implement the fix
    - **Exposed devices**: List of affected devices
    - **Security insights**: Why this recommendation improves security

1. Some recommendations can be remediated directly through Intune. For example, select a recommendation like "Enable tamper protection":
    - If supported, you'll see an option: **Remediate via Intune**
    - This creates a configuration profile in Intune automatically

1. Leave the browser window open for the next task.

### Task 3 - Review alerts and incidents

1. You are still in the **Microsoft Defender portal**.

1. In the left navigation pane, expand **Incidents & alerts** and select **Alerts**.

1. On the **Alerts** page, review any security alerts detected on your devices:
    - **Severity**: Informational, Low, Medium, High, Critical
    - **Status**: New, In progress, Resolved
    - **Detection source**: Defender Antivirus, ASR rules, EDR, etc.
    - **Alert title**: Description of the threat (e.g., "Suspicious PowerShell execution detected")

1. Select an alert (if any exist) to view details:
    - **Alert story**: Timeline of events leading to the alert
    - **Affected assets**: Devices, users, files involved
    - **MITRE ATT&CK techniques**: Attacker tactics and techniques
    - **Recommended actions**: Response steps (isolate device, run scan, block file)

1. Review the alert story to understand what triggered the detection.

1. If no alerts exist yet, this is good news—your devices are secure! Alerts will appear when threats are detected.

## Lab Completion

Congratulations! You have successfully completed Lab 05: Harden devices with security baselines.

### Summary of what you accomplished

In this lab, you:
- ✅ Deployed Windows security baseline with 100+ Microsoft-recommended security settings
- ✅ Monitored security baseline deployment status across devices
- ✅ Configured Microsoft Defender for Endpoint connector in Intune
- ✅ Created Defender for Endpoint onboarding profile to onboard Windows devices
- ✅ Verified both SEA-WS1 and SEA-WS2 onboarding in the Defender portal
- ✅ Compared security posture across multiple devices
- ✅ Configured ASR rules to block credential theft, Office macros, script execution, and ransomware
- ✅ Reviewed vulnerability management dashboard (exposure score, configuration score)
- ✅ Reviewed security recommendations for improving device security
- ✅ Reviewed alerts and incidents to understand threat detections

### Next steps

In **Lab 06: Investigate incidents with Security Copilot (capstone)**, you will:
- Investigate security incidents using AI-powered Security Copilot
- Use natural language prompts to analyze threats and extract intelligence
- Troubleshoot device compliance issues with Copilot in Intune
- Generate investigation reports for technical and executive audiences

---

**Lab Status**: ✅ Complete  
**Next Lab**: Lab 06 - Investigate incidents with Security Copilot (capstone)  
**Estimated Time for Next Lab**: 60 minutes
