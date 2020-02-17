---
title: 將資料庫增長降至最低的提示
seo-title: 將資料庫增長降至最低的提示
description: 長期的流程會將流程資料儲存在AEM表單資料庫中。 使用幾種簡單的流程設計和產品設定策略，可將AEM表單資料庫的成長降至最低。
seo-description: 長期的流程會將流程資料儲存在AEM表單資料庫中。 使用幾種簡單的流程設計和產品設定策略，可將AEM表單資料庫的成長降至最低。
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 將資料庫增長降至最低的提示 {#tips-for-minimizing-database-growth}

長期的流程會將流程資料儲存在AEM表單資料庫中。 使用幾種簡單的流程設計和產品設定策略，可將AEM表單資料庫的成長降至最低。

## 流程設計提示 {#process-design-tips}

盡可能使用短時間的流程。 短期進程不會將進程資料儲存在資料庫中。 使用短時間進程的缺點是，在管理控制台中不會跟蹤其狀態和狀態，並且沒有進程的歷史記錄。

某些服務操作(如「分配任務」操作（用戶服務）)要求它們用於長期進程。 在這種情況下，您可以將流程分割為數個子流程，並盡可能縮短流程的使用時間。 如果您使用此策略，短期的子流程應處理大型資料項目，例如檔案值。

謹慎使用變數。 使用長壽命進程時，對於每個進程實例，在資料庫中為進程中的每個變數分配空間。 策略性地使用變數可節省大量空間。 例如，當流程中不再需要舊值時，您可以覆寫變數值。 並刪除您已建立且未使用的任何變數。 您可以驗證尋找未使用變數的程式。

使用簡單的變數類型（例如字串或int），並盡可能避免使用複雜的變數類型。 即使變數不包含值，仍會為變數分配資料庫空間。 複雜變數的空間通常比簡單變數要大。

## 產品管理提示 {#product-administration-tips}

有效地使用全域檔案儲存(GDS)。 表單伺服器上的GDS目錄可用來儲存傳遞至屬於AEM表單一部分的服務的檔案，除其他外。 為了改善效能，較小的檔案會儲存在記憶體中並保存在資料庫中。

管理控制台公開「預設檔案最大內嵌大小」屬性，以設定儲存在記憶體中並保存在資料庫中的檔案大小上限。 (請參 [閱「設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)」。)如果將此屬性設定為低值，則大多數文檔都保存在GDS目錄中，而不是保存在資料庫中。 優點是，當檔案儲存在GDS目錄時，不再需要時，您可以更輕鬆地刪除這些檔案。
