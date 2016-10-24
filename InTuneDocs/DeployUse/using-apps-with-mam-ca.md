---
# required metadata

title: Using apps with MAM CA | Microsoft Intune
description: Understand the concepts of how MAM CA can help with controlling what apps have access to O365 services.
keywords:
author: karthikaraman
manager: angrobe
ms.date: 10/24/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 71dcf9bc-bfd1-4e06-b7ad-14b33a2288d0
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: chrisgre
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# What to expect when using an app with MAM CA
MAM CA verifies the identity of the approved application by means of a broker app that must be present on the device:
*  On **iOS**, the **Azure Authenticator app** is the broker app.
* On **Android**, the **Intune Company Portal app** is the broker app. 

End-users signing in for the first time, to an app that is supported by MAM CA, like OneDrive or Outlook, are prompted to install the broker app and register the device with Azure AD. Device registration in Azure AD (previously known as Workplace Join) will create a device record and certificate against which tokens are issued.  This is **not** the same as **MDM enrollment**. There are no management profiles or policies that are applied, and there is no inventory taken of apps on the device.  The process of installing the broker app and registering the device will only happen on the first use of a managed app.

The following is a list of properties  get recorded in Azure AD when a device is registered:

* accountEnabled
* approximateLastLogonTimeStamp
* deletionTimestamp
* deviceId
* deviceObjectVersion
* devicePhysicalIds
* dirSyncEnabled
* isCompliant
* IsManaged
* lastDirSyncTime
* objectId
* objectType




## MAM CA with conditional access based on device compliance  

You can configure [Conditional access based on device compliance](restrict-access-to-email-and-o365-services-with-microsoft-intune.md) (**Device CA**) on the [Intune administrator console](https://manage.microsoft.com) or the [Azure AD Premium management console] (https://manage.windowsazure.com). Device CA require users to connect to Exchange Online only through Intune-managed  devices that are compliant with the Intune device compliance policy or domain-joined PCs.  If a user belongs to one or more security groups that are targeted for both  MAM CA and Device CA policies, the user must meet one of the two requirements:
* The app used to access the service is a mobile app that is supported by MAM CA, and the device that the app is running on, has **iOS Authenticator (for iOS devices)**, or the **Company Portal app (for Android devices)** installed.
* The device used to access the service is **Intune-managed and compliant** with the Intune device compliance policy, or it is a **domain-joined PC**.  Here are some examples to help illustrate this:
  * If a user tries to connect from the **native iOS email app**, he or she will be required to be on a **managed and compliant device** since the native mail app is not supported by MAM CA.
  * If a user tries to connect from a **Windows home PC**, the **Device CA policy** will apply, requiring that the he or she must use a domain-joined PC.




## Next steps
[Create an Exchange Online Policy for MAM apps](mam-ca-for-exchange-online.md)

[Block apps that do not have modern authentication](block-apps-with-no-modern-authentication.md)

### See also

[Protect app data with MAM policies](protect-app-data-using-mobile-app-management-policies-with-microsoft-intune.md)