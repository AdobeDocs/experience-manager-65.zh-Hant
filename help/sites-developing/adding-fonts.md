---
title: 新增字型以進行圖形演算
seo-title: 新增字型以進行圖形演算
description: AEM可讓您產生包含動態擷取自內容之文字的圖形
seo-description: AEM可讓您產生包含動態擷取自內容之文字的圖形
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 新增字型以進行圖形演算{#adding-fonts-for-graphic-rendering}

AEM可讓您產生包含動態擷取自內容之文字的圖形。

若要這麼做，您也可以載入並使用您自己的字型。

目前，Java Platform的所有實作都支援 [TrueType](https://en.wikipedia.org/wiki/Truetype) 字型。

1. 開啟CRXDE Lite並導覽至您的專案應用程式資料夾：

   `/apps/<your-project>/`

1. 在創 `/apps/<your-project>/` 建新節點下：

   * **名稱**: `fonts`
   * **類型**: `sling:Folder`
   儲存所有變更。

1. 將字型檔案複製到此檔案夾；例如，使用WebDAV。

   >[!NOTE]
   >
   >儲存庫中的字型檔案必須有尾碼 `*.ttf` 或 `*.TTF`。

1. 更新 [Day Commons](/help/sites-deploying/configuring-osgi.md) GFX Font Helper [的OSGi組態](/help/sites-deploying/osgi-configuration-settings.md)。 新增字型資料夾的路徑；即 `/apps/<your-project>/fonts`。

1. 返回CRXDE Lite。 您現在應該會在資 `.fontlist` 料夾中看到包含已匯入字型名稱的節點。

   這些字型現在已可供Java API使用。

如需如何搭配Java API使用字型的完整詳細資訊，請參 [閱Java API的Font類別檔案](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)。

