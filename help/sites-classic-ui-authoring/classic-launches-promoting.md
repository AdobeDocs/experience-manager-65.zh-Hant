---
title: 提升 Launch
seo-title: Promoting Launches
description: 發佈前，您必須促銷啟動頁面，才能將內容移回來源（生產）。 啟動頁面升級時，來源頁面的對應頁面會取代為升級頁面的內容。
seo-description: You need to promote launch pages to move the content back into the source (production) before publishing. When a launch page is promoted, the corresponding page of the source pages is replaced with the content of the promoted page.
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 3%

---

# 提升 Launch{#promoting-launches}

發佈前，您必須促銷啟動頁面，才能將內容移回來源（生產）。 啟動頁面升級時，來源頁面的對應頁面會取代為升級頁面的內容。 提升啟動頁面時，可使用下列選項：

* 僅促銷目前頁面還是整個啟動。
* 是否促銷目前頁面的子頁面。
* 是要促銷完整啟動，還是只促銷已變更的頁面。

## 提升啟動頁面 {#promoting-launch-pages}

若要促銷頁面，請在編輯您要促銷的啟動頁面時執行下列步驟：

1. 在 **頁面** 標籤，按一下 **促銷啟動**.
1. 指定要促銷的頁面：

   * （預設）若要僅促銷目前的頁面，請選取 **將頁面變更提升至生產版本**.
   * 若要同時促銷目前頁面的子頁面，請選取 **包含子頁面**.
   * 若要促銷啟動中的所有頁面，請選取 **將Full Launch提升至生產版本**.

1. 若要將生產頁面新增至工作流程套件，請選取 **添加到工作流包** ，然後選擇工作流包。
1. 按一下 **提升**.

## 使用 AEM 工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流程模型來執行大量處理提升的啟動頁面：

1. 建立工作流程套件。
1. 作者促銷Launch頁面時，會將其儲存在工作流程套件中。
1. 以套件作為裝載，啟動工作流程模型。

若要在頁面升級時自動啟動工作流程， [設定工作流程啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers) （針對包節點）。

例如，當作者促銷啟動頁面時，您可以自動產生頁面啟動請求。 設定工作流程啟動器，以在修改套件節點時啟動「請求啟動」工作流程。

![chlimage_1-136](assets/chlimage_1-136.png)
