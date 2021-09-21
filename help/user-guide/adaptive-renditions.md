---
title: Adaptive Renditions in AEM Screens
description: This page describes how to use Adaptive Renditions in AEM Screens.
index: no
---
# Adaptive Renditions {#adaptive-renditions}

## Introduction {#introduction}

Adaptive Renditions allow the devices to automatically select the best rendition for a device based on customer-defined rules. The devices will automatically download and play the most appropriate rendition of an asset based on these rules allowing customers to only focus on designing the *main* experience.

## Objective {#objective}

As an AEM Screens Content Author, you can now configure device-specific asset renditions to be downloaded and played automatically without having to create all content variations manually.

So, if you deployed a variety of devices, using this feature will allow the device to automatically download and play the most appropriate rendition of an asset based on the rules.

## Architectural Overview {#architectural-overview}

Adaptive Renditions are based on the idea of having multiple asset renditions named following a specific naming convention. The decision to play a specific rendition is made by evaluating media query expressions that can only be resolved on devices with expected capabilities. The ability of having an associated rendition naming pattern defines a rendition mapping rule. After computing all available expressions the Screens player will collect the naming patterns corresponding to the matching rules. The patterns are used to find the correct renditions during the sequence playback by looking for the patterns in the rendition names.


## Configuring the Setup for using Adaptive Renditions {#setup-adaptive-renditions}

To enable the Adaptive Renditions feature, the mapping rules should be present and the CA configuration resolvable for channels and displays:

1. Check if the rendition mapping configuration exists in `JCR`. All the latest feature packs have this node structure pre-populated.

   >[!NOTE]
   >All the latest feature packs have this node structure pre-populated.


1. Ensure the Screens project has the rendition mapping configuration associated with it.

   * Every new project created with the Screens project wizard will contain a reference pointing to rendition mapping configuration.

   * In an older version of Screens projects, the association is required to be explicitly defined by adding `sling:configRef` property pointing at `/conf/screens` to the project content node.

## Migration Strategy {#migration-strategy}

>[!IMPORTANT]
>For large networks, it is recommended that the migration is done gradually to mitigate the risks as the feature will introduce changes in the manifest and file storage format. 

To enable the feature, add at least one mapping rule and make sure the rendition mapping configuration is resolvable in the context of displays and channels:

1. Add rendition mapping rules.
1. Create a folder for new channels and add a reference pointing at the rendition mapping configuration.
1. Create new channels replacing the old ones and upload renditions.
1. Reassign displays to the new channels.
1. Add a reference to the migrated displays/locations pointing at the rendition mapping configuration.
1. Repeat steps 3, 4, and 5 for all remaining channels and displays.
1. After finishing with migration, remove all config references from channels/displays/locations and add a single one to the project content node.

## Setting up Author and Publish {#setup-author-publish}

Follow the steps below to setup author and publish:

* Rendition mapping has to be replicated manually.

* Asset renditions are not replicated by default. All relevant assets need to be replicated manually.


## Adding Rendition Mapping Rules {#adding-rendition-mapping-rules}

1. To add a mapping rule you need to create a node of type `nt:unstructured` under the rendition-mapping node.

1. Add the expression property with the value containing the query expression.

   >[!NOTE]
   >Refer to [Using Media Query Syntax](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries) to learn more.

1. Add the pattern property with the value containing the rendition naming pattern that will be selected, if the expression is evaluated to true.

## Uploading Renditions {#upload-renditions}

1. Create a version of the asset which better suits the signage display, for example, `portrait orientation`.

1. Choose the rendition naming pattern, for example,`portrait`.

1. Rename the asset file so it contain the pattern, for example, `my_asset_portrait.png`.

1. Upload the rendition by clicking the Add Rendition button in the toolbar.


## The Next Steps {#next-steps}

Once you have uploaded the renditions, you can now use Adaptive Renditions, in your AEM Screens channels.