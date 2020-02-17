---
title: 自訂和擴充AEM資產
description: 瞭解如何自訂和擴充資產共用與資產編輯器，為使用者提供特別自訂的介面和功能集。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 自訂和擴充資產 {#customizing-and-extending-assets}

資產編輯器是Adobe Enterprise Manager(AEM)網站的使用者用來尋找、檢視和控制儲存庫中數位資產的主要存取點。

身為AEM開發人員，您可以透過多種方式自訂和擴充資產編輯器，為使用者提供特別自訂的介面和功能集。

可自訂或增強功能的下列方面：

* [擴充資產編輯器](asseteditorx.md)
* [擴充資產搜尋](searchx.md)
* [使用媒體處理常式和工作流程處理資產](media-handlers.md)
* [將資產與活動串流整合](extending-activity-stream.md)
* [資產代理開發](proxy.md)
* [設定ImageMagick的最佳實務](best-practices-for-imagemagick.md)

## 自訂外觀 {#customizing-the-look-and-feel}

可自訂資產編輯器外觀和感覺的下列方面：

* 標誌：您可以將您自己組織的標誌新增至介面。
* 顏色和字型：您可以變更介面中使用的顏色和字型。
* HTML程式碼：若要更徹底地自訂，您可以變更定義介面的基礎HTML程式碼。

## 自訂轉譯 {#customizing-renditions}

在AEM Assets術語中，轉譯是資產呈現的表單。 一般而言，特定資產可能具有多個轉譯。 例如，全彩影像可能有一個格式副本的原始大小，另一個格式副本的縮放大小，另一個格式副本的縮放大小和灰階轉換大小。

特定資產可用的轉譯可以自訂，並建立新的轉譯。
