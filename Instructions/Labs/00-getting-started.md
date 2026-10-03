---
title: Get started with the MD-4011 labs
---

# Get started with the MD-4011 labs

These labs give you hands-on practice securing endpoints for the Contoso Healthcare scenario with Microsoft Intune, Conditional Access, and Microsoft Defender for Endpoint. They run in one Microsoft 365 tenant, and each lab builds on the one before it.

## Your lab environment

| Item | Detail |
| --- | --- |
| Tenant | A Microsoft 365 training tenant. Lab steps show its domain as `yourtenant.onmicrosoft.com`. |
| SEA-WS1 | A Windows workstation. In Lab 03, it's the corporate-owned device for policy filter testing. |
| SEA-WS2 | A second Windows workstation. In Lab 03, it's the personal device. |
| Lab files | The read-only **AllFiles (F:)** drive on both workstations. The current labs don't need any files from it. |

Open a workstation from the resource selector, workstation tabs, or virtual-machine list in your lab environment.

> [!NOTE]
> Sign in with the accounts and passwords provided in your lab environment. To find your tenant name, go to the Intune admin center and select **Tenant administration** > **Tenant status**.

## Accounts you use

- **Lab 01** starts with the Global Administrator (MOD Administrator) account provided in your lab environment. During Lab 01, you set up Diego Siciliani as an administrator.
- **From then on,** use Diego Siciliani's account for administrative tasks, as the labs direct. Don't use the Global Administrator account again.
- **Test users,** such as Alex Wilber and Allan Deyoung, enroll devices in Lab 02.

## How the labs work

- **Complete the labs in order.** Each lab requires the labs before it, so Lab 05 requires Labs 01 through 04.
- **Expect sync delays.** Device registration can take a few minutes, and policy sync typically takes 5 to 10 minutes after a manual sync. Initial compliance evaluation can take up to 24 hours. Sync a device manually instead of waiting for the scheduled sync.
- **Don't convert the trial.** The training tenant must not be converted to a paid subscription.

## The labs

{% assign course = site.data.course %}
{% for section in course.sections %}{% for group in section.groups %}
**{{ group.title }}**

{% for item in group.items %}- [{{ item.title }}]({{ item.url | relative_url }}){% if item.minutes %} ({{ item.minutes }} minutes){% endif %}
{% endfor %}
{% endfor %}{% endfor %}
When you're ready, start with Lab 01.
