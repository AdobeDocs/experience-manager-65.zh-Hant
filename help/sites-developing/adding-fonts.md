---
title: 為圖形渲染添加字型
seo-title: 為圖形渲染添加字型
description: AEM可讓您產生圖形，並納入從內容動態擷取的文字
seo-description: AEM可讓您產生圖形，並納入從內容動態擷取的文字
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# 為圖形渲染添加字型{#adding-fonts-for-graphic-rendering}

AEM可讓您產生圖形，並納入從內容動態擷取的文字。

要執行此操作，您也可以載入並使用您自己的字型。

目前，Java Platform的所有實施都支援[TrueType](https://en.wikipedia.org/wiki/Truetype)字型。

1. 開啟CRXDE Lite並導覽至您的專案應用程式資料夾：

   `/apps/<your-project>/`

1. 在`/apps/<your-project>/`下建立新節點：

   * **名稱**:  `fonts`
   * **類型**:  `sling:Folder`

   儲存所有變更。

1. 將字型檔案複製到此資料夾中；例如，使用WebDAV。

   >[!NOTE]
   >
   >儲存庫中的字型檔案必須尾碼為`*.ttf`或`*.TTF`。

1. 更新[Day Commons GFX字型幫助程式](/help/sites-deploying/osgi-configuration-settings.md)的[OSGi配置](/help/sites-deploying/configuring-osgi.md)。 將路徑添加到字型資料夾；即。`/apps/<your-project>/fonts`。

1. 返回CRXDE Lite。 您現在應該會在資料夾中看到包含匯入字型名稱的`.fontlist`節點。

   這些字型現在已可用於Java API。

有關如何將字型與Java API搭配使用的完整詳細資訊，請參閱[有關Java API](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)字型類的文檔。
