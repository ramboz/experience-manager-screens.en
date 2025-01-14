---
title: Channel Level Activation - Single Event Playback
seo-title: Channel Level Activation - Single Event Playback
description: Follow this guide to understand channel level activation using single event playback.
topic-tags: authoring
feature: Authoring Screens, Channels
role: Admin, Developer
level: Intermediate
exl-id: 51a63429-2488-45be-b8f5-cb755ca69c7f
---
# Channel Level Activation {#channel-level-activation-single-event-playback}

This page describes channel level activation for the assets used in Channels.

The following topics are covered in this section:

* Overview
* Activation Window
* Using Channel Level Activation as a Single Event Playback
* Handling Recurrence for Assets in a Channel 
   * DayParting
   * WeekParting
   * MonthParting
   * Combination of Partings
* Using Channel Level Activation as a Single Event Playback

## Overview {#overview}

***Channel Level Activation*** allows the channels to switch after a particular set schedule. The single event channel replaces the main channel after a set schedule and plays for a particular time, until the main channel plays its content again.

The following example provides a solution by focusing on the following key terms:

* a ***main sequence channel*** for the global sequence
* a ***single event channel*** that runs only once at a set time
* a ***set schedule and priority*** for the single playback event that occurs inside the main sequence channel

## Activation Window {#using-channel-level-activation}

The following section explains the creation of a single event playback inside a channel for an AEM Screens project.

### Prerequisites {#prerequisites}

Before you start implementing this functionality, please make sure you have the following prerequisites ready to start implementing channel level activation:

* Create an AEM Screens project, in this example, **Channel Level Activation**

* Create a channel as **MainAdChannel** under **Channels** folder

* Create another channel as **TargetedSinglePlay** under **Channels** folder

* Add relevant assets to both the channels

The following image shows the **Channel Level Activation** project with **MainAdChannel** and **TargetedSinglePlay** channels in **Channels** folder.

![screen_shot_2018-11-27at104500am](assets/screen_shot_2018-11-27at104500am.png)

>[!NOTE]
>
>For additional information on how to create a project and how to create a sequence channel, please refer to resources below:
>
>* [Creating and Managing Projects](creating-a-screens-project.md)
>
>* [Managing a Channel](managing-channels.md)
>

### Implementation {#implementation}

Implementing Channel Level Activation in an AEM Screens project involves three major tasks:

1. **Setting up Project taxonomy including Channels, Locations, and Displays**
1. **Assigning Channels to Display**
1. **Setting up a Schedule and Priority**

Follow the steps below to implement the functionality:

1. **Create a Location**

   Navigate to your **Locations** folder in your AEM Screens project and create a location as **Region**.

   ![screen_shot_2018-11-27at112112am](assets/screen_shot_2018-11-27at112112am.png)

   >[!NOTE]
   >
   >To learn how to create a location, please refer to **[Creating and Managing Locations](managing-locations.md)**.

1. **Create Display under Location**

    1. Navigate to **Channel Level Activation** > **Locations** > **Region**.
    1. Select **Region** and click **+ Create** from the action bar.
    1. Select **Display** from the wizard and create a display titled as **RegionDisplay.**

   ![screen_shot_2018-11-27at112216am](assets/screen_shot_2018-11-27at112216am.png)

1. **Assign Channels to Display**

   For **MainAdChannel:**

    1. Navigate to **Channel Level Activation** > **Locations** > **Region** > **RegionDisplay** and click **Assign Channel** from the action bar.
    1. **Channel Assignment** dialog box opens.
    1. Select **Reference Channel**.. by path.
    1. Select the **Channel Path** as **Channel Level Activation** --&gt; ***Channels*** --&gt; ***MainAdChannel***.
    1. The **Channel Role** is populated as **mainadchannel**.
    1. Select the **Priority** as **1**.
    1. Select the **Supported Events** as **Initial Load** and **Idle Screen**.
    1. Click **Save**.

   ![screen_shot_2018-11-27at124626pm](assets/screen_shot_2018-11-27at124626pm.png)

   >[!NOTE]
   >
   >You can also assign channel from the display dashboard by navigating to **Channel Level Activation** --&gt; **Locations** --&gt; **Region** --&gt; **RegionDisplay** and clicking **Dashboard** from the action bar. Click **+ Assign Channel** from the **ASSIGNED CHANNELS & SCHEDULES** panel.

   Similarly, assign channel **TargetedSinglePlay** for display**:

    1. Navigate to **Channel Level Activation** --&gt; **Locations** --&gt; **Region** --&gt; **RegionDisplay** and click **Assign Channel** from the action bar.
    1. **Channel Assignment** dialog box opens.
    1. Select **Reference Channel**.. by path.
    1. Select the **Channel Path** as **Channel Level Activation*** --&gt; ***Channels*** --&gt; ***TargetedSinglePlay***.
    1. The **Channel Role** is populated as **targetedsingleplay**.
    1. Set the **Priority** as **2**.
    1. Select the **Supported Events** as **Initial Load**, **Idle Screen** and **Timer**, *as shown in the figure below.
    1. Choose the date in **active from** as November 27, 2018 11:59 pm and in **active until** as November 28, 2018 12:05 am.
    1. Click **Save**.

   >[!CAUTION]
   >
   >You must set the priority for **TargetedSinglePlay** channel higher than the **MainAdSegment** channel.

   ![screen_shot_2018-11-27at31206pm](assets/screen_shot_2018-11-27at31206pm.png)

   >[!NOTE]
   >
   >To choose the same day, you have to select the next day and the manually edit the date to the same day but for a later time. This restricts the user from selecting a past date. Please refer to the example below:

   ![new1](assets/new1.gif)

## Viewing the Results {#viewing-the-results}

Once you have the set up for channels and display complete, please launch the AEM Screens player to view the content.

The player displays the content of **MainAdChannel** and exactly at 11:59 pm (as set in the schedule), the **TargetedSinglePlay** channel will display its content until 12:05 am and then the **MainAdChannel** will resume playing its content again.

>[!NOTE]
>
>To learn about AEM Screen Player, please refer to the following resources:
>[AEM Screens Player downloads](https://download.macromedia.com/screens/)
>[Working with AEM Screens Player](working-with-screens-player.md)


## Handling Recurrence for Assets in a Channel {#handling-recurrence-in-assets}

You can schedule assets in a channel to recur at certain intervals on daily, weekly, or monthly basis too as per your requirement.

Suppose you want to display contents of a channel only on Fridays from 1:00 pm until 10:00 pm. You can use the **Activation** tab to set the desired recurring interval for your asset.

### Day Parting {#day-parting}

1. Select the channel and click on **Dashboard** from the action bar to open the channel dashboard.

1. After entering the start date/time and end/date time from the **Channel Assignment** dialog box, you can use an expression or a natural text version to specify your recurrence schedule.

   >[!NOTE]
   >
   >You can skip or include the **Active from** and **Active Until** fields and add the expression to the Schedules field, as per your requirement.

1. Enter the expression into the **Schedule** and your asset will display for the particular interval of day and time.

#### Example Expressions for Day Parting {#example-one}

The following table summarizes few example expressions that you can add to the schedule while assigning channel to a display.

| **Expression** | **Interpretation** |
|---|---|
| before 8:00 am | the asset in the channel plays before 8:00 am everyday |
| after 2:00 pm | the asset in the channel plays after 2:00 pm everyday |
| after 12:15 and before 12:45 | the asset in the channel plays after 12:15 pm everyday for 30 minutes |
| before 12:15 also after 12:45 | the asset in the channel plays before 12:15 pm everyday and then also after 12:45 pm |
| Mon,Tue,Wed or Mon-Wed | the asset plays in the asset in the channel from Monday until Wednesday |
| on the 1st day of January after 2:00 pm also on the 2nd day of January also on the 3rd day of January before 3:00 am | the asset in the channel starts playing after 2:00 pm on January 1st, continues playing for the whole day on January 2nd all the way until 3:00 am on January 3rd |
| on the 1-2 day of January after 2:00 pm also on the 2-3 day of January before 3:00 am | the asset in the channel starts player after 2:00 pm on January 1st, continues playing until 3:00 am on January 2nd, then it starts again on January 2nd at 2:00 pm and continues playing until 3:00 am on January 3rd |

>[!NOTE]
>
>You can also use _military time_ notation (that is, 14:00) instead of *am/pm* notation (that is, 2:00 pm).

### WeekParting {#week-parting}

1. Select the channel and click on **Dashboard** from the action bar to open the channel dashboard.

1. After entering the start date/time and end/date time from the **Channel Assignment** dialog box, you can use an expression or a natural text version to specify your recurrence schedule.

   >[!NOTE]
   >
   >You can skip or include the **Active from** and **Active Until** fields and add the expression to the Schedules field, as per your requirement.

1. Enter the expression into the **Schedule** and your asset will display for the particular interval of day and time.

#### Example Expressions for WeekParting {#example-two}

The following table summarizes few example expressions that you can add to the schedule while assigning channel to a display.

| **Expression** | **Interpretation** |
|---|---|
| Mon,Tue,Wed or Mon-Wed | the asset plays in the asset in the channel from Monday until Wednesday |
| before 8:00 am | the asset in the channel plays before 8:00 am everyday |
| after 2:00 pm | the asset in the channel plays after 2:00 pm everyday |
| after 12:15 and before 12:45 | the asset in the channel plays after 12:15 pm everyday for 30 minutes |
| before 12:15 also after 12:45 | the channel plays before 12:15 pm everyday and then also after 12:45 pm |

>[!NOTE]
>
>You can also use _military time_ notation (that is, 14:00) instead of *am/pm* notation (that is, 2:00 pm).


### MonthParting {#month-parting}

1. Select the channel and click on **Dashboard** from the action bar to open the channel dashboard.

1. After entering the start date/time and end/date time from the **Channel Assignment** dialog box, you can use an expression or a natural text version to specify your recurrence schedule.

   >[!NOTE]
   >
   >You can skip or include the **Active from** and **Active Until** fields and add the expression to the Schedules field, as per your requirement.

1. Enter the expression into the **Schedule** and your asset will display for the particular interval of day and time.

#### Example Expressions for MonthParting {#example-three}

The following table summarizes few example expressions that you can add to the schedule while assigning channel to a display.

| **Expression** | **Interpretation** |
|---|---|
| of February,May,August,November | the asset plays in the channel in February,May,August,November |

>[!NOTE]
>
>When defining days of the week and months, you can both use the short hand and full-name notations, such as, Mon/Monday and Jan/January.

>[!NOTE]
>
>You can also use _military time_ notation (that is, 14:00) instead of *am/pm* notation (that is, 2:00 pm).

### Combination of Partings {#combined-parting}

1. Select the channel and click on **Dashboard** from the action bar to open the channel dashboard.

1. After entering the start date/time and end/date time from the **Channel Assignment** dialog box, you can use an expression or a natural text version to specify your recurrence schedule.

   >[!NOTE]
   >
   >You can skip or include the **Active from** and **Active Until** fields and add the expression to the Schedules field, as per your requirement.

1. Enter the expression into the **Schedule** and your asset will display for the particular interval of day and time.

#### Example Expressions for Combination of Partings {#example-four}

The following table summarizes few example expressions that you can add to the schedule while assigning channel to a display.

| **Expression** | **Interpretation** |
|---|---|
| after 6:00 and before 18:00 on Mon,Wed of Jan-Mar | the asset plays in the channel between 6am and 6pm on Mondays and Wednesdays from January to end of March |
| on the 1st day of January after 2:00 pm also on the 2nd day of January also on the 3rd day of January before 3:00 am | the asset in the channel starts playing after 2:00 pm on January 1st, continues playing for the whole day on January 2nd all the way until 3:00 am on January 3rd |
| on the 1-2 day of January after 2:00 pm also on the 2-3 day of January before 3:00 am | the asset in the channel starts player after 2:00 pm on January 1st, continues playing until 3:00 am on January 2nd, then it starts again on January 2nd at 2:00 pm and continues playing until 3:00 am on January 3rd |

>[!NOTE]
>
>When defining days of the week and months, you can both use the short hand and full-name notations, such as, Mon/Monday and Jan/January.  Additionally, you can also use _military time_ notation (that is, 14:00) instead of *am/pm* notation (that is, 2:00 pm).
