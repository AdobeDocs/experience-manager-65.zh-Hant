---
title: 變更品牌化的組織標誌
description: 若要品牌化AEM Forms工作區，請自訂預設標誌，以提供您組織的標誌。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 變更品牌化的組織標誌 {#changing-the-organization-logo-for-branding}

組織標誌會顯示在AEM Forms工作區的左上角。 若要更新標誌，請遵循 [AEM Forms工作區自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) 然後執行下列步驟。

1. 建立標誌並將檔案命名為 `NewWorkspace.png`. 使用WebDAV使用者端將影像檔案置於/apps/ws/images資料夾中。

   >[!NOTE]
   >
   >標誌影像的建議大小為218畫素×20畫素。

   >[!NOTE]
   >
   >如需詳細資訊，請參閱 [WebDAV存取](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en).

   [WebDAV存取](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en)

1. 請新增下列樣式，以參考樣式表中的新標誌影像：/apps/ws/css/newStyle.css。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
