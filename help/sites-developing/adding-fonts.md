---
title: 新增圖形演算的字型
description: AEM可讓您產生結合動態擷取自內容之文字的圖形
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 1%
---
# 新增圖形演算的字型{#adding-fonts-for-graphic-rendering}

AEM可讓您產生結合動態擷取自內容的文字的圖形。

要執行此操作，您也可以載入並使用您自己的字型。

目前Java平台的所有實作都支援[TrueType](https://en.wikipedia.org/wiki/Truetype)字型。

1. 開啟CRXDE Lite並導覽至您的專案應用程式資料夾：

   `/apps/<your-project>/`

1. 在`/apps/<your-project>/`下建立節點：

   * **名稱**：`fonts`
   * **類型**：`sling:Folder`

   儲存所有變更。

1. 將字型檔案複製到此資料夾；例如，使用WebDAV。

   >[!NOTE]
   >
   >存放庫中的字型檔案必須有字尾`*.ttf`或`*.TTF`。

1. 更新[Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md)的[OSGi設定](/help/sites-deploying/configuring-osgi.md)。 將路徑新增至您的字型資料夾；也就是`/apps/<your-project>/fonts`。

1. 返回CRXDE Lite。 您現在應該會在包含匯入字型名稱的資料夾中看到`.fontlist`節點。

   這些字型現已可在Java API中使用。

如需有關如何搭配Java API使用字型的完整詳細資訊，請參閱Java API字型類別[&#128279;](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)的檔案。
