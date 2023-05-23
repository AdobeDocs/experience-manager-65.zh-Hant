---
title: 添加圖形渲染的字型
seo-title: Adding Fonts for Graphic-Rendering
description: 允AEM許您生成圖形，並包含從內容中動態獲取的文本
seo-description: AEM allows you to generate graphics incorporating text dynamically taken from your content
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 添加圖形渲染的字型{#adding-fonts-for-graphic-rendering}

允許AEM您生成包含從內容中動態提取的文本的圖形。

為此，您還可以載入和使用自己的字型。

當前所有Java平台實現都支援 [真類型](https://en.wikipedia.org/wiki/Truetype) 字型。

1. 開啟CRXDE Lite並導航到項目應用程式資料夾：

   `/apps/<your-project>/`

1. 下 `/apps/<your-project>/` 建立新節點：

   * **名稱**: `fonts`
   * **類型**: `sling:Folder`

   保存所有更改。

1. 將字型檔案複製到此資料夾中；例如，使用WebDAV。

   >[!NOTE]
   >
   >儲存庫中的字型檔案必須具有尾碼 `*.ttf` 或 `*.TTF`。

1. 更新 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 共 [Day Commons GFX字型助手](/help/sites-deploying/osgi-configuration-settings.md)。 將路徑添加到字型資料夾；即 `/apps/<your-project>/fonts`。

1. 返回CRXDE Lite。 你現在應該看到 `.fontlist` 資料夾中包含導入字型名稱的節點。

   這些字型現在可以在Java API中使用。

有關如何將字型與Java API一起使用的完整詳細資訊，請參見 [Java API的Font類的文檔](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)。
