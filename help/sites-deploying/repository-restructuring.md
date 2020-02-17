---
title: AEM 6.5中的資料庫重組
seo-title: AEM 6.5中的資料庫重組
description: 瞭解AEM 6.5中資料庫重組的基本概念和推理
seo-description: 瞭解AEM 6.5中資料庫重組的基本概念和推理
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
translation-type: tm+mt
source-git-commit: 97b2da315fac6f84fcba6d4464bf8dd1d690cfd1

---


# AEM 6.5中的資料庫重組{#repository-restructuring-in-aem}

## 簡介 {#introduction}

在AEM 6.4之前，客戶程式碼部署在JCR的不可預測區域，這些區域可能會因升級而變更。 因此，正式的AEM版本常會覆寫自訂代碼、設定或內容。 此外，客戶變更有時會覆寫AEM產品代碼或內容，突破產品功能。

透過清楚說明AEM產品程式碼和客戶程式碼的階層，可以避免這些衝突。

為此，從AEM 6.4開始，並在未來發行中繼續，內容將從/etc重組為儲存庫中的其他資料夾，以及內容所在位置的准則，並遵守下列高階規則：

* AEM產品程式碼永遠會放在/libs中，而自訂程式碼不能覆寫它
* 自訂代碼應放置在/apps、/content和/conf中

## 對6.5升級的影響 {#impact-on-upgrades}

升級至AEM 6.5時，/etc下的大部分內容會複製到儲存庫中的其他資料夾。 這些新位置是參考內容的首選位置。 不過，我們已嘗試將AEM 6.5升級版向後相容於/etc檔案夾中的先前位置，因此在大多數情況下，舊位置仍會繼續由AEM程式碼參考，直到在客戶的應用程式中主動進行變更（在許多情況下是手動進行）。 從時間軸的角度來看，有兩類變更：

* 有了6.5升級版——少數幾項重組變更無法向後相容，因此應規劃並實作為AEM 6.5升級的一部分。
* 未來升級前——絕大多數的重組更改都可以延遲到將來升級後的某個時間。 如前所述，AEM 6.5程式碼將繼續參照舊位置，直到修改作為客戶版本的一部分實施為止。 雖然沒有強制變更的時間表，但建議在未來升級之前進行，因為未來的功能可能會依賴參考的新位置。 此外，特定功能的檔案將依慣例參照新位置，因此，如果仍在使用舊位置，則可能會令人混淆。

### 重組指導 {#restructuring-guidance}

在規劃升級至AEM 6.5時，應參考下列各解決方案頁面，以評估工作成果：

* [所有AEM解決方案共同的儲存庫重組](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites儲存庫重組](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assets儲存庫重組](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets Dynamic media儲存庫重組](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Forms資料庫重組](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communities儲存庫重組](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM Commerce儲存庫重組](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

每個頁面包含兩個區段，以對應必要變更的緊急性。 AEM 6.5升級專案中應處理「With 6.5 Upgrade」（含6.5升級版）下的任何內容。 「未來升級前」項下的任何項目都可選擇延遲至升級後。

頁面上的每個條目都包含一個「重組指導」欄位，該欄位詳細說明了與新的6.5儲存庫模型一致的建議技術策略，以便以前位於/etc資料夾下的內容引用新位置。 「附加附註」欄位提供任何其他實用的內容。
