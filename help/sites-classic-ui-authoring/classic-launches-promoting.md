---
title: 提升 Launch
description: 在發佈之前，您需要升級啟動頁面，以將內容移回源（生產）。 當啟動頁面被升級時，源頁面的相應頁面被升級頁面的內容替換。
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 3%

---

# 提升 Launch{#promoting-launches}

在發佈之前，您需要升級啟動頁面，以將內容移回源（生產）。 當啟動頁面被升級時，源頁面的相應頁面被升級頁面的內容替換。 升級啟動頁時可使用以下選項：

* 是僅升級當前頁面還是整個啟動。
* 是否提升當前頁的子頁。
* 是升級完整啟動，還是僅升級已更改的頁面。

## 升級啟動頁 {#promoting-launch-pages}

要升級頁面，請在編輯要升級的啟動頁面時執行以下步驟：

1. 在 **頁面** 頁籤，按一下 **升級啟動**。
1. 指定要升級的頁：

   * （預設）要僅升級當前頁面，請選擇 **將頁面更改提升到生產版本**。
   * 要同時提升當前頁面的子頁面，請選擇 **包括子頁**。
   * 要升級啟動中的所有頁面，請選擇 **將完全啟動升級為生產版本**。

1. 要將生產頁添加到工作流包，請選擇 **添加到工作流包** ，然後選擇工作流包。
1. 按一下 **提升**。

## 使用 AEM 工作流程處理提升頁面 {#processing-promoted-pages-using-aem-workflow}

使用工作流模型對已升級的「啟動」頁執行批量處理：

1. 建立工作流包。
1. 當作者升級「啟動」頁面時，他們會將其儲存在工作流包中。
1. 使用包作為負載啟動工作流模型。

要在升級頁面時自動啟動工作流， [配置工作流啟動程式](/help/sites-administering/workflows-starting.md#workflows-launchers) 的子菜單。

例如，當作者提升「啟動」頁面時，可以自動生成頁面激活請求。 配置工作流啟動程式以在修改包節點時啟動請求激活工作流。

![chlimage_1-136](assets/chlimage_1-136.png)
