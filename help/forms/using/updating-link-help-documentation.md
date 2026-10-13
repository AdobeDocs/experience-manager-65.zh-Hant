---
title: 更新檔案的連結
description: 如何更新AEM Forms工作區中Workspace說明連結的目的地，以指向您的自訂檔案連結。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 2%
---
# 更新檔案的連結 {#updating-the-link-to-the-documentation}

您可以選取&#x200B;**說明> AEM Forms說明**，以存取Workspace工作區的預設說明內容。 它指向Adobe網站上的線上檔案。 不過，您可以將其更新為指向任何其他URL。

請考量下列您可能想要變更預設說明URL的使用案例：

* 以您選擇的語言提供當地語系化說明。
* 提供自訂工作區的自訂說明內容。

若要更新線上檔案的URL，請遵循[自訂的一般步驟](/help/forms/using/generic-steps-html-workspace-customization.md)，然後遵循下列步驟。

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
   1. 搜尋並以`text!/lc/apps/ws/js/runtime/templates/userinfo.html`取代`text!/lc/libs/ws/js/runtime/templates/userinfo.html`。
