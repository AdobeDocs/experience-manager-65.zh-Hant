---
title: 更新指向文檔的連結
seo-title: Updating the link to the documentation
description: How-to更新AEM Forms工作區中「工作區幫助」連結的目標，以指向您的自定義文檔連結。
seo-description: How-to update the destination of Workspace Help link in AEM Forms workspace to point to your custom documentation link.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 2%

---

# 更新指向文檔的連結 {#updating-the-link-to-the-documentation}

通過選擇 **幫助>工作區幫助**。 它指向Adobe網站上的線上文檔。 但是，您可以更新它以指向任何其它URL。

請考慮以下可能要更改預設幫助URL的使用情形：

* 以您選擇的語言提供本地化幫助。
* 用於為自定義工作區提供自定義幫助內容。

要更新聯機文檔的URL，請遵循 [定製的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md) 然後執行以下步驟。

1. 複製 `userinfo.html` 檔案 `/libs/ws/js/runtime/templates` 至 `/apps/ws/js/runtime/templates`。
1. 更改：

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   至

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. 請執行下列動作：

   1. 開啟/apps/ws/js/registry.js進行編輯。
   1. 搜索和替換 `text!/lc/libs/ws/js/runtime/templates/userinfo.html` 與 `text!/lc/apps/ws/js/runtime/templates/userinfo.html`。
