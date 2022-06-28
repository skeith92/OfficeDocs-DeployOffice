---
title: "Macros from the internet are blocked by default in Office "
ms.author: danbrown
author: DHB-MSFT
manager: dougeby
audience: ITPro
ms.topic: article
ms.service: o365-proplus-itpro
ms.localizationpriority: medium
ms.collection: Ent_O365
ms.custom: Ent_Office_Security
description: "Provides guidance for admins about how Office blocks macros in files from the internet."
---

# Macros from the internet will be blocked by default in Office

VBA macros are a common way for malicious actors to gain access to deploy malware and ransomware. Therefore, to help improve security in Office, we’re changing the default behavior of Office applications to block macros in files from the internet.

With this change, when users open a file that came from the internet, such as an email attachment, and that file contains macros, the following message will be displayed:

![Security risk banner about blocked macros with a Learn More button](../images/security/vba-security-risk-banner.png)

The **Learn More** button goes to an [article for end users and information workers](https://support.microsoft.com/topic/0952faa0-37e7-4316-b61d-5b5ed6024216) that contains information about the security risk of bad actors using macros, safe practices to prevent phishing and malware, and instructions on how to enable these macros (if absolutely needed).

> [!IMPORTANT]
> Organizations can use the [Block macros from running in Office files from the Internet](#block-macros-from-running-in-office-files-from-the-internet) policy to prevent users from inadvertently opening files from the internet that contain macros. We recommend enabling this policy as part of the [security baseline](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/bg-p/Microsoft-Security-Baselines) for Microsoft 365 Apps for enterprise. If you do enable the policy, your organization won’t be affected by this default change.
>
> For more information, see [Use policies to manage how Office handles macros](#use-policies-to-manage-how-office-handles-macros).

## Prepare for this change

To prepare for this change, we recommend that you work with the business units in your organization that use macros in their Office files, such as the Finance department, and with independent software vendors (ISVs) that you rely on who make use of macros in Office files.

Also, review the following information:

- [Versions of Office affected by this change](#versions-of-office-affected-by-this-change)
- [How Office determines whether to run macros in files from the internet](#how-office-determines-whether-to-run-macros-in-files-from-the-internet)
- [Use the Readiness Toolkit to identify files with VBA macros that might be blocked](#use-the-readiness-toolkit-to-identify-files-with-vba-macros-that-might-be-blocked)

There are several options available to you to allow VBA macros to run in files that you trust.

- Save files to a [Trusted Location](#trusted-locations).
- Designate a file server or network share as a [Trusted site](#trusted-sites).
- For [files on OneDrive or SharePoint](#files-on-onedrive-or-sharepoint) (including Teams channels), have users open files in the browser or by using the **Open in Desktop App** option.
- Have users clear the **Unblock** checkbox on the **General** tab of the **Properties** dialog for the file to make it a [Trusted Document](#mark-of-the-web-and-trusted-documents).

## Versions of Office affected by this change

This change only affects Office on devices running Windows and only affects the following applications: Access, Excel, PowerPoint, Visio, and Word.

The change will begin rolling out in Version 2203, starting with Current Channel (Preview) in early April 2022. Later, the change will be available in the other update channels, such as Current Channel and Monthly Enterprise Channel.

The following table shows the forecasted schedule of when this change will be available in each update channel. Information in italics is subject to change.

|Update channel  |Version  |Date  |
|---------|---------|---------|
|Current Channel (Preview)|Version 2203|Started rolling out on April 12, 2022|
|Current Channel|Version 2205|Started rolling out on June 6, 2022.|
|Monthly Enterprise Channel|*To be determined*|*July 2022*|
|Semi-Annual Enterprise Channel (Preview)|*To be determined*|*September 2022*|
|Semi-Annual Enterprise Channel |*To be determined*|*January 2023*|

At a future date to be determined, we also plan to make this change to volume licensed versions of Office LTSC 2021, Office 2019, Office 2016, and Office 2013.

The change doesn’t affect Office on a Mac, Office on Android or iOS devices, or Office on the web.

## How Office determines whether to run macros in files from the internet

The following flowchart graphic shows how Office determines whether to run macros in a file from the internet.

![Flowchart that shows how Office determines whether to run macros in files from the internet](../images/security/vba-macro-flowchart.png)

The following steps explain the information in the flowchart graphic, except for Excel Add-in files. For more information about those files, see [Macro-enabled add-in files for PowerPoint and Excel](#macro-enabled-add-in-files-for-powerpoint-and-excel).

1. A user opens an Office file containing macros obtained from the internet. For example, an email attachment. The file has Mark of the Web (MOTW).

> [!NOTE]
> - Mark of the Web is added by Windows to files from an untrusted location, such as the internet or Restricted Zone. For example, browser downloads or email attachments. 
> - Mark of the Web only applies to files saved on an NTFS file system, not files saved to FAT32 formatted devices.

2. If the file is from a Trusted Location, the file is opened with the macros enabled. If the file isn't from a Trusted Location, the evaluation continues.

3. If the macros are digitally signed and the matching Trusted Publisher certificate is installed on the device, the file is opened with the macros enabled. If not, then the evaluation continues.

4. Policies are checked to see if macros are allowed or blocked. If the policies are set to Not Configured, the evaluation continues to Step 6.

5. (a) If macros are blocked by policy, the macros are blocked. </br>
   (b) If the macros are enabled by policy, the macros are enabled.

6. If the user had previously opened the file, before this change in default behavior, and had selected **Enable content** from the Trust Bar, then the macros are enabled because the file is considered trusted.

> [!NOTE]
> - For more information, see [New security hardening policies for Trusted Documents](https://techcommunity.microsoft.com/t5/office-365-blog/new-security-hardening-policies-for-trusted-documents/ba-p/3023465). 
> - For perpetual versions of Office, such as Office LTSC 2021 or Office 2019, this step occurs after Step 3 and before Step 4, and isn’t affected by the change coming to Current Channel.

7. This step is where the change to the default behavior of Office takes effect. With this change, macros in files from the internet are blocked and users will see the **Security Risk** banner when they open the file.

> [!NOTE]
> Previously, before this change in default behavior, the app would check to see if the [VBA Macro Notification Settings](#vba-macro-notification-settings) policy was enabled and how it was configured.
>
> If the policy was set to Disabled or Not Configured, then the app would check the settings under **File** > **Options** > **Trust Center** > **Trust Center Settings...** > **Macro Settings**. The default is set to "Disable all macros with notification," which allows users to enable content in the Trust Bar.

## Use policies to manage how Office handles macros

You can use policies to manage how Office handles macros. We recommend that you use the [Block macros from running in Office files from the Internet](#block-macros-from-running-in-office-files-from-the-internet) policy. But if that policy isn't appropriate for your organization, the other option is the [VBA Macro Notification Settings](#vba-macro-notification-settings) policy.

For more information on how to deploy these policies, see [Tools available to manage policies](#tools-available-to-manage-policies).

> [!IMPORTANT]
> You can only use policies if you're using Microsoft 365 Apps for enterprise. Policies aren't available for Microsoft 365 Apps for business.

### Block macros from running in Office files from the Internet

This policy prevents users from inadvertently opening files containing macros from the internet. When a file is downloaded to a device running Windows, Mark of the Web is added to the file identifying it was sourced from the internet.

We recommend enabling this policy as part of the [security baseline](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/bg-p/Microsoft-Security-Baselines) for Microsoft 365 Apps for enterprise. You should enable this policy for most users and only make exceptions for certain users as needed.

There's a separate policy for each of the five applications. The following table shows where each policy can be found in the Group Policy Management Console under User Configuration\Policies\Administrative Templates:

|Application|Policy location |
|---------|---------|
|Access|Microsoft Access 2016\Application Settings\Security\Trust Center|
|Excel|Microsoft Excel 2016\Excel Options\Security\Trust Center|
|PowerPoint|Microsoft PowerPoint 2016\PowerPoint Options\Security\Trust Center|
|Visio|Microsoft Visio 2016\Visio Options\Security\Trust Center|
|Word|Microsoft Word 2016\Word Options\Security\Trust Center|

Which state you choose for the policy determines the level of protection you're providing. The following table shows the current level of protection you get with each state, before the change in default behavior is implemented.

|Icon|Protection level|Policy state|Description|
|-----|---------|---------|---------|
|![Green circle with white check mark](../images/security/icon-protected.png)| Protected **[recommended]**|Enabled |Users will be blocked from running macros in files obtained from the internet. <br/><br/>Part of the Microsoft recommended security baseline. |
|![Red circle with white X](../images/security/icon-not-protected.png)| Not protected|Disabled| Will respect the settings configured under **File** > **Options** > **Trust Center** > **Trust Center Settings...** > **Macro Settings**.         |
|![Red circle with white X](../images/security/icon-not-protected.png)| Not protected |Not Configured| Will respect the settings configured under **File** > **Options** > **Trust Center** > **Trust Center Settings...** > **Macro Settings**.            |

After we implement the change to the default behavior, the level of protection changes when the policy is set to Not Configured.

|Icon|Protection level|Policy state|Description|
|---|---------|---------|---------|
|![Green circle with white check mark](../images/security/icon-protected.png)|Protected |Not Configured| Users will be blocked from running macros in files obtained from the internet.<br/><br/> Users will see the Security Risk banner with a Learn More button |

### VBA Macro Notification Settings

If you don't use the "Block macros from running in Office files from the Internet" policy, you can use the "VBA Macro Notification Settings" policy to manage how macros are handled by Office.

This policy prevents users from being lured into enabling malicious macros. By default, Office is configured to block files that contain VBA macros and display a Trust Bar with a warning that macros are present and have been disabled. Users can inspect and edit the files if appropriate, but can’t use any disabled functionality until they select **Enable Content** on the Trust Bar. If the user selects **Enable Content**, then the file is added as a Trusted Document and macros are allowed to run.

There's a separate policy for each of the five applications. The following table shows where each policy can be found in the Group Policy Management Console under User Configuration\Policies\Administrative Templates:

|Application|Policy location |
|---------|---------|
|Access|Microsoft Access 2016\Application Settings\Security\Trust Center|
|Excel <sup>[1]</sup>|Microsoft Excel 2016\Excel Options\Security\Trust Center|
|PowerPoint|Microsoft PowerPoint 2016\PowerPoint Options\Security\Trust Center|
|Visio|Microsoft Visio 2016\Visio Options\Security\Trust Center|
|Word|Microsoft Word 2016\Word Options\Security\Trust Center|

> [!NOTE]
> - <sup>[1]</sup> For Excel, the policy is named Macro Notification Settings.
>- The "VBA Macro Notification Settings" policy is also available for Project and Publisher.

Which state you choose for the policy determines the level of protection you're providing. The following table shows the level of protection you get with each state.

|Icon|Protection level|Policy state|Policy value|
|--------|---------|---------|---------|
|![Green circle with white check mark](../images/security/icon-protected.png)|Protected **[recommended]** |Enabled|Disable all except digitally signed macros (and select "Require macros to be signed by a trusted publisher")|
|![Green circle with white check mark](../images/security/icon-protected.png)|Protected |Enabled|Disable all without notification |
|![Orange circle with white check mark](../images/security/icon-partially-protected.png)|Partially protected |Enabled|Disable all with notification |
|![Orange circle with white check mark](../images/security/icon-partially-protected.png)|Partially protected|Disabled|*(Same behavior as "Disable all with notification")*|
|![Red circle with white X](../images/security/icon-not-protected.png)|Not protected|Enabled|Enable all macros (not recommended) |

> [!IMPORTANT]
> Securing macros is important. For users that don't need macros, turn off all macros by choosing "Disable all without notification."
>
> Our security baseline recommendation is that you should do the following:
> - Enable the "VBA Macro Notification Settings" policy.
> - For users that need macros, choose "Disable all except digitally signed macros" and then select "Require macros to be signed by a trusted publisher." The certificate needs to be installed as a Trusted Publisher on users' devices.

If you don't configure the policy, users can configure macro protection settings under **File** > **Options** > **Trust Center** > **Trust Center Settings...** > **Macro Settings**.

The following table shows the choices users can make under **Macro Settings** and the level of protection each setting provides.

|Icon|Protection level|Setting chosen|
|----|---------|---------|
|![Green circle with white check mark](../images/security/icon-protected.png)|Protected |Disable all macros except digitally signed macros|
|![Green circle with white check mark](../images/security/icon-protected.png)|Protected |Disable all macros without notification|
|![Orange circle with white check mark](../images/security/icon-partially-protected.png)|Partially protected |Disable all macros with notification *(default)*|
|![Red circle with white X](../images/security/icon-not-protected.png)| Not protected|Enable all macros (not recommended; potentially dangerous code can run)|

> [!NOTE]
> In the policy setting values and the product UI for Excel, the word "all" is replaced by "VBA."  For example, "Disable VBA macros without notification."

## Tools available to manage policies

There are several tools available to you to configure and deploy policy settings to users in your organization.

- [Office cloud policy service](#office-cloud-policy-service)
- [Microsoft Endpoint Manager admin center](#microsoft-endpoint-manager-admin-center)
- [Group Policy Management Console](#group-policy-management-console)

### Office cloud policy service

You can use the Office cloud policy service to configure and deploy policy settings to devices in your organization, even if the device isn't domain joined. The Office cloud policy service is a web-based tool and is found in the [Microsoft 365 Apps admin center](https://config.office.com).

In the Office cloud policy service, you create a policy configuration, assign it to a group, and then select policies to be included in the policy configuration. To select a policy to include, you can search by the name of the policy. The Office cloud policy service also shows which policies are part of the Microsoft recommended security baseline. The policies available in the Office cloud policy service are the same User Configuration policies that are available in the Group Policy Management Console.

For more information, see [Overview of the Office cloud policy service for Microsoft 365 Apps for enterprise](../admincenter/overview-office-cloud-policy-service.md).

### Microsoft Endpoint Manager admin center

In the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com), you can use either the Settings catalog (preview) or Administrative Templates to configure and deploy policy settings to your users for devices running Windows 10 or later.

To get started, go to **Devices** > **Configuration profiles** > **Create profile**. For **Platform**, choose **Windows 10 and later** and then choose the profile type.

For more information, see the following articles:
- [Use the settings catalog to configure settings on Windows and macOS devices - preview](/mem/intune/configuration/settings-catalog)
- [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](/mem/intune/configuration/administrative-templates-windows)

### Group Policy Management Console

If you have Windows Server and Active Directory Domain Services (AD DS) deployed in your organization, you can configure policies by using Group Policy. To use Group Policy, download the most current [Administrative Template files (ADMX/ADML) for Office](https://www.microsoft.com/download/details.aspx?id=49030), which include the policy settings for Microsoft 365 Apps for enterprise. After you copy the Administrative Template files to AD DS, you can use the Group Policy Management Console to create Group Policy Objects (GPOs) that include policy settings for your users, and for domain joined devices.

## Additional information

### Mark of the Web and Trusted Documents

When a file is downloaded to a device running Windows, Mark of the Web is added to the file, identifying its source as being from the internet. Currently, when a user opens a file with Mark of the Web, a **SECURITY WARNING** banner appears, with an **Enable content** button. If the user selects **Enable content**, the file is considered a Trusted Document and macros are allowed to run. The macros will continue to run even after the change of default behavior to block macros in files from the internet is implemented, because the file is still considered a Trusted Document.

After the change of default behavior to block macros in files from the internet, users will see a different banner the first time they open a file with macros from the internet. This **SECURITY RISK** banner doesn't have the option to **Enable content**. But users will be able to go to the Properties dialog for the file, and select **Unblock**, which will remove Mark of the Web from the file and allow the macros to run, as long as no policy or Trust Center setting is blocking.

![File properties dialog showing the choice to unblock](../images/security/vba-unblock-file-properties.PNG)

> [!TIP]
> You can also use the Unblock-File cmdlet in PowerShell to unblock files. For more information, see [Mark of the Web and zones](#mark-of-the-web-and-zones).

### Trusted Locations

Saving files from the internet to a Trusted Location ignores the check for Mark of the Web and opens with VBA macros enabled. For example, a line of business application could send reports with macros on a recurring basis. If files with macros are saved to a Trusted Location, users won't need to go to the Properties for the file and select **Unblock** to allow the macros to run. Trusted Locations should be managed carefully and used sparingly. For more information, see [Trusted Locations for Office files](trusted-locations.md).

### Trusted sites

Files that are from a trusted site will ignore the check for Mark of the Web and their VBA macros will be enabled when those files are opened. To see a list of trusted sites on a Windows device, go to **Control Panel** > **Internet Options** > **Change security settings**. For example, you could add a file server or network share as a trusted site, by adding its FQDN or IP address to the list of trusted sites.

You can use Group Policy and the "Site to Zone Assignment List" policy to add locations as trusted sites to Windows devices in your organization. This policy is found under Windows Components\Internet Explorer\Internet Control Panel\Security Page in the Group Policy Management Console. It’s available under both Computer Configuration\Policies\Administrative Templates and User Configuration\Policies\Administrative Templates.

To check if an individual file is from a trusted site location, see [Mark of the Web and zones](#mark-of-the-web-and-zones).

### Files on OneDrive or SharePoint

- If a user downloads a file on OneDrive or SharePoint by using a web browser, the configuration of the Windows internet security zone (**Control Panel** > **Internet Options** > **Security**) will determine whether the browser sets Mark of the Web. For example, Microsoft Edge sets Mark of the Web on a file if it's determined to be from the Internet zone.

- If a user selects **Open in Desktop App** in a file opened from the OneDrive website or from a SharePoint site (including a site used by a Teams channel), then the file won't have Mark of the Web.

- If a user has the OneDrive sync client running and the sync client downloads a file, then the file won't have Mark of the Web.

- Files that are in Windows known folders (Desktop, Documents, Pictures, Screenshots, and Camera Roll), and are synced to OneDrive, don't have Mark of the Web.

- If you have a group of users, such as the Finance department, that need to use files from OneDrive or SharePoint without macros being blocked, here are some possible options:

  - Have them open the file in the browser or by using the **Open in Desktop App** option

  - Have them download the file to a [Trusted Location](trusted-locations.md).

  - Set the Windows internet security zone assignment for OneDrive or SharePoint domains to Trusted Sites. Admins can use the "Site to Zone Assignment List" policy and configure the policy to place `https://{your-domain-name}.sharepoint.com` (for SharePoint) or `https://{your-domain-name}-my.sharepoint.com` (for OneDrive) into the Trusted Sites zone.

     - This policy is found under Windows Components\Internet Explorer\Internet Control Panel\Security Page in the Group Policy Management Console. It’s available under both Computer Configuration\Policies\Administrative Templates and User Configuration\Policies\Administrative Templates.

     - SharePoint permissions and OneDrive sharing aren't changed by adding these locations to Trusted Sites. Maintaining access control is important. Anyone with permissions to add files to SharePoint could add files with active content, such as macros. Users who download files from domains in the Trusted Sites zone will bypass the default to block macros.

### Macro-enabled template files for Word, PowerPoint, and Excel

Macro-enabled template files for Word, PowerPoint, and Excel that are downloaded from the internet will have Mark of the Web. For example, template files with the following extensions:
- .dot
- .dotm
- .pot
- .potm
- .xlt
- .xltm

When the user opens the macro-enabled template file, the user will be blocked from running the macros in the template file. If the user trusts the source of the template file, they can remove Mark of the Web from the template file, and then reopen the template file in the Office app.

If you have a group of users that need to use macro-enabled templates without macros being blocked, you can take either of the following actions:
- Use a digital signature and trust the publisher.
- If you're not using digital signatures, you can save the template file to a [Trusted Location](trusted-locations.md) and have users get the template file from that location.

### Macro-enabled add-in files for PowerPoint and Excel

Macro-enabled Add-in files for PowerPoint and Excel that are downloaded from the internet will have Mark of the Web. For example, Add-in files with the following extensions:

- .ppa
- .ppam
- .xla
- .xlam

When the user tries to install the macro-enabled Add-in, by using **File** > **Options** > **Add-ins** or by using the **Developer** ribbon, the Add-in will be loaded in a disabled state and the user will be blocked from using the Add-in. If the user trusts the source of the Add-in file, they can remove Mark of the Web from the Add-in file, and then reopen PowerPoint or Excel to use the Add-in.

If you have a group of users that need to use macro-enabled Add-in files without macros being blocked, you can take the following actions.

For PowerPoint Add-in files:
- Use a digital signature and trust the publisher.
- Save the Add-in file to a [Trusted Location](trusted-locations.md) for users to retrieve.

For Excel Add-in files:
- Remove Mark of the Web from the .xla or .xlam file.
- Save the Add-in file to a [Trusted Location](trusted-locations.md) for users to retrieve.

> [!NOTE]
> Using a digital signature and trusting the publisher doesn't work for Excel Add-in files that have Mark of the Web. This behavior isn't new for Excel Add-in files that have Mark of the Web. It's worked this way since 2016, as a result of a previous security hardening effort (related to Microsoft Security Bulletin MS16-088).

### Mark of the Web and zones

By default, Mark of the Web is added to files from locations in the following zones:

- Trusted sites
- Internet
- Restricted sites

But, VBA macros in a file with Mark of the Web are only blocked by default if the zone for the file is identified as being Internet or Restricted sites. If the zone for the file is identified as being Trusted sites, the macros in the file with Mark of the Web aren't blocked by default.

You can view the ZoneId value for a file by running the following command at a command prompt, and replacing *{name of file}* with your file name.

```console
notepad {name of file}:Zone.Identifier
```

When you run this command, Notepad will open and display the ZoneId under the [ZoneTransfer] section.

Here's a list of ZoneId values and what zone they map to.

- 0 = My Computer
- 1 = Local intranet
- 2 = Trusted sites
- 3 = Internet
- 4 = Restricted sites

For example, if the ZoneID is 2, VBA macros in that file won't be blocked by default. But if the ZoneID is 3, macros in that file will be blocked by default.

You can use the [Unblock-File](/powershell/module/microsoft.powershell.utility/unblock-file) cmdlet in PowerShell to remove the ZoneID value from the file. Removing the ZoneID value will allow VBA macros to run by default. Using the cmdlet does the same thing as clearing the **Unblock** checkbox on the **General** tab of the **Properties** dialog for the file.

### Use the Readiness Toolkit to identify files with VBA macros that might be blocked

To identify files that have VBA macros that might be blocked from running, you can use the Readiness Toolkit for Office add-ins and VBA, which is a free download from Microsoft.

The Readiness Toolkit includes a standalone executable that can be run from a command line or from within a script. You can run the Readiness Toolkit on a user's device to look at files on the user's device. Or you can run it from your device to look at files on a network share.

When you run the standalone executable version of the Readiness Toolkit, a JSON file is created with the information collected. You'll want to save the JSON files in a central location, such as a network share. Then you'll run the Readiness Report Creator, which is a UI wizard version of the Readiness Toolkit. This wizard will consolidate the information in the separate JSON files into a single report in the form of an Excel file.

To identify files that might be impacted by using the Readiness Toolkit, follow these basic steps:

1. [Download the most current version](https://www.microsoft.com/download/details.aspx?id=55983) of the Readiness Toolkit from the Microsoft Download Center. Make sure you're using at least Version 1.2.22161, which was released on June 14, 2022.
2. Install the Readiness Toolkit.
3. From a command prompt, go to the folder where you installed the Readiness Toolkit and run the ReadinessReportCreator.exe command with the blockinternetscan option. 

   For example, if you want to scan files in the c:\officefiles folder (and all its subfolders) on a device and save the JSON file with the results to the Finance share on Server01, you can run the following command.

```console
ReadinessReportCreator.exe -blockinternetscan -p c:\officefiles\ -r -output \\server01\finance -silent
```

4. After you've done all your scans, run the Readiness Report Creator.
5. On the **Create a readiness report page**, select **Previous readiness results saved together in a local folder or network share**, and then specify the location where you saved all the files for the scans.
6. On the **Report settings** page, select **Excel report**, and then specify a location to save the report.
7. When you open the report in Excel, go to the **VBA Results** worksheet.
8. In the **Guideline** column, look for **Blocked VBA file from Internet**.

For more detailed information about using the Readiness Toolkit, see [Use the Readiness Toolkit to assess application compatibility for Microsoft 365 Apps](../readiness-toolkit-application-compatibility-microsoft-365-apps.md).

## Related articles

- [Macro malware](/windows/security/threat-protection/intelligence/macro-malware)
- [Understanding malware & other threats](/windows/security/threat-protection/intelligence/understanding-malware)
- [How to protect against phishing attacks](/windows/security/threat-protection/intelligence/phishing)
- [Manage active content in Office documents](/microsoft-365/security/active-content-in-trusted-docs)
- [Add, remove, or change a trusted location](https://support.microsoft.com/office/7ee1cdc2-483e-4cbb-bcb3-4e7c67147fb4)
- [Trusted document settings have changed](https://support.microsoft.com/topic/0be30e4c-926a-4761-bdef-3f91097beb5a)
