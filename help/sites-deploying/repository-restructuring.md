---
title: AEM 6.5中的存放庫重新調整架構
seo-title: Repository Restructuring in AEM 6.5
description: 了解AEM 6.5中重新調整存放庫架構的基本概念和推理
seo-description: Learn about the basics and reasoning behind the repository restructuring in AEM 6.5
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# AEM 6.5中的存放庫重新調整架構{#repository-restructuring-in-aem}

## 簡介 {#introduction}

在AEM 6.4之前，客戶代碼部署在JCR的不可預測區域，在升級時可能會有所變更。 因此，正式的AEM發行通常會覆寫自訂程式碼、設定或內容。 此外，客戶變更有時會覆寫AEM產品代碼或內容，導致產品功能中斷。

透過清楚定義AEM產品代碼和客戶代碼的階層，可以避免這些衝突。

為此，從AEM 6.4開始，為了在未來版本中繼續，內容將從/etc重組為存放庫中的其他資料夾，並附上內容所在位置的准則，請遵循下列高階規則：

* AEM產品程式碼一律會放置在/libs中，且不得由自訂程式碼覆寫
* 自訂程式碼應放置在/apps、/content和/conf中

## 對6.5升級的影響 {#impact-on-upgrades}

升級至AEM 6.5時，/etc底下的大部分內容會複製到存放庫中的其他資料夾中。 這些新位置是參考內容的偏好位置。 不過，我們已嘗試讓AEM 6.5升級回溯相容/etc資料夾中的先前位置，因此在大多數情況下，AEM程式碼會繼續參考舊位置，直到在客戶應用程式中主動（且在許多情況下手動）進行變更為止。 從時間軸的觀點來看，有兩類變更：

* 若使用6.5升級 — 少數/etc重組變更無法回溯相容，因此在AEM 6.5升級中，應規劃並實作修改。
* 未來升級前 — 大部分的/etc重組更改都可以推遲到將來的升級後的某個時間。 如先前所述，AEM 6.5程式碼將繼續參考舊位置，直到修改在客戶版本中實作為止。 雖然沒有應進行變更的強制時間表，但建議您在未來升級前進行變更，因為未來功能可能需仰賴參考的新位置。 此外，根據慣例，特定功能的檔案會參考新位置，因此，如果仍使用舊位置，則可能會造成混淆。

### 重組指導 {#restructuring-guidance}

規劃升級至AEM 6.5時，應參考下列各解決方案頁面，以評估工作成果：

* [所有AEM解決方案共同的存放庫重組](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites存放庫重組](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assets存放庫重組](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets Dynamic Media存放庫重組](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Forms存放庫重組](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communities存放庫重組](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM商務存放庫重組](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

每個頁面包含與必要變更的緊急程度對應的兩個區段。 在「具有6.5升級」一節下的任何項目，都應作為AEM 6.5升級專案的一部分處理。 「未來升級前」下的任何項目都可選擇延遲至升級後。

頁面上的每個項目都包含一個「重新調整指南」欄位，其中詳細說明了與新的6.5儲存庫模型一致的建議技術策略，以便參照先前位於/etc資料夾下的內容的新位置。 其他「附註」欄位可提供任何其他實用內容。
