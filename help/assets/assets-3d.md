---
title: Working with 3D assets in Dynamic Media
description: Learn how to work with 3D assets in Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
source-git-commit: 787c0c25da2258f234d3c821038d62bf8ef68932
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 2%

---

# Work with 3D assets in Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media lets you upload, manage, view, and deliver 3D assets as immersive experiences.

* ****
* Optimized support for viewing 3D assets with the high-quality, interactive Dimensional viewer preset powered by Adobe Dimension.
* The 3D Media WCM component lets you easily add 3D assets to your Adobe Experience Manager Sites pages.

There is no additional configuration required to use 3D assets in Dynamic Media.

![](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)**

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## 3D formats supported in Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media supports the following 3D formats.

[](/help/assets/assets-formats.md)

| 3D file extension | File format | MIME type | 附註 |
|---|---|---|---|
| GLB | Binary GL Transmission | model/gltf-binary | Includes the materials and textures as a single asset. |
| OBJ | WaveFront 3D Object File | application/x-tgif |  |
| STL | Stereolithography | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Description Zip archive | model/vnd.usdz+zip | ** |

>[!NOTE]
>
>The 3D Media WCM component and 3D preview on an asset&#39;s Details page is not compatible with the latest version of Chrome (97.x). Instead, to work with 3D assets, use Firefox or Safari, or use an earlier version of Chrome (96.x).

## Quick Start: 3D assets in Dynamic Media {#quick-start-three-d}

The following step-by-step workflow description is designed to help you get up and running quickly with 3D assets in Dynamic Media - Scene7 mode.

>[!IMPORTANT]
>
>3D assets are not supported in Dynamic Media - Hybrid mode.

Before you work with 3D assets in Dynamic Media, make sure that your Experience Manager administrator has already enabled and configured Dynamic Media Cloud Services in Dynamic Media - Scene7 mode.

[](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)[](/help/assets/troubleshoot-dms7.md)

1. ****

   * [](/help/assets/manage-assets.md#uploading-assets)
   * [](#supported-three-d-file-formats-in-dm)

1. ****

   * Organize and search 3D assets

      * [](/help/assets/organize-assets.md#organize-digital-assets)
      * [](/help/assets/search-assets.md)
      * [](/help/assets/search-assets.md#custompredicates)
   * View 3D assets

      * [](#viewing-three-d-assets)
      * [](/help/assets/managing-viewer-presets.md)
   * Work with 3D asset metadata

      * [](/help/assets/metadata.md)
      * [](/help/assets/metadata-schemas.md)



1. ****

   * [Publish static Dynamic Media 3D assets](#publishing-three-d-assets)
   * [Alternate methods for publishing Dynamic Media 3D assets using the Dimensional viewer](#alternate-publish-methods)

## About viewing and interacting with 3D assets {#viewing-three-d-assets}

This section describes how to view and interact with 3D assets two different ways: from within the asset details page and from within the 3D Media component in Experience Manager Sites.

The interactive 3D viewer includes, among other things, a collection of interactive camera controls that let you orbit, zoom, and pan the 3D asset.

The time it takes to open a 3D asset in the Asset Details page view depends on several factors. These factors include such things as the following:

* Bandwidth to the server.
* Latencies to the server
* Complexity of the image.

In addition, the capabilities of the client computer-such as a workstation, notebook, or mobile touch device-are also important to consider when you manipulate the camera interactively. A reasonably powerful system with good graphics capabilities can make the interactive 3D viewing experience smoother and more favorable.

>[!TIP]
>
>You can open the Dimensional viewer preset in the Viewer Preset Editor to practice navigating a 3D asset without the need to first upload any 3D files. The Dimensional viewer preset has a built-in 3D asset for you to interact with.
>
>[](/help/assets/managing-viewer-presets.md)

## View and interact with a 3D asset from the asset details page {#viewing-three-d-assets-from-asset-details-page}

[](/help/assets/previewing-assets.md)

****

1. Make sure you have uploaded 3D assets into Experience Manager.

   [](/help/assets/manage-assets.md#uploading-assets)

1. ************
1. ********
1. Navigate to a 3D asset that you want to view.
1. Select the card of the 3D asset.
1. On the details view page for the 3D asset, do any of the following:

   | 檢視 | 說明 | Mouse action | Touch screen action |
   | --- | --- | --- | --- |
   | **** | 使檢視畫面在 3D 場景和物件周圍環繞 | Left click + drag. | Single-finger press + drag. |
   | **** | Pan your view left, right, up, or down. | Right click + drag. | Two-finger press + drag. |
   | **** | Move in and out of areas in the 3D scene. | Scroll wheel. | Two-finger pinch. |
   | **** | Recenter your camera to a point on an object in the 3D scene. | Double-click. | Double-tap. |
   | **重設** | Near the lower-right corner of the page, select the Reset icon to restore the view target point to the center of the 3D asset. Reset also moves the camera closer or further away to show the asset in its entirety and at a reasonable viewing size. |  |  |
   | **** | To enter full screen mode, in the lower-right corner of the page, select the Fullscreen icon. |  |  |

1. ****

## Viewing and interacting with a 3D asset inside a 3D Media component {#interacting-with-asset-inside-three-d-media-component}

********

>[!IMPORTANT]
>
>You can accomplish this task only after you have added a 3D Media component to a web page and assigned a 3D asset to the component. [](#adding-the-three-d-media-component-to-a-web-page)[](#assigning-a-three-d-asset-to-the-component)

[](/help/assets/previewing-assets.md)

****

1. ****

   * ********
   * `/editor.html`

A fully interactive 3D asset as displayed in    ![](/help/assets/assets-dm/3d-asset-in-3d-media.png)****

1. ****

   | 檢視 | 說明 | Mouse action | Touch screen action |
   | --- | --- | --- | --- |
   | **** | 使檢視畫面在 3D 場景和物件周圍環繞 | Left click + drag. | Single-finger press + drag. |
   | **** | Pan your view left, right, up, or down. | Right click + drag. | Two-finger press + drag. |
   | **** | Move in and out of areas in the 3D scene. | Scroll wheel. | Two-finger pinch. |
   | **** | Recenter your camera to a point on an object in the 3D scene. | Double-click. | Double-tap. |
   | **重設** | Near the lower-right corner of the page, select the Reset icon to restore the view target point to the center of the 3D asset. Reset also moves the camera closer or further away to show the asset in its entirety and at a reasonable viewing size. |  |  |
   | **** | To enter full screen mode, in the lower-right corner of the page, select the Fullscreen icon. |  |  |

## About working with the 3D Media component {#working-with-three-d-media-component}

Dynamic Media includes a Dynamic Media 3D Media component that you can use in Adobe Experience Manager Sites to enable interactive viewing of 3D models on your web pages.

* [Add the 3D Media component to the page template](#adding-three-d-media-component-to-page-template)
* [Add the 3D Media component to a web page](#adding-the-three-d-media-component-to-a-web-page)
   * [Optional - Configure the 3D Media component](#configuring-the-three-d-component)
* [Assign a 3D asset to the 3D Media component](#assigning-a-three-d-asset-to-the-component)

## Add the 3D Media component to the page template {#adding-three-d-media-component-to-page-template}

1. ************
1. Navigate to the page template that you want to enable the 3D component in and select the template.
1. ****
1. ****

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. ****
1. ********
1. ****************
1. ********

   You can now place the Dynamic Media 3D Media component on all pages that use this template.

## Add the 3D Media component on a web page {#adding-the-three-d-media-component-to-a-web-page}

If you use Experience Manager as your web content management system, you can add 3D assets to your web pages by way of the 3D Media component.

[](/help/assets/adding-dynamic-media-assets-to-pages.md)

****

1. Open Experience Manager Sites and select the web page to which you want to add the Dynamic Media 3D Media component.
1. ********

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. On the toolbar, select the Side Panel icon to toggle or &quot;turn on&quot; the display of the panel.

1. ****

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. ********

You are now ready to assign a 3D asset to the component.

[](#assigning-a-three-d-asset-to-the-component)

### Optional - Configure the 3D Media component {#configuring-the-three-d-component}

1. ****
1. ****

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. ****

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. In the upper-right corner, select the check mark to save your changes.

## Assign a 3D asset to the 3D Media component {#assigning-a-three-d-asset-to-the-component}

After you have added a 3D Media component to a web page, you can assign a 3D asset to it.

[](#adding-the-three-d-media-component-to-a-web-page)

****

1. ********
1. ****
1. In the side panel, search for or scroll to the 3D asset that you want to view on the page being edited.
1. ****

   ![](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>********

## Publish static Dynamic Media 3D assets {#publishing-three-d-assets}

**** The reason is because Dynamic Media Imaging Server does not recognize 3D formats. As such, after you publish a 3D asset in Dynamic Media, you have an instant URL that you can copy. The URL for the 3D asset follows the usual Dynamic Media URL structure. However, you cannot edit any parameters in the asset&#39;s URL, unlike traditional image assets in Dynamic Media.

[](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)

****&#x200B;在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

If you use Experience Manager as your WCM, use this publishing method to add the Dynamic Media 3D assets directly on your web page.

[](publishing-dynamicmedia-assets.md)

[](/help/sites-authoring/publishing-pages.md)

****

1. Open a 3D asset (GLB, OBJ, or STL file format) so you can view it in the asset details page.
1. ****

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. ****
1. ****

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. ********
   * The 3D asset is a supported format (GLB, OBJ, STL, and USDZ).
   * The 3D asset was ingested into the Dynamic Media Image Production System (IPS).
   * The 3D asset is published.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. ****

### Alternate methods for publishing Dynamic Media 3D assets using the Dimensional viewer {#alternate-publish-methods}

**

* ********

   [](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)

* ********&#x200B;您可將內嵌代碼複製到剪貼簿，以便貼到網頁中。****

   [](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)
