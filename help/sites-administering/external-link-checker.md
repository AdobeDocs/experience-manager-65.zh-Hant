---
title: 連結檢查器
description: 「連結檢查器」可幫助驗證內部和外部連結，並允許進行連結重寫。
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
source-git-commit: 0b9de3261d8747f3e7107962b6aea1dbdf9d6773
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# 連結檢查器 {#the-link-checker}

內容作者不必擔心驗證其內容頁面中包含的每個連結。

「連結檢查器」會自動運行，以幫助內容作者獲取其連結，包括：

* 在連結添加到內容時驗證它們
* 顯示內容中所有外部連結的清單
* 正在執行連結轉換

連結檢查器 [配置選項](#configuring) 例如，定義內部驗證，允許某些連結或連結模式從驗證中省略，以及重寫連結重寫規則。

連結檢查器將驗證兩者 [內部連結](#internal) 和 [外部連結。](#external)

>[!NOTE]
>
>由於「連結檢查器」會檢查每個內容頁的連結，因此「連結檢查器」會影響大型儲存庫的效能。 在這種情況下，您可能需要 [配置連結檢查器運行頻率](#configuring) 或 [禁用它。](#disabling)

## 內部連結檢查 {#internal}

內部連結是指向儲存庫中其他內容AEM的連結。 可以使用路徑選取器RTE或自定義元件添加內部連結。 例如：

* 您的頁面 `/content/wknd/us/en/adventures/ski-touring.html`
* 包含指向 `/content/wknd/us/en/adventures/extreme-ironing.html` 在 [文本元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

一旦內容作者將內部連結添加到頁面，內部連結即被驗證。 如果連結無效：

* 它將從發佈伺服器中刪除。 連結的文本仍保留，但連結本身已被刪除。
* 它在創作介面中顯示為斷開的連結。

![創作頁面時斷開內部連結](assets/link-checker-invalid-link-internal.png)

## 外部連結檢查 {#external}

外部連結是指向儲存庫外部內容的AEM連結。 可以使用RTE或自定義元件添加外部連結。 例如：

* 您的頁面 `/content/wknd/us/en/adventures/ski-touring.html`
* 包含指向 `https://bunwarmerthermalunderwear.com` 在 [文本元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

通過檢查外部連結的可用性，驗證其語法。 此檢查在可配置的內部非同步完成。 如果連結檢查器發現外部連結無效：

* 它將從發佈伺服器中刪除。 連結的文本仍保留，但連結本身已被刪除。
* 它在創作介面中顯示為斷開的連結。

![創作頁面時斷開內部連結](assets/link-checker-invalid-link-external.png)

另外， [外部連結檢查器](#external-link-checker) interface提供了內容頁面上所有外部連結的概覽。

### 使用外部連結檢查器 {#external-link-checker}

要使用「外部連結檢查器」，請執行以下操作：

1. 使用 **導航**&#x200B;選中 **工具**，則 **站點**。
1. 選擇 **外部連結檢查器** 將顯示所有外部連結的清單。

![「外部連結檢查器」窗口](assets/external-link-checker.png)

顯示以下資訊：

* **狀態**  — 連結的驗證狀態，可以是下列之一：
   * **有效**  — 連結檢查器可以訪問外部連結
   * **待定**  — 已將外部連結添加到網站內容，但尚未通過連結檢查器驗證
   * **無效**  — 鏈路檢查器無法訪問外部鏈路
* **URL**  — 外部連結
* **引用者**  — 包含外部連結的內容頁面
   * 僅填充 [。](#configuring)
* **上次檢查時間**  — 上次連結檢查器驗證外部連結時
   * 檢查連結的頻率 [可配置。](#configuring)
* **上次狀態**  — 當「Link Checked（連結已檢查）」上次檢查外部連結時返回的上次HTML狀態代碼
* **上次可用**  — 自連結檢查器上次使用連結以來的時間
* **上次訪問時間**  — 自上次在創作介面中訪問具有外部連結的頁面以來的時間

通過使用連結清單頂部的兩個按鈕，可以操作窗口的內容：

* **刷新**  — 刷新清單內容
* **檢查**  — 檢查清單中選定的單個外部連結

### 外部連結檢查器的工作原理 {#how-it-works}

儘管易於使用，但「外部連結檢查器」依靠許多服務並瞭解這些服務的工作方式有助於您瞭解如何 [配置連結檢查器](#configuring) 以滿足你的需要。

1. 每當內容作者保存到頁面的任何連結時，都會觸發事件處理程式。
1. 事件處理程式遍歷下的所有內容 `/content` 並檢查新連結或更新的連結，並將它們添加到「連結檢查器」的快取中。
1. 的 **第CQ天連結檢查器服務** 然後按常規計畫執行，以檢查快取中的項是否有效語法。
1. 經語法驗證的連結隨後出現在 [外部連結檢查器](#external-link-checker) 的子菜單。 不過，他們將在 **待定** 狀態。
1. 的 **第CQ天連結檢查器任務** 然後定期執行，通過進行GET呼叫來驗證連結。
1. 的 **第CQ天連結檢查器任務** 然後使用GET調用的結果更新「外部連結檢查器」窗口中的條目。

## 配置連結檢查器 {#configuring}

「Link Checker（連結檢查器）」可在中自動開箱使AEM用。 但是，可以修改許多OSGi配置以更改其行為：

* **第CQ天連結檢查器資訊儲存服務**  — 此服務定義儲存庫中「連結檢查器」快取的大小。
* **第CQ天連結檢查器服務**  — 此服務對外部連結的語法執行非同步檢查。 您可以定義檢查期間，以及檢查器在其它選項中跳過哪些類型的連結。
* **第CQ天連結檢查器任務**  — 此服務執行外部連結的GET驗證。 它允許對時間間隔進行單獨定義，以檢查其他選項之間的不良和良好連結。
* **Day CQ鏈路檢查器變壓器**  — 允許基於用戶定義的規則集轉換連結。

查看文檔 [OSGi配置設定](/help/sites-deploying/osgi-configuration-settings.md) 的子菜單。

## 禁用連結檢查器 {#disabling}

您可以選擇完全禁用「連結檢查器」。 為此：

1. 開啟OSGi控制台。
1. 編輯 **Day CQ鏈路檢查器變壓器**
1. 選中要禁用的選項：
   * **禁用檢查**  — 禁用連結驗證
   * **禁用重寫**  — 禁用連結轉換

>[!NOTE]
>
>如果在開始建立內容後禁用連結檢查，則仍可在 [「外部連結檢查器」窗口](#external-link-checker)，但不再更新。
