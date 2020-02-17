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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 變更組織品牌標誌 {#changing-the-organization-logo-for-branding}

組織標誌會顯示在AEM Forms工作區的左上角。 若要更新標誌，請依照AEM Forms工 [作區自訂的「一般」步驟](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) ，然後依照下列步驟進行。

1. 建立標誌，並將檔案命名為 `NewWorkspace.png`。 使用WebDAV用戶端將影像檔置於/apps/ws/images檔案夾中。

   >[!NOTE]
   >
   >標誌影像的建議大小為218 px x 20 px。

   >[!NOTE]
   >
   >如需WebDAV存取的詳細資訊，請參閱 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

1. 新增下列樣式，在/apps/ws/css/newStyle.css的樣式表中參考新的標誌影像。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
