---
title: Implementing Android Player
seo-title: Implementation of Android Player
description: Follow this page to learn implementation of Android Watchdog, a solution to recover the player from crashes.
seo-description: Follow this page to learn implementation of Android Watchdog, a solution to recover the player from crashes.
uuid: 17edd093-f1b1-479e-9f25-28c64f1a7223
contentOwner: Jyotika syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SCREENS
topic-tags: administering
discoiquuid: 77fe9d4e-e1bb-42f7-b563-dc03e3af8a60
docset: aem65
feature: Administering Screens, Android Player
role: Admin
level: Intermediate
exl-id: d1331cb8-8bf6-4742-9525-acf18707b4d8
---
# Implementing Android Player {#implementing-android-player}

This section describes configuring Android player. It provides information of the configuration file and the options available and recommendations as to which settings to use for development and testing.

Additionally, **Watchdog** is a solution to recover the player from crashes. An application needs to register itself with the watchdog service and then periodically send messages to the service that it is alive. In case the watchdog service does not receive a keep-alive message within a stipulated time, the service attempts to reboot the device for a clean recovery (if it has the sufficient privileges) or restart the application.

## Installing Android Player {#installing-android-player}

To implement Android Player for AEM Screens, please install Android Player for AEM Screens.

Visit the [**AEM 6.5 Player Downloads**](https://download.macromedia.com/screens/) page.

### Setting up Environment for AEM Screens 6.5.5 Service Pack {#fp-environment-setup}

>[!NOTE]
>You must set up an environment for Android player if you are using AEM Screens 6.5.5 Service Pack.

Set the **SameSite attribute for the login-token cookies** from **Lax** to **None** from **Adobe Experience Manager Web Console Configuration** on all AEM author and publish instances.

Follow the steps below:

1. Navigate to **Adobe Experience Manager Web Console Configuration** using `http://localhost:4502/system/console/configMgr`.

1. Search for *Adobe Granite Token Authentication Handler*.

1. Set the **SameSite attribute for the login-token cookies** from **Lax** to **None**.
   ![image](/help/user-guide/assets/granite-updates.png)

1. Click **Save**.


### Ad-Hoc Method {#ad-hoc-method}

The Ad-Hoc method allows you to install the latest Android Player (*.exe*). Visit [**AEM 6.5 Player Downloads**](https://download.macromedia.com/screens/) page.

Once you download the application, follow the steps on the player to complete the ad-hoc installation:

1. Long-press on the top left corner to open the admin panel.
1. Navigate to **Configuration** from the left action menu and enter the location (address) of the AEM instance you wish to connect to and click **Save**.

1. Navigate to the **Device** **Registration** link from the left action menu to check the status of the device registration process.

>[!NOTE]
>
>If the **State** is **REGISTERED**, you will notice the **Device id** field will be populated.
>
>If the **State** is **UNREGISTERED**, you can use the **Token** to register the device.

## Implementing Android Watchdog {#implementing-android-watchdog}

Due to Android's architecture, rebooting the device requires that the application has system privileges. To do this, you need to sign the apk using the manufacturer's signing keys, otherwise watchdog will restart the player application and not reboot the device.

### Signage of Android apks using Manufacturer Keys {#signage-of-android-apks-using-manufacturer-keys}

To access some of the privileged APIs of Android such as *PowerManager* or *HDMIControlServices*, you need to sign the android apk using the manufacturer's keys.

>[!CAUTION]
>
>Pre-requisites:
>
>You should have the android SDK installed, before you perform the following steps.

Follow the steps below to sign the android apk using the manufacturer's keys:

1. Download the apk from Google Play or from [AEM Screens Player Downloads](https://download.macromedia.com/screens/) page
1. Obtain the platform keys from the manufacturer to get a *pk8* and a *pem* file

1. Locate the apksigner tool in android sdk using find ~/Library/Android/sdk/build-tools -name "apksigner"
1. &lt;pathto&gt; /apksigner sign --key platform.pk8 --cert platform.x509.pem aemscreensplayer.apk
1. Find the path to the zip align tool in android sdk
1. &lt;pathto&gt; /zipalign -fv 4 aemscreensplayer.apk aemscreensaligned.apk
1. Install ***aemscreensaligned.apk*** using adb install to the device

## Understanding Android Watchdog Services {#android-watchdog-services}

The cross-Android watchdog service is implemented as a cordova plugin using *AlarmManager*.

The following diagram shows the implementation of watchdog service:

![chlimage_1-31](assets/chlimage_1-31.png)

**1. Initialization** At the time of initialization of the cordova plugin, permissions are checked to see if we have system privileges and thus the Reboot permission. If these two criteria are met, a pending Intent for Reboot is created, otherwise a pending Intent to restart the application (based on its Launch Activity) is created.

**2. Keep Alive Timer** A keep alive timer is used to trigger an event every 15 seconds. In that event, you need to cancel the existing pending intent (to reboot or restart the app) and register a new pending intent for the same 60 seconds in the future (essentially postponing reboot).

>[!NOTE]
>
>In Android, the *AlarmManager* is used to register the *pendingIntents* that can execute even if the app has crashed and its alarm delivery is inexact from API 19 (Kitkat). Keep some spacing between the timer's interval and the *AlarmManager's* *pendingIntent's* alarm.

**3. Application Crash** In case of a crash, the pendingIntent for Reboot registered with AlarmManager is no longer reset and thus it executes a reboot or restart of app (depending on permissions available at the time of initialization of the cordova plugin).

## Bulk Provisioning of Android Player {#bulk-provision-android-player}

When rolling out the Android player in bulk, there is a need to provision the player to point to an AEM instance as well as configure other properties without manually entering those in the Admin UI. 

>[!NOTE]
>This feature is available from Android player 42.0.372.

Follow the steps below to allow bulk provisioning in the Android player:

1. Create a configuration JSON file with the name `player-config.default.json`. 
   Refer to a [Example JSON Policy](#example-json) as well as a table that describes the use of the various [Policy Attributes](#policy-attributes).

1. Use an MDM or ADB or Android Studio file explorer to drop this policy JSON file to the *sdcard* folder on the Android device. 

1. Once the file is deployed, use the MDM to install the player application.

1. When the player application launches, it will read this configuration file and point to the applicable AEM server where it can be registered and subsequently controlled.

   >[!NOTE]
   >This file is *read only* the first time the application is launched and cannot be used for subsequent configurations. If the player is launched before the configuration file was dropped, simply uninstall and re-install the application on the device.

### Policy Attributes {#policy-attributes}

The following table summarizes the policy attributes with an example policy JSON for reference:

| **Policy Name** |**Purpose** |
|---|---|
| *server* |The URL to the Adobe Experience Manager server. |
| *resolution* |The resolution of the device. |
| *rebootSchedule* |The schedule to reboot applies to all platforms. |
| *enableAdminUI* |Enable the Admin UI to configure the device on site. Set to *false* once it is fully configured and in production. |
| *enableOSD* |Enable the channel switcher UI for users to switch channels on device. Consider setting to *false* once it is fully configured and in production. |
| *enableActivityUI* |Enable to show progress of activities such as download and sync. Enable for troubleshooting and disable once it is fully configured and in production. |
| *enableNativeVideo* |Enable to use native hardware acceleration for video playback (Android only). |

### Example JSON Policy {#example-json}

```java
{
  "server": "https://author-screensdemo.adobecqms.net",
"device": "",
"user": "",
"password": "",
"resolution": "auto",
"rebootSchedule": "at 4:00 am",
"maxNumberOfLogFilesToKeep": 10,
"logLevel": 3,
"enableAdminUI": true,
"enableOSD": true,
"enableActivityUI": false,
"enableNativeVideo": false,
"enableAutoScreenshot": false,
"cloudMode": false,
"cloudUrl": "https://screens.adobeioruntime.net",
"cloudToken": "",
"enableDeveloperMode": true
}
```

>[!NOTE]
>All Android devices have an *sdcard* folder whether an actual *sdcard* is inserted or not. This file when deployed would be at the same level as the Downloads folder. Some MDMs such as Samsung Knox may refer to this *sdcard* folder location as *Internal storage*.

## Bulk Provisioning of Android Player using Enterprise Mobility Management {#bulk-provisioning}

When deploying the Android player in bulk, it becomes tedious to manually register every single player with AEM. It is highly recommended to use an EMM (Enterprise Mobility Management) solution such as VMWare Airwatch, MobileIron or Samsung Knox to remotely provision and manage your deployment. AEM Screens Android player supports the industry standard EMM AppConfig to allow for remote provisioning. 

## Naming Android Player {#name-android}

You can assign a user friendly device name to your Android player, thereby sending the assigned device name to Adobe Experience Manager (AEM). This capability not only allows you to name your Android player but also allows to you to easily assign appropriate content.

>[!NOTE]
>You can choose the Player name only before registration. Once the Player is registered, the Player name cannot be changed anymore.

Follow the steps below to configure the name in Android player:

1. Navigate to **settings** --> **About device** 
1. Edit and set your device name to name your Android player

### Implementing Bulk Provisioning of Android Player using Enterprise Mobility Management {#implementation}

Follow the steps below to allow bulk provisioning in Android Player:

1. Ensure your Android device supports Google Play services.
1. Enroll your Android player devices with your favorite EMM solution that supports AppConfig. 
1. Log into your EMM console and pull the AEM Screens Player application from Google Play.
1. Select managed configuration or related option.
1. You should now see a list of player options that can be configured, such as server and bulk registration code.
1. Configure these parameters, save, and deploy the policy to the devices.

   >[!NOTE]
   >The devices should receive the application along with the configuration and point to the correct AEM server with the selected configuration. If you chose to configure the bulk registration code and kept it the same as configured in AEM, the player should be able to automatically register itself. If you had configured a default display, it can also download and show some default content (which can later be changed as per your convenience).

Additionally, you should check with your EMM vendor on AppConfig support. Most popular ones such as [VMWare Airwatch](https://docs.samsungknox.com/admin/uem/vm-configure-appconfig.htm), [Mobile Iron](https://docs.samsungknox.com/admin/uem/mobileiron2-configure-appconfig.htm), [SOTI](https://docs.samsungknox.com/admin/uem/soti-configure-appconfig.htm), [Blackberry UEM](https://docs.samsungknox.com/admin/uem/bb-configure-appconfig.htm), [IBM Maas360](https://docs.samsungknox.com/admin/uem/ibm-configure-appconfig.htm) and [Samsung Knox](https://docs.samsungknox.com/admin/uem/km-configure-appconfig.htm) among others support this industry standard.
