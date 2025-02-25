---
title: Multi-zone Layout
seo-title: Multi-zone Layout
description: Multi-zone Layout allows you to create multiple zone content and use a variety of assets such as videos, images and text that can be combined in a single screen. Follow this page to learn more.
seo-description: Multi-zone Layout allows you to create multiple zone content and use a variety of assets such as videos, images and text that can be combined in a single screen. Follow this page to learn more.
uuid: 2ad689ef-700a-4eed-b5e2-fc57f2288388
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/6.5/SCREENS
content-type: reference
topic-tags: authoring
discoiquuid: 4c073172-d93c-4b73-87ab-0b08789193a3
noindex: true
feature: Authoring Screens
role: Admin, Developer
level: Intermediate
exl-id: 901ed50e-d3f0-4c85-ad79-6c4595382759
---
# Multi-zone Layout {#multi-zone-layout}

The following page describes the usage of multi-zone layout and covers the following topics:

* Overview
* Creating Multi-zone Layout
* Prerequisites
* Using Single Assets in one or more Zones
* Using Sequenced Content in one or more Zones

## Overview {#overview}

***Multi-zone Layout*** allows you to create multiple zone content and use a variety of assets such as videos, images, and text that can be combined in a single screen. You can pull in images, videos, and text allowing it all to blend together and create an intuitive digital experience.

As per the project requirements, sometimes you need multiple zones in a channel and edit them as one comprehensive unit. For example, a product sequence with a related social media feed running in three separate zones on a single channel.


### Prerequisites {#prerequisites}

Before you start implementing this functionality, please make sure you have the conceptual knowledge on:

* [Creating an AEM Screens Project](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/authoring/setting-up-projects/creating-a-screens-project.html)
* [Creating a Display](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/authoring/setting-up-projects/managing-displays.html)
* [Assigning a Channel to a Display](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/authoring/setting-up-projects/channel-assignment.html)

## Creating Multi-zone Layout {#creating-multi-zone-layout}

While creating a channel, you can use different templates in order to create zones in your channel. You can add a single image, video, or an embedded channel which allows for multiple assets to be shown in a sequence.

**Creating a Channel**

1. Select the Adobe Experience Manager link (top left) and then **Screens**. Alternatively, you can ﻿go directly to: `http://localhost:4502/screens.html/content/screens`.
1. Navigate to **Channels** folder and click **Create** from the action bar.

1. Select **1x2 Split Screen Channel** from the **Create** wizard.

1. Click **Next** and enter the **title** as **MultiZone**.

1. Click **Create** to complete the channel creation.

### Using Single Assets in one or more Zones {#using-single-assets-in-one-or-more-zones}

You can use single assets such as an image or a video in all individual zones. Follow the steps below for implementation:

1. **Adding Content to the Channel**

    1. Navigate to **Zones** --&gt; **Channels**--&gt; **MultiZone**.
    1. Select the **MultiZone** channel and click **Edit** from the action bar to open the editor.

1. **Adding Images to the Channel**

   To play a single image or a video in two zones, simply drag and drop an image to each zone in the channel editor, as shown in the figure below:

   ![image](/help/user-guide/assets/multi-zone/multizone-img3.png)

### Using Sequenced Content in one or more Zones {#using-sequenced-content-in-one-or-more-zones}

If you want the zones to display sequence of images and a video in the different zones, follow steps below for details.

1. **Creating a Channel Folder**

    1. Navigate to **Zones** --&gt; **MultiZone** --&gt; **Channels** and click **Create** from the action bar.
    1. Select **Channels Folder** from the **Create** wizard and click **Next**.
    1. Enter the title as **EmbeddedChannels** and click **Create**.

   ![screen_shot_2018-12-19at125428pm](assets/screen_shot_2018-12-19at125428pm.png)

1. **Adding two more channels to Channel Folder**

    1. Navigate to **Zones** --&gt; **Channels** --&gt; **EmbeddedChannels** and click **Create** from the action bar.
    1. Select **Sequence Channel** from the **Create** wizard to create a channel titled as **Zone1**.
    1. Select **Zone1** and click **Edit** from the action bar to open the editor.
    1. Drag and drop few images to this channel.
    1. Similarly, create another sequence channel titled as **Zone2** in **EmbeddedChannels** folder.
    1. Drag and drop a video to this channel.

    The following figure shows the channels **Zone1** and **Zone2**:
   
   ![screen_shot_2018-12-19at125930pm](assets/screen_shot_2018-12-19at125930pm.png)

   The images added to editor of **Zone1** sequence channel are shown below:

   ![screen_shot_2018-12-19at125930pm](/help/user-guide/assets/multi-zone/multizone-img4.png)

   The video added to editor of **Zone2** sequence channel is shown below:

   ![screen_shot_2018-12-19at125930pm](/help/user-guide/assets/multi-zone/multizone-img5.png)

1. **Adding Embedded Sequences (component) to main channel (MultiZone)**

    1. Navigate to **Zones** --&gt; **Channels** --&gt; **MultiZone**.
    1. Click **Edit** from the action bar to open the editor.
    1. Drag and drop the **Embedded Sequence** component to both the zones.
    1. Select the embedded sequence in one of the zones.
    1. Click the **Configure** (wrench) icon to one of the embedded sequences in the editor.
    1. Select the channel path as **Zones** --&gt; **Channels** --&gt; **EmbeddedChannels** --&gt; **Zone1**, as shown in the figure below.
    1. Similarly, add the **Zone2** to another embedded sequence component in the editor. 

       ![image](/help/user-guide/assets/multi-zone/multizone-3.png)

### Creating a Location and a Display {#creating-location}

You must create a location and a display to view the content in the Screens player. Follow the steps below to create a location and a display.

1. **Creating a Location**

   1. Navigate to **Zones** --&gt; **Locations** folder.
   1. Select the **Locations** folder and click **Create** from the action bar.
   1. Select **Location** from the **Create** wizard and click **Next**.
   1. Enter the **Title** as **SanJose** and click **Create**.

1. **Creating a Display**

   1. Navigate to **Zones** --&gt; **Locations** folder.
   1. Select the **SanJose** location and click **Create** from the action bar.
   1. Select **Display** from the **Create** wizard and click **Next**.
   1. Enter the **Title** as **Lobby** and click **Create**.

### Assigning Channels to the Display {#channel-channel}

You must assign the channels to the display to view the content. Follow the steps below to assign the channel to the display.

1. **Assigning Channel to the Display**

   1. Navigate to **Zones** --&gt; **Locations** --&gt; **SanJose**--&gt; **Lobby**.
   1. Select the **Lobby** display and click **Assign Channel** from the action bar.
   1. Enter the path to the **MultiZone** channel in **Channel Path**.
   1. Set the **Supported Events** as **Initial Load**, **Idle Screen**, and **Timer**.
   1. Click **Save**.

      ![image](/help/user-guide/assets/multi-zone/multizone-img9.png)
   1. Similarly, you must assign the other two embedded channels (**Zone1** and **Zone2**) to this display.
   1. Once you assign all three channels to the **Lobby** display, you should be able to view the assigned channels from the display dashboard.

      ![image](/help/user-guide/assets/multi-zone/multizone-img8.png)

  
      >[!IMPORTANT]
      >
      > Once you assign the main channel (in this case, **MultiZone**) to the display, it is mandatory to assign the other two embedded channels **Zone1** and **Zone2** also to the same display.

### Registering the Device {#registering-device}

Once you have set up a location and a display, follow the steps below to register the device and assign display to the device.

1. **Registering the Device**

   1. Navigate to **Zones** --&gt; **Devices** folder.
   1. Select the **Devices** folder and click **Device Manager** from the action bar.
   1. Click **Device Registration** and select the pending device from the list.
      >[!NOTE]
      > The title of the device must match the device token (**Token** field) displayed in the **Device Registration** tab.
   1. If the title matches the device token, then select the device and click **Register Device** from the action bar.
   1. If the registration code matches the code in the Screens player **Device Registration** tab, click **Validate** from the action bar.
      ![image](/help/user-guide/assets/multi-zone/multizone-img6.png)
   1. Enter the **Title** as **Chrome-Device1** and click **Register**.
   1. Select **Assign Display** and select the path to the device config.

    >[!NOTE]
    >If you are trying to view the content in the Screens player, make sure you click **Update Offline Content** from the channel dashboard for each of the channels assigned to the display.

### Viewing the Result {#viewing-the-result}

Once you implement multi-zone layouts using the preceding steps, the following output displays.

Check the Screens player to view the output that displays the content in two different zones. The left and the right zones (both use embedded sequence as a component).

The left zone is a sequence channel and the right zone includes a video.

![new2-1](/help/user-guide/assets/multi-zone/Multi-gif.gif)
