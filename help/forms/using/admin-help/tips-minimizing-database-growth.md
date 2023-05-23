---
title: 最小化資料庫增長的提示
seo-title: Tips for minimizing database growth
description: 長期進程將進程資料儲存在表單數AEM據庫中。 使用一些簡單的AEM流程設計和產品配置策略，可以最大限度地減少表單資料庫的增長。
seo-description: Long-lived processes store process data in the AEM forms database. The growth of the AEM forms database can be minimized using a few easy process design and product configuration strategies.
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 最小化資料庫增長的提示 {#tips-for-minimizing-database-growth}

長期進程將進程資料儲存在表單數AEM據庫中。 使用一些簡單的AEM流程設計和產品配置策略，可以最大限度地減少表單資料庫的增長。

## 工藝設計提示 {#process-design-tips}

盡可能使用短時間進程。 短期進程不會在資料庫中儲存進程資料。 使用短期進程的缺點是它們的狀態和狀態在管理控制台中沒有跟蹤，並且沒有該進程的歷史記錄。

某些服務操作(如「分配任務」操作（用戶服務）)要求在長期進程中使用它們。 在這種情況下，您可以將流程分割為多個子流程，並盡可能縮短它們的使用時間。 如果使用此策略，則短期子進程應處理大資料項，如文檔值。

少用變數。 在使用長壽命進程時，對於每個進程實例，在資料庫中為進程中的每個變數分配空間。 策略性地使用變數可以節省相當大的空間。 例如，當流程中不再需要舊值時，可以覆蓋變數值。 並刪除已建立且未使用的任何變數。 您可以驗證該流程以查找未使用的變數。

使用簡單變數類型（例如，字串或int），並盡可能避免使用複雜的變數類型。 即使變數不包含值，也會為變數分配資料庫空間。 複雜變數通常需要比簡單變數更大的空間。

## 產品管理提示 {#product-administration-tips}

有效地使用全局文檔儲存(GDS)。 表單伺服器上的GDS目錄用於儲存傳遞給進程中表單一部分的服務的AEM檔案。 為了提高效能，較小的文檔將儲存在記憶體中並保留在資料庫中。

管理控制台顯示「預設文檔最大內聯大小」屬性，用於配置儲存在記憶體中並保留在資料庫中的文檔的最大大小。 (請參閱 [配置常規AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。) 如果將此屬性設定為低值，則大多數文檔會保留在GDS目錄中，而不是在資料庫中。 優點是，當檔案儲存在GDS目錄中時，您可以更輕鬆地刪除它們。
