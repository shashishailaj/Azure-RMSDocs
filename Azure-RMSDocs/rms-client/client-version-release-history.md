---
# required metadata

title: Azure Information Protection client - Version history & support policy
description: See what's new or changed in a release of the Azure Information Protection client for Windows, and understand the lifecycle policy for support. 
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection

# optional metadata

#ROBOTS:
#audience:git
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure Information Protection client: Version release history and support policy

>*Applies to: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions for: [Azure Information Protection client for Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

The Azure Information Protection team regularly updates the Azure Information Protection client for fixes and new functionality. 

You can download the latest general availability release version and the current preview version (if available) from the [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018). After a short delay of typically a couple of weeks, the latest general availability version is also included in the Microsoft Update Catalog (category: **Azure Information Protection**). This inclusion in the catalog means that you can upgrade the client by using WSUS or Configuration Manager, or other software deployment mechanisms that use Microsoft Update.

For more information, see [Upgrading and maintaining the Azure Information Protection client](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

> [!TIP]
> Interested in using the Azure Information Protection unified labeling client because your labels are published from the Office 365 Security & Compliance Center, Microsoft 365 security center, or Microsoft 365 compliance center? When you download and then install the unified labeling client from the Microsoft Download Center, you can upgrade your Azure Information Protection client to this [unified labeling client](unifiedlabelingclient-version-release-history.md).

### Servicing information and timelines

Each general availability (GA) version of the Azure Information Protection client is supported for up to six months after the release of the subsequent GA version. The documentation does not include information about unsupported versions of the client. Fixes and new functionality are always applied to the latest GA version and will not be applied to older GA versions.

Preview versions should not be deployed for end users on production networks. Instead, use the latest preview version to see and try new functionality or fixes that are coming in the next GA version. Preview versions that are not current are not supported.

### Release history

Use the following information to see what’s new or changed for a supported release of the Azure Information Protection client for Windows. The most current release is listed first. 

> [!NOTE]
> Minor fixes are not listed so if you experience a problem with the Azure Information Protection client, we recommend that you check whether it is fixed with the latest GA release. If the problem remains, check the current preview version (if available).
>  
> For technical support, see the [Support options and community resources](../information-support.md#support-options-and-community-resources) information. We also invite you to engage with the Azure Information Protection team, on their [Yammer site](https://www.yammer.com/askipteam/).

## Version 1.48.204.0

**Released**: 04/16/2019

This version includes the MSIPC version 1.0.3592.627 of the RMS client.

**New features:**

- The Azure Information Protection scanner is now configured from the Azure portal, rather than by using PowerShell.
    
    If you are upgrading from a general availability version of the scanner, the upgrade process is different from previous versions, so be sure to read [Upgrading the Azure Information Protection scanner](client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

- The scanner now supports multiple configuration databases on the same SQL server instance when you specify a profile name.

- Support for the following sensitive information types that help to identify credentials in documents and emails:
    - Azure Service Bus Connection String
    - Azure IoT Connection String
    - Azure Storage Account
    - Azure IAAS Database Connection String and Azure SQL Connection String
    - Azure Redis Cache Connection String
    - Azure SAS
    - SQL Server Connection String
    - Azure DocumentDB Auth Key
    - Azure Publish Setting Password
    - Azure Storage Account Key (Generic)

- New advanced client settings that implement pop-up messages in Outlook that can warn, justify, or block emails being sent. [More information](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    
    Note that if you configured the advanced client property of OutlookCollaborationTrustedDomains for the preview version, this setting is now replaced by three new settings, so that domains can be exempt per action: OutlookWarnTrustedDomains, OutlookJustifyTrustedDomains, and OutlookBlockTrustedDomains.

- If you label and protect files by using the [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) cmdlet, you can use the *EnableTracking* parameter to register the file with the document tracking site. [More information](client-admin-guide-document-tracking.md#using-powershell-to-register-labeled-documents-with-the-document-tracking-site)

- New advanced client setting that's applicable only when you configure the policy setting to not display custom permissions: When there's a file that's protected with custom permissions, display the custom permissions option in File Explorer so that users can see and change them (if they have permissions to change the protection settings). [More information](client-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)

- Endpoint discovery for [Azure Information Protection analytics](../reports-aip.md).
    
- Two new advanced client settings for analytics, for the following scenarios:
    
    - Prevent sending information type matches for a subset of users when you have selected the checkbox in the Azure portal to collect content matches. [More information](client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - For the **Data discovery** report, display whether files contain sensitive information. [More information](client-admin-guide-customizations.md#enable-azure-information-protection-analytics-to-discover-sensitive-information-in-documents)

**Fixes**:

- Paths and file names do not display question marks (**?**) instead of non-ASCII characters in Azure Information Protection analytics when the sending operating system locale is English.

- New visual markings are consistently applied when a user adds new sections to a Word document, and then relabels the document.

- The Azure Information Protection client correctly removes protection from a PDF document that was protected by the Rights Management sharing application.

- Sublabels are correctly applied by PowerShell and the scanner when the parent label is configured for user-defined permissions.

- The Azure Information Protection client correctly displays labels that have been applied by [clients that support unified labeling](../configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

- Documents open correctly in Office without a recovery message after protection has been removed by File Explorer and right-click, PowerShell, and the scanner.

- When you use the advanced client setting to set a [default label for Outlook](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook), you can apply a parent label that has sublabels when all those sublabels are disabled for the user.

- When you use the [policy setting](../configure-policy-settings.md) **For email messages with attachments, apply a label that matches the highest classification of those attachments** and the label with the highest classification is configured for user-defined permissions, the outcome previously was that the label was applied to the email, but the protection was not. Now:
    - When the label's user-defined permissions include Outlook (Do Not Forward): Apply that label and its Do Not Forward protection to the email.
    - When the label's user-defined permissions are just for Word, Excel, PowerPoint, and File Explorer: Do not apply the label and do not apply any protection to the email.

**Additional changes:**

- The following sensitive information types are no longer supported for labels that you configure for recommended or automatic classification:
    - EU Phone Number
    - EU GPS Coordinates

- Because the Azure Information Protections scanner is configured from the Azure portal, the following cmdlets are now deprecated and can't be used to configure data repositories or the file types list:
    - Add-AIPScannerRepository
    - Add-AIPScannerScannedFileTypes
    - Get-AIPScannerRepository
    - Remove-AIPScannerRepository
    - Remove-AIPScannerScannedFileTypes
    - Set-AIPScannerRepository
    - Set-AIPScannerScannedFileTypes

- A new PowerShell cmdlet, [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration), for scenarios where the Azure Information Protection scanner cannot download its configuration from the Azure portal.

- The Azure Information Protection scanner no longer excludes .zip files by default. To inspect and label .zip files, see the [To inspect .zip files](client-admin-guide-file-types.md#to-inspect-zip-files) section of the admin guide.

- The [policy setting](../configure-policy-settings.md) **Users must provide justification to set a lower classification label, remove a label, or remove protection** no longer applies to the scanner. The scanner performs these actions when you configure the setting **Relabel files** to **On** in the scanner profile.

## Version 1.41.51.0

**Released**: 11/27/2018

This version includes the MSIPC version 1.0.3592.627 of the RMS client.

**New features:**

- The Azure Information Protection client by default, now protects PDF files by using the ISO standard for PDF encryption. Previously, you had to enable this support with an advanced client setting.
    
    If you want the client to revert to protecting PDF files by using a .ppdf file name extension, use the same [advanced client setting](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), but specify **False**.

- Auditing data support for [central reporting](../reports-aip.md) by using Azure Information Protection analytics, announced at Microsoft Ignite 2018.

- Excel now also supports [visual marking](../configure-policy-markings.md)s in different colors.

- For existing S/MIME deployments, a new advanced client setting to configure a label to automatically apply S/MIME protection in Outlook. [More information](client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- A new advanced client setting, as an alternative to editing the registry to prevent sign-in prompts for the Azure Information Protection service for [disconnected computers](client-admin-guide-customizations.md#support-for-disconnected-computers).

- A new advanced client setting to [support the order of sublabels](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments) when you use the following policy setting:
    - **For email messages with attachments, apply a label that matches the highest classification of those attachments**

**Fixes**:

- The Azure Information Protection client no longer excludes .msg, .rar, and .zip file name extensions for File Explorer (right-click) and PowerShell commands. However, these file name extensions remain excluded by default for the scanner. 

- The Azure Information Protection client can unprotect multiple files (multi-select and a folder that contains protected files) when you use File Explorer, right-click.

- For Excel:
    
    - Visual markings are now applied if you save the spreadsheet while editing a cell.
    
    - Excel 2010: When a spreadsheet is protected by using the Co-Author [permission level](../configure-usage-rights.md#rights-included-in-permissions-levels), the **Delete Label** button is now available when you right-click the file and choose **Classify and Protect**.

- The advanced client settings that can [remove headers and footers from other labeling solutions](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions) now supports custom layouts.

**Additional changes:**

- When the scanner's schedule is set to **Always**, there is now a delay of 30 seconds between scans.

- The scanner no longer changes the Rights Management owner for files that it labels when the file is already protected.

## Version 1.37.19.0

**Released**: 09/17/2018

This version includes the MSIPC version 1.0.3592.627 of the RMS client.

**New features**: 

- Support for the ISO standard for PDF encryption, by configuring a new [advanced client configuration](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption). When this option is set to **True**, PDF documents that you protect retain their .pdf file name extension (rather than change to .ppdf) and can be opened by PDF readers that support this ISO standard. Currently, you must instruct users to open these protected PDFs manually by using the Azure Information Protection viewer. To help users do this, when they open one of these protected PDFs, they see a page with icons to select for their operating system.

- Support for new sensitive information types to help you classify documents that contain personal information. [More information](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- Labels that apply protection now display in Office 365 apps from Office 365 Business or Microsoft 365 Business when the user is assigned a license for Azure Rights Management (also known as Azure Information Protection for Office 365).

- Labeling support for **Strict Open XML Document** format in Word, Excel, and PowerPoint files. For more information about the Open XML formats, see the Office blog post, [New file format options in the new Office](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/). 

- Support for files that have been protected by Secure Islands when those files are other than PDF and Office documents. For example, protected text and picture files. Or, files that have a .pfile file name extension. This support enables new scenarios, such as the Azure Information Protection scanner being able to inspect these files for sensitive information, and automatically relabeling them for Azure Information Protection. [More information](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- New advanced client settings to remove headers and footers that have been applied to documents by other labeling solutions. [More information](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)

- For the Azure Information Protection scanner:

    - New cmdlet, [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner): Required to run once after upgrading from the previous GA version (1.29.5.0) or earlier.
    
    - New cmdlet, [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus): Gets the current status of the service for the scanner.  
    
    - New cmdlet, [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan): Instructs the scanner to start a one time scan cycle when the schedule is set to manual.
    
    - PDF documents are now protected by default when you use the ISO standard for PDF encryption.
    
    - SharePoint Server 2010 is supported for customers who have [extended support for this version of SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
- Support for the new **Azure Information Protection - Nodes (Preview)** blade in the Azure portal, that lets you manage scanners from a central location. Information from your deployed scanners that have connectivity to Azure is updated every five minutes. From this blade, you can start the scanner for a one-time scan, rescan all files, check the status of a scanner, and view the scan rate.

**Fixes**

- For the Azure Information Protection scanner:
    
    - For documents that are protected in SharePoint libraries, if the *DefaultOwner* parameter is not used for the data repository, the SharePoint Editor value is now used as the default value instead of the Author value.
    
    - Scanner reports include "Last modified by" for Office documents.
    
    - You can now protect all file types by using the `*` wildcard when you edit the registry as described in the [Editing the registry for the scanner](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner) section.

- Viewing emails by using the Next Item and Previous Item arrow icons on the Quick Access toolbar shows the correct label for each email.

- When you classify and protect by using File Explorer, PowerShell, or the scanner, the Office document metadata is not removed or encrypted.

- Custom permissions support recipient email addresses that contain an apostrophe.

- The computer environment will successfully initialize (bootstrap) when this action is initiated by opening a protected document that's stored in SharePoint Online.

- When you use the client for right-click in File Explorer, PowerShell, or the scanner, labeling is blocked for files in WebDav locations because this is an unsupported scenario.

- The Delete Label icon does not display in client apps (Word, Excel, PowerPoint, and Outlook) when you configure the [policy setting](../configure-policy-settings.md) of **All documents and emails must have a label**.

**Additional changes**:

- For [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration):
    
    - Values for the *Schedule* parameter are no longer **OneTime**, **Continuous**, and **Never**, but now **Manual** and **Always**.
        
    - The *Type* parameter is removed, so it is also removed from the output when you run [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration). By default, only new or modified files are inspected after the first scan cycle. If you previously set the *Type* parameter to **Full** to rescan all files, now run [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) with the *Reset* parameter. The scanner must also be configured for a manual schedule, which requires the *Schedule* parameter to be set to **Manual** with [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).
    
- The default exclusion list for the client and scanner now includes .msg, .rar, and .zip files. The scanner also excludes .rtf files. [More information](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- The policy version is changed to 1.4. Identifying the version number is required for [configuring disconnected computers](client-admin-guide-customizations.md#support-for-disconnected-computers).

- The **Send Us Feedback** link in the **Help and Feedback** dialog box is removed. It was temporarily replaced with **Report an Issue** that by default, sent an email to Microsoft. From December 2018 onward, the  **Report an Issue** option is not displayed by default but can be added with an [advanced client setting](client-admin-guide-customizations.md#add-report-an-issue-for-users) where you specify an HTTP string for the link. For example, a customized web page that you have for users to report issues, or an email address that goes to your help desk. 


## Next steps

For more information about installing and using the client: 

- For users: [Download and install the client](install-client-app.md)

- For admins: [Azure Information Protection client administrator guide](client-admin-guide.md)
