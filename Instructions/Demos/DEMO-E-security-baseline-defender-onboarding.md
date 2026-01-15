# Demo E: Security Baseline and Defender Onboarding

**Module**: Module 5 - Harden endpoints and monitor security  
**Duration**: 12-15 minutes  
**Difficulty**: Intermediate to Advanced  
**Demo Type**: Instructor-led hands-on

## Learning Objectives

After this demonstration, learners will understand how to:
- Deploy Windows security baselines to harden device configurations
- Onboard devices to Microsoft Defender for Endpoint
- Configure Attack Surface Reduction (ASR) rules
- Monitor device security posture in Defender portal
- View and respond to security alerts

## Prerequisites

### Instructor Requirements
- Intune Administrator and Security Administrator roles
- Completion of Demos A-C (device enrolled, policies applied)

### Environment Requirements
- Windows 11 device enrolled in Intune
- Microsoft Defender for Endpoint P2 license
- Internet connectivity for onboarding

### Licenses Required
- Microsoft 365 E5 or E3 + Defender for Endpoint P2

## Demo Scenario

**Context**: Contoso Healthcare has enrolled devices and applied basic policies. Now they need to harden Windows devices with security baselines and enable advanced threat protection with Microsoft Defender for Endpoint.

**Narrative**: "Basic policies aren't enough against modern threats. We need comprehensive security hardening and continuous threat monitoring. We'll deploy Microsoft's security baseline (100+ security settings) and onboard devices to Defender for Endpoint for real-time threat detection."

## Step-by-Step Instructions

### Part 1: Deploy Windows security baseline (5-6 minutes)

#### Step 1.1: Access security baselines

**Action**: Navigate to security baselines in Intune

1. Navigate to **https://intune.microsoft.com**
2. Go to **Endpoint security** → **Security baselines**
3. Review available baselines:
   - Security Baseline for Windows 10 and later (latest version)
   - Microsoft Defender for Endpoint baseline
4. Select **Security Baseline for Windows 10 and later**
5. Click **+ Create policy**
6. In the **Create a profile** pane, select **Create**

**Talking points**:
- "Security baselines are Microsoft's recommended security configurations"
- "Based on real-world threats and Microsoft Security Team guidance"
- "Windows baseline contains 100+ settings: BitLocker, firewall, Defender, user rights, etc."
- "Baselines are updated regularly as new threats emerge"

![Security baselines page](media/microsoft-intune-admin-center-create-baseline-profile.png)

#### Step 1.2: Configure baseline settings

**Action**: Review and customize baseline settings

1. **Basics** page:
   - Name: `Windows 11 Security Baseline - Corporate Devices`
   - Description: `Microsoft recommended security settings for Windows 11 devices`
2. Click **Next**
3. **Configuration settings** page:
   - Review categories: Application Guard, Defender, BitLocker, Browser, Device Guard, Firewall, etc.
   - For demo, leave all settings at **default (recommended)** values
   - Optionally expand a few categories to show:
     - **Defender**: Real-time protection, cloud-delivered protection, potentially unwanted application blocking
     - **Browser**: Password Manager, Smart Screen
     - **Firewall**: Domain, private, and public profile settings
4. Click **Next**

**Talking points**:
- "Baseline includes ~100 settings - would take hours to configure manually"
- "All settings are pre-configured to Microsoft's recommendations"
- "You can customize if your organization needs stricter or different settings"
- "Green checkmarks indicate settings are enabled/configured"

![Baseline settings configuration](media/microsoft-intune-admin-center-create-baseline-profile-settings.png)

#### Step 1.3: Assign baseline

**Action**: Deploy to Windows devices

1. **Assignments** page:
   - Include: **All Windows Devices** (dynamic group)
   - Exclude: None (or create exception group for testing)
2. Click **Next**
3. **Review + create**: Review and click **Create**

**Talking points**:
- "Baseline deploys like any other configuration profile"
- "Devices will receive 100+ security settings in one policy"
- "Deployment can take 15-30 minutes depending on number of settings"
- "Monitor deployment status in Endpoint security → Security baselines"

![Baseline policy assignments](media/microsoft-intune-admin-center-create-baseline-profile-assignments.png)

---

### Part 2: Onboard devices to Microsoft Defender for Endpoint (4-5 minutes)

#### Step 2.1: Configure Defender for Endpoint connector

**Action**: Connect Intune to Defender

1. In Intune admin center, go to **Tenant administration** → **Connectors and tokens** → **Microsoft Defender for Endpoint**
2. Verify or enable:
   - **Connect Windows devices to Microsoft Defender for Endpoint**: **On**
   - **Connect Android devices**: Optional (On if managing Android)
   - **Connect iOS devices**: Optional (On if managing iOS)
3. Optionally configure:
   - **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations**: **On** (enables Security Management for Devices)
4. Click **Save**

**Talking points**:
- "This connector enables automatic onboarding - devices enroll in Intune and onboard to Defender simultaneously"
- "No manual onboarding package needed - completely automated"
- "Enforcement setting allows Defender to push security configurations even to non-Intune devices"

<!-- **TODO**: Screenshot of Defender connector settings -->

#### Step 2.2: Create Defender onboarding configuration profile

**Action**: Deploy onboarding policy

1. Navigate to **Devices** → **Configuration** → **Create** → **New policy**
2. Select:
   - Platform: **Windows 10 and later**
   - Profile type: **Templates** → **Microsoft Defender for Endpoint (Windows 10 Desktop)**
3. **Basics**:
   - Name: `Defender for Endpoint Onboarding - Windows`
   - Description: `Onboards Windows devices to Defender for Endpoint`
4. **Configuration settings**:
   - **Microsoft Defender for Endpoint client configuration package type**: **Onboard**
   - Onboarding blob auto-populates (fetched from Defender)
5. **Assignments**: **All Windows Devices**
6. **Review + create** and click **Create**

**Talking points**:
- "This policy installs the Defender for Endpoint sensor on devices"
- "Sensor sends telemetry to Defender cloud: processes, network connections, file activities"
- "Onboarding takes 5-10 minutes after policy deployment"
- "Once onboarded, devices appear in Microsoft Defender portal"

![Defender for Endpoint onboarding profile](media/microsoft-intune-admin-center-create-configuration-profile-defender-endpoint.png)

<!-- **TODO**: Screenshot of onboarding policy assignments -->

#### Step 2.3: Verify onboarding in Defender portal

**Action**: Check device onboarding status

1. Open new browser tab and navigate to **https://security.microsoft.com** (Microsoft Defender portal)
2. Sign in with Security Administrator credentials
3. Go to **Devices** → **Device inventory**
4. Look for the enrolled Windows device
5. Click on device to view:
   - Onboarding status: Active
   - Risk level: None/Low/Medium/High
   - Sensor health: Active
   - Last seen: Recent timestamp
   - Threat detections: Count of alerts

**Talking points**:
- "Device appears in Defender within 15 minutes of onboarding"
- "Active sensor health means telemetry is flowing properly"
- "Risk level is calculated based on alerts, vulnerabilities, and security configuration"
- "This is where security teams monitor threats in real-time"

<!-- **TODO**: Screenshot of Defender device inventory -->
<!-- **TODO**: Screenshot of device details in Defender portal -->

---

### Part 3: Configure Attack Surface Reduction rules (3-4 minutes)

#### Step 3.1: Create ASR policy

**Action**: Deploy ASR rules to block threats

1. Return to Intune admin center: **https://intune.microsoft.com**
2. Navigate to **Endpoint security** → **Attack surface reduction**
3. Click **+ Create Policy**
4. Select:
   - Platform: **Windows**
   - Profile: **Attack Surface Reduction Rules**
5. Click **Create**

**Talking points**:
- "ASR rules block common attack techniques: malicious Office macros, script-based threats, credential theft"
- "These are preventative - stop attacks before they execute"
- "Can be set to Audit (log only) or Block (prevent execution)"

![ASR policy creation](media/microsoft-intune-admin-center-create-asr-policy-rule.png)

#### Step 3.2: Configure ASR rule settings

**Action**: Enable key ASR rules

1. **Basics**:
   - Name: `ASR Rules - Block Common Threats`
   - Description: `Blocks Office macros, script-based attacks, and credential theft attempts`
2. **Configuration settings**, enable these rules (set to **Block**):
   - **Block credential stealing from Windows local security authority subsystem (lsass.exe)**: **Block**
   - **Block executable content from email client and webmail**: **Block**
   - **Block Office applications from creating executable content**: **Block**
   - **Block Office applications from injecting code into other processes**: **Block**
   - **Block JavaScript or VBScript from launching downloaded executable content**: **Block**
   - **Block execution of potentially obfuscated scripts**: **Block**
3. Click **Next**

**Talking points**:
- "LSASS protection prevents credential dumping attacks - like the exercise in Module 6"
- "Office macro protection stops malicious document-based attacks"
- "Script execution blocks prevent PowerShell/JavaScript-based malware"
- "Start with Audit mode in production to test impact, then switch to Block"

![ASR rules configuration](media/microsoft-intune-admin-center-create-asr-rule-settings.png)

#### Step 3.3: Assign ASR policy

**Action**: Deploy to Windows devices

1. **Assignments**: **All Windows Devices**
2. Click **Next**
3. **Review + create** and click **Create**

**Talking points**:
- "ASR rules apply immediately after policy sync"
- "Users may see toast notifications when threats are blocked"
- "Monitor ASR effectiveness in Defender portal → Reports → Attack surface reduction"

![ASR policy assignments](media/microsoft-intune-admin-center-create-asr-rule-assignments.png)

---

### Part 4: Monitor security posture (2-3 minutes)

#### Step 4.1: View security recommendations

**Action**: Check Defender Vulnerability Management

1. In Defender portal (**https://security.microsoft.com**):
2. Go to **Vulnerability management** → **Dashboard**
3. Review:
   - **Exposure score**: Organizational vulnerability level (0-1000, lower is better)
   - **Configuration score**: Security configuration effectiveness
   - **Top security recommendations**: Most impactful actions to improve security
4. Click **Recommendations**
5. Browse top recommendations:
   - Update Microsoft Office
   - Enable tamper protection
   - Configure controlled folder access
   - Turn on exploit protection

**Talking points**:
- "Defender continuously scans for vulnerabilities and misconfigurations"
- "Exposure score gives at-a-glance view of organizational risk"
- "Recommendations are prioritized by impact - fix high-impact issues first"
- "Recommendations link back to Intune policies for remediation"

<!-- **TODO**: Screenshot of Vulnerability Management dashboard -->
<!-- **TODO**: Screenshot of security recommendations -->

#### Step 4.2: View security alerts (simulated or historical)

**Action**: Show alert investigation workflow

1. In Defender portal, go to **Investigation & response** → **Incidents & alerts** → **Alerts**
2. If alerts exist, select one to demonstrate:
   - Alert severity: Informational, Low, Medium, High
   - Alert story: Timeline of attack
   - Affected assets: Devices, users, files involved
   - MITRE ATT&CK techniques: Attack classification
3. Show recommended actions:
   - Isolate device
   - Run antivirus scan
   - Block file
   - Investigate user

**Talking points**:
- "Alerts are generated when suspicious activity is detected"
- "Each alert provides investigation context - what happened, when, which device"
- "MITRE ATT&CK mapping helps understand attacker techniques"
- "Recommended actions guide response - even for junior analysts"
- "In Module 6, we'll use Security Copilot to investigate alerts even faster"

<!-- **TODO**: Screenshot of alerts queue -->
<!-- **TODO**: Screenshot of alert details with investigation timeline -->

---

## Demo Summary

**Recap key steps**:
1. ✅ Deployed Windows security baseline with 100+ recommended security settings
2. ✅ Enabled Defender for Endpoint connector for automatic onboarding
3. ✅ Created onboarding configuration profile to deploy Defender sensor
4. ✅ Verified device onboarding in Defender portal
5. ✅ Configured Attack Surface Reduction (ASR) rules to block common threats
6. ✅ Reviewed security posture: vulnerability dashboard, recommendations, alerts

**Key takeaways**:
- "Security baselines provide comprehensive hardening in one policy - 100+ settings vs. manual configuration"
- "Defender for Endpoint onboarding is automated via Intune connector - no manual deployment needed"
- "ASR rules prevent attacks before execution - proactive defense, not reactive response"
- "Vulnerability Management continuously assesses risk and provides actionable recommendations"
- "Defender portal is central hub for threat monitoring, investigation, and response"

**Transition to next module**:
"We've hardened devices and enabled continuous monitoring. In Module 6, we'll add AI-powered capabilities with Security Copilot to investigate threats even faster and empower analysts of all skill levels."

---

## Common Issues and Troubleshooting

### Issue: Device doesn't appear in Defender portal after onboarding
**Cause**: Onboarding delay, network connectivity, or sensor not running  
**Solution**: 
- Wait 30 minutes for initial onboarding telemetry
- Verify device has internet connectivity to Defender cloud endpoints
- Check Defender services running: Settings → Privacy & Security → Windows Security → Virus & threat protection

### Issue: Security baseline fails to deploy to some devices
**Cause**: Conflicting policies, device offline, or OS version incompatibility  
**Solution**: 
- Check device compliance and last sync time
- Review baseline deployment status: Endpoint security → Security baselines → Select baseline → Monitor → Device status
- Resolve policy conflicts: If multiple policies configure same setting, most restrictive wins

### Issue: ASR rules block legitimate business applications
**Cause**: Application behavior triggers ASR rule (false positive)  
**Solution**: 
- Start with Audit mode to identify false positives before Block mode
- Create exclusions: Endpoint security → Attack surface reduction → Select policy → Properties → Exclusions
- Work with application vendor to modify app behavior if possible

### Issue: Exposure score is very high (> 500)
**Cause**: Many unpatched vulnerabilities, missing security configurations  
**Solution**: 
- Review top security recommendations and implement high-impact fixes first
- Deploy Windows Update policies to ensure devices receive security patches
- Remediate highest-severity vulnerabilities (CVE score > 7.0) immediately

---

## Additional Resources

- [Security baselines overview](https://learn.microsoft.com/mem/intune/protect/security-baselines)
- [Onboard Windows devices to Defender for Endpoint](https://learn.microsoft.com/defender-endpoint/onboard-windows-client)
- [Attack Surface Reduction rules overview](https://learn.microsoft.com/defender-endpoint/attack-surface-reduction)
- [Microsoft Defender Vulnerability Management](https://learn.microsoft.com/defender-endpoint/next-gen-threat-and-vuln-mgt)
- [Investigate alerts in Defender for Endpoint](https://learn.microsoft.com/defender-endpoint/investigate-alerts)

---

**Demo Status**: ✅ Ready for delivery  
**Last Updated**: November 11, 2025  
**Next Demo**: Demo F - Security Copilot Incident Investigation (Capstone)
