---
title: 開發和頁面差異
description: 瞭解如何開發及利用Adobe Experience Manager中的頁面差異功能。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---

# 開發和頁面差異{#developing-and-page-diff}

## 功能概述 {#feature-overview}

內容建立是一個反複的過程。 以高效率撰寫需要能夠檢視反複專案之間的變更。 檢視一個頁面版本然後檢視另一個頁面版本會效率低下，並容易發生錯誤。 作者希望能夠並排比較目前頁面與先前版本，並醒目提示差異。

頁面差異可讓使用者將目前頁面與啟動項、舊版等專案進行比較。 如需此使用者功能的詳細資訊，請參閱 [頁面差異](/help/sites-authoring/page-diff.md).

## 作業詳細資料 {#operation-details}

比較頁面的版本時，使用者想要比較的先前版本會由AEM在背景重新建立，以方便差異比較。 這是為了能夠呈現內容 [用於並排比較](/help/sites-developing/pagediff.md#operation-details).

此重新建立操作由AEM內部完成，對使用者而言是透明的，不需要任何干涉。 但是，管理員檢視存放庫(例如，在CRXDE Lite中)時，會在內容結構中看到這些重新建立的版本。

比較內容時，系統會在下列位置重新建立整個樹狀結構，一直到要比較的頁面為止：

`/tmp/versionhistory/`

清除工作會自動執行，以清除此暫存內容。

## 權限 {#permissions}

先前，在傳統UI中，必須進行特殊的開發考量，以促進AEM差異(例如使用 `cq:text` 標籤程式庫，或自訂整合 `DiffService` OSGi服務轉換為元件)。 新的diff功能不再需要此專案，因為差異是透過DOM比較在使用者端發生。

不過，開發人員必須考慮一些限制。

* 此功能使用的CSS類別未與AEM產品建立名稱空間。 如果頁面上包含其他相同名稱的自訂CSS類別或協力廠商CSS類別，差異的顯示可能會受到影響。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 由於diff是使用者端並在頁面載入時執行，因此使用者端diff服務執行後對DOM所做的任何調整都不會計算在內。 這可能會影響

   * 使用AJAX來包含內容的元件
   * 單頁應用程式
   * 可在使用者互動時操控DOM的JavaScript型元件。

>[!NOTE]
>
>頁面差異比較僅適用於具有有效cq：editConfig節點的元件。
