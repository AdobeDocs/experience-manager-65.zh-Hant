---
title: 提升啟動
seo-title: 提升啟動
description: 發佈前，您需要促銷啟動頁面，將內容移回來源（生產）。 升級啟動頁面時，來源頁面的對應頁面會以升級頁面的內容取代。
seo-description: 發佈前，您需要促銷啟動頁面，將內容移回來源（生產）。 升級啟動頁面時，來源頁面的對應頁面會以升級頁面的內容取代。
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 3%

---


# 提升啟動{#promoting-launches}

發佈前，您需要促銷啟動頁面，將內容移回來源（生產）。 升級啟動頁面時，來源頁面的對應頁面會以升級頁面的內容取代。 升級啟動頁面時可使用下列選項：

* 是僅促銷目前頁面還是整個啟動。
* 是否提升目前頁面的子頁面。
* 是要促銷完整啟動，還是只促銷已變更的頁面。

## 升級啟動頁面{#promoting-launch-pages}

若要升級頁面，請在編輯您要升級的啟動頁面時執行下列步驟：

1. 在Sidekick的&#x200B;**Page**&#x200B;標籤上，按一下「提升啟動」**。**
1. 指定要升級的頁面：

   * （預設）若要僅升級目前頁面，請選取「將頁面變更提升至生產版本」**。**
   * 要升級當前頁的子頁，請選擇&#x200B;**包含子頁**。
   * 若要升級啟動中的所有頁面，請選取「將完整啟動提升至生產版本」**。**

1. 要將生產頁添加到工作流包，請選擇&#x200B;**添加到工作流包**，然後選擇工作流包。
1. 按一下&#x200B;**Promote**。

## 使用AEM工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流程模型，對提升的啟動頁面執行大量處理：

1. 建立工作流程套件。
1. 當作者促銷「啟動」頁面時，會將其儲存在工作流程套件中。
1. 使用套件作為裝載，啟動工作流程模型。

要在升級頁時自動啟動工作流，請[為包節點配置工作流啟動程式](/help/sites-administering/workflows-starting.md#workflows-launchers)。

例如，當作者促銷「啟動」頁面時，您可以自動產生頁面啟動請求。 設定工作流程啟動程式，以在修改封裝節點時啟動「請求啟動」工作流程。

![chlimage_1-136](assets/chlimage_1-136.png)

