---
title: 更新檔案的連結
seo-title: 更新檔案的連結
description: 如何更新AEM Forms工作區中「工作區說明」連結的目的地，以指向您的自訂檔案連結。
seo-description: 如何更新AEM Forms工作區中「工作區說明」連結的目的地，以指向您的自訂檔案連結。
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 更新檔案的連結 {#updating-the-link-to-the-documentation}

您可以選取「說明>工作區說明」，以存取AEM Forms工作區 **的預設說明內容**。 它指向Adobe網站上的線上檔案。 不過，您可將其更新為指向任何其他URL。

請考慮下列使用案例，您可能想要變更預設說明URL:

* 提供您所選語言的本地化說明。
* 針對您的自訂工作區提供自訂說明內容。

若要更新線上檔案的URL，請遵循自訂的 [一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md) ，然後遵循下列步驟。

1. 將檔 `userinfo.html` 案從復 `/libs/ws/js/runtime/templates` 制到 `/apps/ws/js/runtime/templates`。
1. 變更：

   ```
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   至

   ```
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. 執行下列動作：

   1. 開啟/apps/ws/js/registry.js進行編輯。
   1. 搜尋並取代 `text!/lc/libs/ws/js/runtime/templates/userinfo.html` 為 `text!/lc/apps/ws/js/runtime/templates/userinfo.html`。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
