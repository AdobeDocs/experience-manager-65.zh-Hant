---
title: 更新檔案的連結
seo-title: 更新檔案的連結
description: 如何更新AEM Forms工作區中工作區說明連結的目的地，以指向您的自訂檔案連結。
seo-description: 如何更新AEM Forms工作區中工作區說明連結的目的地，以指向您的自訂檔案連結。
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---

# 正在更新指向文檔{#updating-the-link-to-the-documentation}的連結

您可以選取&#x200B;**Help > Workspace說明**，以存取AEM Forms工作區的預設說明內容。 它指向Adobe網站上的線上文檔。 不過，您可以更新它以指向任何其他URL。

請考量下列使用案例，其中您可能想要變更預設說明URL:

* 以您所選擇的語言提供本地化說明。
* 為您的自訂工作區提供自訂說明內容。

要更新聯機文檔的URL，請執行[自定義的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)，然後執行以下步驟。

1. 將`userinfo.html`檔案從`/libs/ws/js/runtime/templates`複製到`/apps/ws/js/runtime/templates`。
1. 變更：

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
   1. 搜尋並將`text!/lc/libs/ws/js/runtime/templates/userinfo.html`取代為`text!/lc/apps/ws/js/runtime/templates/userinfo.html`。
