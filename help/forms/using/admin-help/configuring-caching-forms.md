---
title: 設定Forms的快取
seo-title: Configuring caching for Forms
description: 了解如何配置快取設定，以及如何為快取設定叢集考量事項。
seo-description: Learn how to configure cache settings and how to cluster considerations for caches.
uuid: 70f36191-4163-410b-991a-e1481488aea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8a07dddf-1281-45ac-a55e-4333b860a261
exl-id: 6b57d00e-5ba0-41ee-8497-49ecfec5b9ed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 0%

---

# 設定Forms的快取{#configuring-caching-for-forms}

Forms服務會採用在Designer中建立的表單設計，並以各種格式轉譯。

管理控制台中的Forms頁面包含可控制Forms服務快取項目的方式的設定。 您可以調整這些設定，以最佳化Forms服務的效能。

Forms服務會快取下列項目：

* **表單設計：** Forms服務快取其從存放庫或HTTP來源擷取的表單設計。 此快取可改善效能，因為對於後續的轉譯請求，Forms服務會從快取（而非存放庫）擷取表單設計。
* **片段和影像：** Forms服務可快取表單設計中使用的片段和影像。 Forms服務快取這些物件時，會改善效能，因為只會在第一個要求時從存放庫讀取片段和影像。
* **表單：** Forms服務會快取其轉譯的表單。 這類快取可改善效能，因為Forms服務不需要在後續請求中解析及轉譯相同的表單。

Forms會將快取儲存在兩個位置：

* **記憶體中：** 項儲存在記憶體中以便快速訪問。 記憶體內快取的大小有限，當您重新啟動伺服器時會刪除該快取。
* **磁碟上：** 項儲存在伺服器的檔案系統中。 磁碟快取的容量比記憶體內快取大，當您重新啟動伺服器時，它會保留。 磁碟快取的位置取決於您的應用程式伺服器。 有關更改磁碟快取位置的資訊，請參見 [配置Forms位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## 指定快取模式 {#specifying-the-cache-mode}

Forms支援兩種快取模式：

* 無條件
* 使用快取檢查點

如果您在快取模式之間切換，請重新啟動Forms服務，讓變更生效。 若要重新啟動此服務，請使用Workbench或參閱 [啟動或停止與AEM表單模組相關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 的說明。

在模式之間切換時，快取檢查點時間會自動重置。

### 使用無條件快取 {#using-unconditional-caching}

在此模式中，Forms服務收到要求時，會驗證所需的資源（表單設計和任何相關資產，例如片段和影像）。 Forms服務會比較存放庫中資源的時間戳記與快取中資源的時間戳記。 如果快取中的資源較舊，Forms服務會更新它。

此快取模式可保證使用最新的資源。 不過，效能會受到影響，因為Forms服務會透過每個要求，根據存放庫驗證快取的項目。 此快取模式適用於資源經常更新且效能不是主要考量的開發和預備環境。

**指定無條件快取**

1. 在管理主控台中，按一下「服務> Forms」。
1. 在「Forms快取控制設定」下，選擇「無條件」，然後按一下「保存」。

### 使用快取檢查點 {#use-the-cache-check-point}

在此模式中，當快取資源的時間戳記早於快取檢查點時間時，Forms服務只會檢查存放庫是否有較新版本的資源。 最後一個快取檢查點時間會顯示在「管理控制台」的「Forms」頁面上。

在效能是問題且資源變更不頻繁的高效能生產環境中使用此快取模式。 當要部署對儲存庫資源所做的任何更改時，可以重置快取檢查點時間。

**指定快取檢查點的使用**

1. 在Administration Console中，按一下「服務> Forms」。
1. 在「Forms快取控制設定」下，僅在快取檢查點時間之前完成其上次驗證時選取，然後按一下「儲存」。

**重置快取檢查點**

1. 在管理主控台中，按一下「服務> Forms」。
1. 在「Forms快取控制設定」下，按一下「快取檢查點」。

**重置快取內容**

您可以隨時清除快取的內容。 快取重設後，每個表單的第一個要求會較慢，因為Forms服務會執行完整轉譯並建立新的快取內容。

1. 在管理主控台中，按一下「服務> Forms」。
1. 在「Forms快取控制設定」下，按一下「重設快取」。

## 配置快取設定 {#configuring-cache-settings}

您可以指定Forms用於快取的設定，以便最佳化AEM表單環境的效能。

若要存取這些設定，請在管理控制台中按一下「服務> Forms」。

>[!NOTE]
>
>快取的磁碟要求應等於儲存庫。

### 指定全局快取設定 {#specifying-global-cache-settings}

中的設定 **全局快取設定** 區域會影響所有類型的快取。 如果您變更其中一項設定，請重新啟動Forms服務，讓變更生效。 若要重新啟動此服務，請使用Workbench或參閱 [啟動或停止與AEM表單模組相關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 的說明。

**最大快取文檔大小(KB):** 表單設計或其他資源的最大大小（以千位元組為單位），可以儲存在任何記憶體快取中。 此全局設定適用於所有記憶體內快取。 如果資源大於此值，則不會快取記憶體中的資源。 預設值為1024 KB。 此設定不影響磁碟快取。

**表單呈現快取已啟用：** 依預設，會選取此選項，這表示已轉譯的表單會快取以供後續擷取。 此設定可改善效能，因為Forms服務只需轉譯特定表單一次，便可使用快取版本。 此選項適用於表單設計的快取屬性。 有關在表單設計中配置此值的資訊，請參閱設計工具幫助。

### 快取表單設計 {#caching-form-designs}

Forms服務收到轉譯請求時，會從存放庫擷取表單設計並加以快取。 此快取可改善效能，因為對於後續的轉譯請求，Forms服務會從快取（而非存放庫）擷取表單設計。

Forms服務一律會在磁碟上快取表單設計。 如果表單設計儲存在伺服器上，則這些檔案將被視為磁碟快取。 Forms服務也會根據 **記憶體模板快取** 的上界。 如果您變更其中任何設定，請重新啟動Forms服務，讓變更生效。 若要重新啟動此服務，請使用Workbench或參閱 [啟動或停止與AEM表單模組相關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 的說明。

**模板配置快取大小：** 要保留在記憶體中的模板配置對象的最大數量。 預設值為 100。建議您將此值設定為大於或等於「範本快取大小」值。 此設定不影響磁碟快取。

**模板快取大小：** 要保留在記憶體中的模板內容對象的最大數量。 預設值為 100。此設定不影響磁碟快取。

**已啟用：** 依預設，會選取此核取方塊，表示表單範本會快取於記憶體中。 未選擇此選項時，僅快取磁碟上的表單模板。

### 快取呈現的表單 {#caching-rendered-forms}

Forms服務會快取已轉譯的表單，因此不需要在後續請求中解析和轉譯相同的表單。 已呈現的表單會快取在磁碟和記憶體中。

這些設定位於 **記憶體表單呈現快取** 的上界。 如果您變更其中一項設定，請重新啟動Forms服務，讓變更生效。 若要重新啟動此服務，請使用Workbench或參閱 [啟動或停止與AEM表單模組相關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 的說明。

**快取大小：** 指定可駐留在記憶體內快取中的已呈現表單的最大數量。 預設值為 100。此設定不影響磁碟快取。

**已啟用：** 依預設，會選取此選項，表示已轉譯的表單會快取於記憶體中。 未選擇此選項時，僅對磁碟快取呈現的表單。

### 快取片段和影像 {#caching-fragments-and-images}

Forms服務會在磁碟上快取表單設計中使用的片段和影像。 這會改善效能，因為片段和影像只會從第一個要求的存放庫讀取。 接著，在後續的請求中，Forms服務會從磁碟快取中讀取片段和影像。 片段和影像僅快取在磁碟上，而不是記憶體中。

您可以使用下列設定來控製片段和影像的磁碟上快取。 這些設定位於 **模板資源快取設定** 區域：

**資源快取** 從清單中選取下列其中一個選項：

**為片段和影像啟用：** Forms服務會快取片段和影像。 這是預設選項。

**為片段啟用：** Forms服務會快取片段，但不會快取影像。

**已禁用：** Forms服務不會快取片段或影像。

**清理間隔（秒）:** 指定Forms服務移除舊無效快取檔案的頻率。 Forms服務未刪除有效的快取檔案。 如果您變更清理間隔，請重新啟動Forms服務，讓變更生效。 若要重新啟動此服務，請使用Workbench或參閱啟動或停止與AEM表單模組相關聯的服務以取得指示。 預設值為600秒。

## 快取的叢集考量事項 {#clustering-considerations-for-caches}

在群集環境中，每個節點都會維護其自己的記憶體和磁碟快取。 每個節點上的快取內容取決於在該節點上呈現的表單。

快取的位置在群集的每個節點上必須相同（磁碟和路徑相同）。 請勿將快取放置在共用儲存上。

如果您使用管理控制台中的「Forms」頁面來變更特定節點的快取設定，則當請求傳至該節點時，其他節點上的快取設定會更新。 此行為也適用於「重設快取」按鈕。 如果按一下某個節點的「重置快取」按鈕，則會立即從該節點中刪除快取。 當請求傳至該節點時，會清除其他節點上的快取。
