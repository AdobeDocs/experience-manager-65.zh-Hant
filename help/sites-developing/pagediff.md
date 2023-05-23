---
title: 開發和頁面差異
seo-title: Developing and Page Diff
description: 開發和頁面差異
seo-description: null
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
source-git-commit: 85895215904b8706830d20f7714de5512b2c3ec2
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---

# 開發和頁面差異{#developing-and-page-diff}

## 功能概述 {#feature-overview}

內容建立是一個迭代過程。 創作時需要能夠看到從一個迭代到另一個迭代的更改。 查看一個頁面版本，然後查看另一個頁面版本效率低下且容易出錯。 作者希望能夠將當前頁面與先前版本並排比較，並突出顯示差異。

頁面差異允許用戶將當前頁面與啟動、早期版本等進行比較。 有關此用戶功能的詳細資訊，請參見 [頁面差異](/help/sites-authoring/page-diff.md)。

## 工序詳細資訊 {#operation-details}

在比較頁面的版本時，用戶希望比較的早期版本會在後台AEM重新建立，以便於比較。 這需要能夠呈現內容 [並排比較](/help/sites-developing/pagediff.md#operation-details)。

此娛樂操作由內部AEM完成，對用戶透明，無需干預。 但是，管理員在查看儲存庫時（例如在CRX DE Lite中）會在內容結構中看到這些重新建立的版本。

比較內容時，會在以下位置重新建立整個樹到要比較的頁面：

`/tmp/versionhistory/`

自動運行清除任務以清除此臨時內容。

## 權限 {#permissions}

以前，在Classic UI中，必須進行特別開發考慮，以便AEM於擴散(例如 `cq:text` 標籤庫，或自定義整合 `DiffService` OSGi服務到元件)。 新的差異功能不再需要此功能，因為差異通過DOM比較在客戶端發生。

但開發人員需要考慮一些限制。

* 此功能使用與「產品」不間隔名稱的CSSAEM類。 如果頁面上包含其他具有相同名稱的自定義CSS類或第三方CSS類，則可能會影響差異的顯示。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由於diff是客戶端，並在頁面載入時執行，因此在客戶端diff服務運行後對DOM的任何調整都不會計算在內。 這可能會影響

   * 用於包括內AJAX容的元件
   * 單頁應用程式
   * 基於Javascript的元件，在用戶交互時操作DOM。

>[!NOTE]
>
>頁面差異比較只適用於具有有效cq:editConfig節點的元件。
