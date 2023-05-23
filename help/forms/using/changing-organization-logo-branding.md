---
title: 更改品牌標識
seo-title: Changing the organization logo for branding
description: 要品牌化AEM Forms工作區，請通過自定義預設徽標來提供組織的徽標。
seo-description: To brand AEM Forms workspace provide the logo of your organization by customizing the default logo.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# 更改品牌標識 {#changing-the-organization-logo-for-branding}

組織徽標顯示在AEM Forms工作區的左上角。 要更新徽標，請遵循 [AEM Forms工作區定製的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) 然後執行以下步驟。

1. 建立徽標，並將檔案命名為 `NewWorkspace.png`。 使用WebDAV客戶端將映像檔案放在/apps/ws/images資料夾中。

   >[!NOTE]
   >
   >徽標影像的建議大小為218 px × 20 px。

   >[!NOTE]
   >
   >有關WebDAV訪問的詳細資訊，請參見 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant)。

1. 通過添加以下樣式，參考樣式表中的新徽標影像：/apps/ws/css/newStyle.css。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
