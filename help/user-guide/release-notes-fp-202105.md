---
title: Release Notes for Feature Pack 202105
description: "Follow this page to get information for AEM Screens Feature Pack 202105 released on June 04, 2021."
feature: Feature Pack
role: Developer
level: Intermediate
exl-id: fc210d9d-5fac-4147-849d-182ffbaf0a5e
---
# Release Notes for Feature Pack 202105 {#release-notes-for-feature-pack}

>[!CAUTION]
>It is recommended that you upgrade to the latest version of Adobe Experience Manager (AEM). Screens provides maintenance support for AEM 6.3 Screens platform.

## Availability {#availability}

AEM Screens released AEM 6.5 Feature Pack 8.

You can download the latest feature pack for AEM Screens 6.5.8 Release from the [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) using your Adobe ID. Navigate to **Adobe Experience Manager** tab and search for **Screens** to get the latest feature pack titled as **AEM 6.5 Screens FP8**.

## Release Date {#release-date}

The Release Date for AEM Screens Feature Pack 202105 is June 04, 2021.

### What's New {#what-is-new}

* **Locking Page in an AEM Screens Channel**

   AEM Screens now supporting *Locking a Page*, as already implemented in AEM Sites. Adobe Experience Manager (AEM) allows you to lock a page, so that no one else can modify the contents. This is useful when you are making a lot of edits to one specific page or when you need to freeze a page for a short while.

* **Naming AEM Screens Player Device**

   The AEM Screens players now include the capability of sending a device name to Adobe Experience Manager (AEM).
   By default, when bulk registration is used to register a device, a system generated username is entered in the title field. As an alternative, a customer may use an asset tag or other friendly name so it is visible in AEM and easier to assign appropriate content.
   
   Refer to the following documentation to learn how to configure the name in each supported Operating System:
    
   * [Android](/help/user-guide/implementing-android-player.md#name-android)
   * [Windows](/help/user-guide/implementing-windows-player.md#name-windows)
   * [Tizen](/help/user-guide/tizen-player.md#name-tizen)
   * [Chrome OS](/help/user-guide/implementing-chrome-os-player.md#name-chrome)

* **Manifest Generation**

   Faster channel manifest generation with improved performances such as allocating less resources on the server.

### Bug Fixes {#bug-fixes}

* Player displayed a black screen when switching to channel containing dynamic embedded sequence.
* The Screens players now block the switching to any broken channel that further avoids 404 error or a page with an error message.

### Released AEM Screens Players {#released-aem-screens-players}

The following AEM Screens Players are released for AEM 6.5 Feature Pack 8:

* ChromeOS
* Windows
* Tizen
* Android
* Linux

#### AEM Screens Player Downloads  {#aem-screens-player-downloads}

To download the latest AEM Screens player and learn more about the bug fixes, refer to **[AEM Screens Player Downloads](https://download.macromedia.com/screens/index.html)**.
