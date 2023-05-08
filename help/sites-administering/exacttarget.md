---
title: 與ExactTarget整合
seo-title: Integrating with ExactTarget
description: 了解如何將AEM與ExactTarget整合。
seo-description: Learn how to integrate AEM with ExactTarget.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# 與ExactTarget整合{#integrating-with-exacttarget}

將AEM與Exact Target整合可讓您透過Exact Target管理並傳送在AEM中建立的電子郵件。 它也可讓您透過AEM頁面上的AEM表單，使用Exact Target的銷售機會管理功能。

整合提供下列功能：

* 可在AEM中建立電子郵件，並發佈至Exact Target進行分送。
* 設定AEM表單動作以建立「精確目標」訂閱者的功能。

設定ExactTarget後，您就可以將電子報或電子郵件發佈至ExactTarget。 請參閱 [將電子報發佈至電子郵件服務](/help/sites-authoring/personalization.md).

## 建立ExactTarget設定 {#creating-an-exacttarget-configuration}

ExactTarget設定可透過雲端服務或工具新增。 本節將說明兩種方法。

### 透過雲端服務設定ExactTarget {#configuring-exacttarget-via-cloudservices}

若要在Cloud Services中建立ExactTarget設定：

1. 在歡迎頁面上，按一下 **Cloud Services**. (或直接存取 `https://<hostname>:<port>/etc/cloudservices.html`.)
1. 按一下 **ExactTarget** 然後 **設定**. 「ExactTarget」設定視窗隨即開啟。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 輸入標題，（可選）輸入名稱，然後按一下 **建立**. 此 **ExactTarget設定** 設定視窗隨即開啟。

   ![chlimage_1](assets/chlimage_1.jpeg)

1. 輸入使用者名稱、密碼並選取API端點(例如 **https://webservice.exacttarget.com/Service.asmx**)。
1. 按一下 **連線至ExactTarget。** 成功連線後，您會看到成功對話方塊。 按一下 **確定** 以退出視窗。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 選擇帳戶（如果可用）。 帳戶適用於Enterprise 2.0客戶。 按一下&#x200B;**「確定」**。

   ExactTarget已設定。 您可以按一下「 」，編輯設定 **編輯**. 您可以按一下 **前往ExactTarget**.

1. AEM現在提供資料擴充功能。 您可以匯入ExactTarget資料擴充功能欄。 除了成功建立ExactTarget設定外，按一下出現的「+」符號即可進行設定。 您可以從下拉式清單中選取任何現有的資料擴充功能。 如需如何設定資料擴充功能的詳細資訊，請參閱 [ExactTarget檔案](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&amp;type=5).

   匯入的資料擴充功能欄稍後可透過 **文字和個人化** 元件。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 透過工具設定ExactTarget {#configuring-exacttarget-via-tools}

若要在工具中建立ExactTarget設定：

1. 在歡迎頁面上，按一下 **工具**. 或直接導覽至 `https://<hostname>:<port>/misadmin#/etc`.
1. 選擇 **工具**，然後 **Cloud Services配置、** then **ExactTarget**.
1. 按一下 **新增** 以開啟**建立頁面**視窗。

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. 輸入 **標題** 和（可選） **名稱**，然後按一下 **建立**.
1. 按上一步步驟4所述輸入配置資訊。 請依照該程式完成ExactTarget的設定。

### 新增多個設定 {#adding-multiple-configurations}

若要新增多個設定：

1. 在歡迎頁面上，按一下 **Cloud Services** 按一下 **ExactTarget**. 按一下 **顯示配置** 按鈕，此按鈕會在有一或多個ExactTarget設定可用時顯示。 列出所有可用的配置。
1. 按一下 **+** 在「可用配置」旁邊簽名。 這會開啟 **建立配置** 窗口。 請依照先前的配置過程建立新配置。
