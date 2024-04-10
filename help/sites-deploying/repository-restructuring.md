---
title: AEM 6.5中的存放庫重組
description: 瞭解AEM 6.5中存放庫重新調整的基本知識和推理
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# AEM 6.5中的存放庫重組{#repository-restructuring-in-aem}

## 簡介 {#introduction}

在AEM 6.4之前，客戶程式碼部署在JCR不可預測的區域，這些區域在升級時可能會變更。 因此，正式AEM發行版本通常會覆寫自訂程式碼、設定或內容。 此外，客戶變更有時會覆寫AEM產品程式碼或內容，破壞產品功能。

透過明確界定AEM產品程式碼和客戶程式碼的階層，可以避免這些衝突。

為此，從AEM 6.4開始，並在未來版本中繼續，內容正在從/etc重新構建到存放庫中的其他資料夾，以及有關內容去向的准則，遵守以下高級規則：

* AEM產品程式碼一律會放在/libs中，自訂程式碼不可加以覆寫
* 自訂程式碼應放在/apps、/content和/conf中

## 對6.5升級的影響 {#impact-on-upgrades}

升級至AEM 6.5時，/etc底下內容的大型子集將會在存放庫的其他資料夾中重複。 這些新位置是參照內容的偏好位置。 不過，為了讓AEM 6.5升級能夠回溯相容於/etc資料夾中先前的位置，已做出每次嘗試，所以在大部分情況下，舊位置將繼續由AEM程式碼參考，直到在客戶的應用程式中主動進行變更（且在許多情況下是手動進行）為止。 從時間軸的角度來看，變更分為兩類：

* 升級至6.5 — 有些/etc重組變更無法回溯相容，因此應規劃並實施修改作為AEM 6.5升級的一部分。
* 在未來的升級之前 — 絕大部分/etc重組變更可以延遲到未來升級後的某個時間。 如先前所述，AEM 6.5程式碼將繼續參考舊位置，直到修改作為客戶版本的一部分實施為止。 雖然沒有應進行變更的強制時間表，但建議在將來的升級之前進行這些變更，因為未來的功能可能會依賴參考的新位置。 此外，根據慣例，特定功能的檔案將參照新位置，如果仍在使用舊位置，則可能會造成混淆。

### 重組指南 {#restructuring-guidance}

在規劃升級至AEM 6.5時，請參考下列各解決方案頁面，以評估工作量：

* [所有AEM解決方案通用的存放庫重組](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites存放庫重組](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assets存放庫重組](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets Dynamic Media存放庫重組](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Forms存放庫重組](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communities存放庫重組](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM Commerce存放庫重組](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

每個頁面都有兩個區段，分別對應至必要變更的急迫性。 「使用6.5升級」區段下的任何專案都應在AEM 6.5升級專案中處理。 「未來升級之前」下的任何專案都可選擇延後至升級後。

頁面上的每個專案都包含「重新建構指引」欄位，該欄位詳細說明調整新6.5存放庫模型的建議技術策略，以便新位置參考先前位於/etc資料夾下的內容。 額外的「附註」欄位可提供任何其他有用的內容。
