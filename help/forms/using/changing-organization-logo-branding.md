---
title: 變更組織品牌標誌
seo-title: 變更組織品牌標誌
description: 若要品牌化AEM Forms工作區，請自訂預設標誌，以提供您組織的標誌。
seo-description: 若要品牌化AEM Forms工作區，請自訂預設標誌，以提供您組織的標誌。
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 變更品牌{#changing-the-organization-logo-for-branding}的組織標誌

組織標誌會顯示在AEM Forms工作區的左上角。 若要更新標誌，請遵循AEM Forms工作區自訂的[一般步驟，然後遵循下列步驟。](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)

1. 建立標誌，並將檔案命名為`NewWorkspace.png`。 使用WebDAV用戶端將影像檔置於/apps/ws/images檔案夾中。

   >[!NOTE]
   >
   >標誌影像的建議大小為218 px x 20 px。

   >[!NOTE]
   >
   >有關WebDAV訪問的詳細資訊，請參見[https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

1. 新增下列樣式，在/apps/ws/css/newStyle.css的樣式表中參考新的標誌影像。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
