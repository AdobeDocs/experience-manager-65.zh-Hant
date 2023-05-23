---
title: 與ExactTarget整合
seo-title: Integrating with ExactTarget
description: 瞭解如何與ExactTargetAEM整合。
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

與Exact Target集AEM成允許您管理和發送通過Exact Target建立的AEM電子郵件。 它還允許您通過頁面上的表單使用Exact TargetAEM的銷售線AEM索管理功能。

該整合提供了以下功能：

* 在中建立電子郵件並將其發AEM布到「精確目標」以進行分發的能力。
* 設定表單操作以創AEM建精確目標訂戶的能力。

配置ExactTarget後，您可以將新聞稿或電子郵件發佈到ExactTarget。 請參閱 [將新聞稿發佈到電子郵件服務](/help/sites-authoring/personalization.md)。

## 建立ExactTarget配置 {#creating-an-exacttarget-configuration}

ExactTarget配置可通過CloudServices或Tools添加。 這兩種方法都在本節中介紹。

### 通過CloudServices配置ExactTarget {#configuring-exacttarget-via-cloudservices}

要在Cloud Services中建立ExactTarget配置：

1. 在歡迎頁面上，按一下 **Cloud Services**。 (或直接訪問 `https://<hostname>:<port>/etc/cloudservices.html`。)
1. 按一下 **精確目標** 然後 **配置**。 「ExactTarget配置」（ExactTarget配置）窗口開啟。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 輸入標題，或者輸入名稱，然後按一下 **建立**。 的 **ExactTarget設定** 「配置」(configuration)窗口開啟。

   ![chlimage_1](assets/chlimage_1.jpeg)

1. 輸入用戶名、密碼並選擇API終結點(例如， **https://webservice.exacttarget.com/Service.asmx**)。
1. 按一下 **連接到ExactTarget。** 成功連接後，將看到一個成功對話框。 按一下 **確定** 按鈕。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 選擇帳戶（如果可用）。 該帳戶是用於Enterprise 2.0客戶的。 按一下&#x200B;**「確定」**。

   已配置ExactTarget。 可通過按一下 **編輯**。 通過按一下 **轉到ExactTarget**。

1. 現AEM在提供資料擴展功能。 可以導入ExactTarget資料擴展列。 除成功建立ExactTarget配置外，按一下出現的「+」符號可以配置。 可以從下拉清單中選擇任何現有資料擴展。 有關如何配置資料擴展的詳細資訊，請參見 [ExactTarget文檔](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&amp;type=5)。

   導入的資料擴展列稍後可通過 **文本和個性化** 元件。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 通過工具配置ExactTarget {#configuring-exacttarget-via-tools}

要在工具中建立ExactTarget配置：

1. 在歡迎頁面上，按一下 **工具**。 或者直接通過 `https://<hostname>:<port>/misadmin#/etc`。
1. 選擇 **工具**，則 **Cloud Services配置，** 然後 **精確目標**。
1. 按一下 **新建** 開啟**「建立頁面」**窗口。

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. 輸入 **標題** （可選） **名稱**，然後按一下 **建立**。
1. 輸入上一步驟4中概述的配置資訊。 按照此過程完成ExactTarget的配置。

### 添加多個配置 {#adding-multiple-configurations}

要添加多個配置：

1. 在歡迎頁面上，按一下 **Cloud Services** 按一下 **精確目標**。 按一下 **顯示配置** 按鈕。 列出所有可用配置。
1. 按一下 **+** 在「Available configurations（可用配置）」旁邊登錄。 開啟 **建立配置** 的子菜單。 按照上一配置過程建立新配置。
