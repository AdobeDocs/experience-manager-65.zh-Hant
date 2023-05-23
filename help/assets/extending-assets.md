---
title: 自定義和擴展 [!DNL Assets]
description: 瞭解如何自定義和擴展資產共用和資產編輯器，這些編輯器為用戶提供了專門定製的介面和一組功能。
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 自定義和擴展 [!DNL Assets] {#customizing-and-extending-assets}

資產編輯器是AdobeEnterprise Manager網站的用戶用來查找、查看和操作儲存庫中的數字資產的主要訪問點。

作為 [!DNL Experience Manager] 開發人員，您可以通過多種方式自定義和擴展資產編輯器，向用戶提供專門定製的介面和一組功能。

功能的以下方面可以定制或增強：

* [擴展資產編輯器](asseteditorx.md)
* [擴展資產搜索](searchx.md)
* [使用媒體處理程式和工作流處理資產](media-handlers.md)
* [將資產與活動流整合](extending-activity-stream.md)
* [資產代理開發](proxy.md)
* [配置ImageMagick的最佳做法](best-practices-for-imagemagick.md)

## 自定義外觀 {#customizing-the-look-and-feel}

資產編輯器外觀的以下方面可自定義：

* 標識：您可以將您自己組織的徽標添加到介面。
* 顏色和字型：可以更改介面中使用的顏色和字型。
* HTML代碼：要進行更徹底的自定義，您可以更改定義介面的基礎HTML代碼。

## 自定義格式副本 {#customizing-renditions}

在 [!DNL Experience Manager Assets] 術語格式副本是顯示資產的形式。 通常，特定資產可能具有多個格式副本。 例如，全色影像可能具有一個原始大小的格式副本，另一個格式副本具有縮放大小，另一個格式副本同時縮放並轉換為灰度。

特定資產可用的格式副本可以自定義，並可以建立新格式副本。
