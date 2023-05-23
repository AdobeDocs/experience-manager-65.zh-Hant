---
title: 6.5中的AEM儲存庫重組
seo-title: Repository Restructuring in AEM 6.5
description: 瞭解6.5中儲存庫重組的基礎知識AEM和推理
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

# 6.5中的AEM儲存庫重組{#repository-restructuring-in-aem}

## 簡介 {#introduction}

在6.AEM4之前，客戶代碼部署在JCR的不可預知的區域，這些區域在升級時可能會發生更改。 因此，正式版本通常會覆AEM蓋自定義代碼、配置或內容。 此外，客戶更改有時會改寫AEM產品代碼或內容，從而破壞產品功能。

通過明確定義產品代AEM碼和客戶代碼的層次結構，可以避免這些衝突。

為此，從AEM6.4開始，並在以後的版本中繼續，內容將從/etc重構到儲存庫中的其他資料夾，以及關於內容放在哪裡的指導原則，遵守以下高級規則：

* 產AEM品代碼將始終放在/lib中，該代碼不能被自定義代碼覆蓋
* 自定義代碼應放在/apps、/content和/conf中

## 對6.5升級的影響 {#impact-on-upgrades}

升級到AEM6.5時，/etc下的大部分內容將在儲存庫中的其他資料夾中複製。 這些新位置是引用內容的首選位置。 但是，每次嘗試將AEM6.5升級向後相容/etc資料夾中的先前位置，因此在大多數情況下，舊位置將繼續被代碼引用，直到客戶應用程式中主動進行更改（在很多情況下是手動進行更改）。 從時間軸透視來看，有兩種更改類別：

* 使用6.5升級 — 少量/etc重組更改不向後相容，因此應在6.5升級中規劃並實施AEM修改。
* 在將來升級之前 — 大多數/etc重組更改都可以推遲到將來升級後的某個時間。 如前所述， AEM 6.5代碼將繼續引用舊位置，直到這些修改作為客戶版本的一部分實施。 雖然沒有強制時間表應進行更改，但建議在將來升級之前進行更改，因為將來的功能可能依賴於引用的新位置。 此外，根據慣例，給定功能的文檔會參考新位置，因此，如果仍在使用舊位置，則可能會令人困惑。

### 重組指導 {#restructuring-guidance}

在計畫升級到AEM6.5時，應參考以下每個解決方案頁，以評估工作量：

* [所有解決方案通用的儲存AEM庫重組](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites資料庫重組](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assets資料庫重組](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM AssetsDynamic Media資料庫重組](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Forms資料庫重組](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communities資料庫重組](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [商AEM務庫重組](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

每頁包含兩個與必要更改的緊急程度相對應的部分。 「With 6.5 Upgrade」（帶6.5升級）部分下的任何內容都應作為6.5升級項AEM目的一部分處理。 「Pror to Future Upgrade（將來升級前）」下的任何內容都可以選擇延遲到升級後。

該頁上的每個條目都包括「重組指導」欄位，該欄位詳細說明了建議的技術策略，以便與新的6.5儲存庫模型保持一致，以便新位置被引用到以前位於/etc資料夾下的內容。 附加的「注釋」欄位提供了任何附加的有用上下文。
