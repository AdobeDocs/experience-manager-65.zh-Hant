---
title: 與ExactTarget整合
seo-title: 與ExactTarget整合
description: 瞭解如何將AEM與ExactTarget整合。
seo-description: 瞭解如何將AEM與ExactTarget整合。
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2

---


# 與ExactTarget整合{#integrating-with-exacttarget}

將AEM與Exact target整合，可讓您透過Exact target管理並傳送在AEM中建立的電子郵件。 此外，它還可讓您透過AEM頁面上的AEM表單，使用「完全目標」的銷售機會管理功能。

整合提供下列功能：

* 在AEM中建立電子郵件並發佈至Exact target進行散發的功能。
* 設定AEM表單動作以建立「完全目標」訂閱者的能力。

在設定ExactTarget後，您可以將電子報或電子郵件發佈至ExactTarget。 請參閱 [將電子報發佈至電子郵件服務](/help/sites-authoring/personalization.md)。

## 建立ExactTarget設定 {#creating-an-exacttarget-configuration}

ExactTarget組態可透過Cloudservices或工具新增。 本節將介紹這兩種方法。

### 透過Cloudservices設定ExactTarget {#configuring-exacttarget-via-cloudservices}

若要在雲端服務中建立ExactTarget設定：

1. 在歡迎頁面上，按一下「 **雲端服務」**。 (或直接存取位 `https://<hostname>:<port>/etc/cloudservices.html`置。)
1. 按一 **下ExactTarget** ，然後 **按一下Configure**。 ExactTarget設定視窗隨即開啟。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 輸入標題和名稱（可選），然後按一下「 **建立**」。 「 **ExactTarget設定** 」設定視窗隨即開啟。

   ![chlimage_1](assets/chlimage_1.jpeg)

1. 輸入使用者名稱、密碼並選取API端點(例如 **https://webservice.exacttarget.com/Service.asmx**)。
1. 按一 **下「連線至ExactTarget」。** 成功連線後，您會看到成功對話方塊。 按一下 **確定** ，退出窗口。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 選擇帳戶（如果可用）。 此帳戶適用於Enterprise 2.0客戶。 按一下 **確定**。

   已設定ExactTarget。 您可以按一下「編輯」來編輯 **設定**。 您可以按一下「前往ExactTarget」, **前往ExactTarget**。

1. AEM現在提供「資料延伸功能」。 您可以匯入ExactTarget資料擴充欄。 此設定可透過按一下「+」符號來設定，「+」號碼除了顯示成功建立的ExactTarget設定外，還會顯示。 您可以從下拉式清單中選取任何現有的資料擴充功能。 如需如何設定資料擴充功能的詳細資訊，請參閱 [ExactTarget檔案](https://help.exacttarget.com/en/documentation/exacttarget/subscribers/data_extensions_and_data_relationships)。

   匯入的資料擴充欄稍後可透過「文字與個人化」 **元件使用** 。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 透過工具設定ExactTarget {#configuring-exacttarget-via-tools}

要在工具中建立ExactTarget配置：

1. 在歡迎頁面上，按一下「 **工具**」。 或者，直接前往 `https://<hostname>:<port>/misadmin#/etc`。
1. 依序選 **擇工具**、雲端服 **務設定、** 完 **全目標**。
1. 按一 **下「新增** 」以開啟「**建立頁面**」視窗。

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. 輸入「 **標題** 」(Title **)和（可選）**「名稱 **」(Name**)，然後按一下「建立」。
1. 按照上一步步驟4中的說明輸入配置資訊。 請依照該程式完成ExactTarget的設定。

### 添加多個配置 {#adding-multiple-configurations}

要添加多個配置：

1. 在歡迎頁面上，按一下「 **雲端服務** 」，然後按 **一下「完全目標」**。 按一下「顯 **示配置** 」按鈕，如果有一個或多個ExactTarget配置可用，則該按鈕將顯示。 列出所有可用的配置。
1. 按一下「 **可用** 」組態旁的+號。 這將開啟「創 **建配置** 」窗口。 請依照先前的設定程式來建立新的設定。