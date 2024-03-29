---
title: 新增圖形演算的字型
description: AEM可讓您產生結合動態擷取自內容的文字的圖形
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 1%

---

# 新增圖形演算的字型{#adding-fonts-for-graphic-rendering}

AEM可讓您產生包含動態擷取自內容的文字的圖形。

要執行此操作，您也可以載入並使用您自己的字型。

目前所有Java平台支援的實作 [TrueType](https://en.wikipedia.org/wiki/Truetype) 字型。

1. 開啟CRXDE Lite並導覽至您的專案應用程式資料夾：

   `/apps/<your-project>/`

1. 在 `/apps/<your-project>/` 建立節點：

   * **名稱**：`fonts`
   * **類型**：`sling:Folder`

   儲存所有變更。

1. 將字型檔案複製到此資料夾；例如，使用WebDAV。

   >[!NOTE]
   >
   >存放庫中的字型檔案必須有字尾 `*.ttf` 或 `*.TTF`.

1. 更新 [OSGi設定](/help/sites-deploying/configuring-osgi.md) 之 [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). 將路徑新增至您的字型資料夾；也就是說， `/apps/<your-project>/fonts`.

1. 返回CRXDE Lite。 您現在應該會看到 `.fontlist` 包含已匯入字型名稱的資料夾中的節點。

   這些字型現已可在Java API中使用。

如需如何搭配Java API使用字型的完整詳細資訊，請參閱 [Java API的字型類別檔案](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
