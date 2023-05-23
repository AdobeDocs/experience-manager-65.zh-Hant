---
title: 為Forms配置快取
seo-title: Configuring caching for Forms
description: 瞭解如何配置快取設定以及如何為快取集群注意事項。
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

# 為Forms配置快取{#configuring-caching-for-forms}

Forms服務採用以設計器建立的形式設計，並以各種格式呈現。

管理控制台中的Forms頁包含控制Forms服務快取項目的方式的設定。 您可以調整這些設定以優化Forms服務的效能。

Forms服務快取以下項：

* **窗體設計：** Forms服務快取它從儲存庫或HTTP源檢索的表單設計。 此快取提高了效能，因為對於後續的呈現請求，Forms服務從快取而不是從儲存庫檢索表單設計。
* **片段和影像：** Forms服務可以快取用於表單設計的片段和影像。 當Forms服務快取這些對象時，它會提高效能，因為片段和影像僅在第一個請求時從儲存庫中讀取。
* **表格：** Forms服務快取它呈現的表單。 這種類型的快取提高了效能，因為Forms服務不需要在後續請求中解析和呈現相同的表單。

Forms將快取儲存在兩個位置：

* **記憶體中：** 項儲存在記憶體中以便快速訪問。 記憶體中快取的大小有限，在重新啟動伺服器時將被刪除。
* **磁碟上：** 項儲存在伺服器的檔案系統中。 磁碟快取的容量比記憶體快取大，並且在重新啟動伺服器時保留。 磁碟快取的位置取決於應用程式伺服器。 有關更改磁碟快取位置的資訊，請參見 [配置Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。

## 指定快取模式 {#specifying-the-cache-mode}

Forms支援兩種快取模式：

* 無條件
* 使用快取檢查點

如果在快取模式之間切換，請重新啟動Forms服務以使更改生效。 要重新啟動此服務，請使用Workbench或查看 [啟動或停止與表單模組關聯AEM的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 的雙曲餘切值。

在模式之間切換時，快取檢查點時間會自動重置。

### 使用無條件快取 {#using-unconditional-caching}

在這種模式下，當Forms服務收到請求時，它驗證所需的資源（表單設計和任何相關資產，如片段和影像）。 Forms服務將儲存庫中資源的時間戳與快取中資源的時間戳進行比較。 如果快取中的資源較舊，Forms服務會更新它。

此快取模式確保使用最新資源。 但是，效能會受到影響，因為Forms服務會針對每個請求的儲存庫驗證快取項。 此快取模式適用於頻繁更新資源且效能不是主要問題的開發和轉儲環境。

**指定無條件快取**

1. 在管理控制台中，按一下「服務」>「Forms」。
1. 在「Forms快取控制設定」下，選擇「無條件」，然後按一下「保存」。

### 使用快取檢查點 {#use-the-cache-check-point}

在此模式下，當快取資源的時間戳早於快取檢查點時間時，Forms服務只檢查儲存庫中是否有較新版本的資源。 上次快取檢查點時間顯示在管理控制台的Forms頁上。

在高效能生產環境中使用此快取模式，在這些環境中，效能是一個問題，並且資源變化很少。 當要部署對儲存庫資源所做的任何更改時，可以重置快取檢查點時間。

**指定快取檢查點的使用**

1. 在管理控制台中，按一下「服務」>「Forms」。
1. 在「Forms快取控制設定」下，僅在快取檢查點時間之前完成了上次驗證時才選擇，然後按一下「保存」。

**重置快取檢查點**

1. 在管理控制台中，按一下「服務」>「Forms」。
1. 在「Forms快取控制設定」下，按一下快取檢查點。

**重置快取內容**

可以隨時清除快取的內容。 快取重置後，對每個表單的第一個請求會變慢，因為Forms服務執行完整呈現並建立新的快取內容。

1. 在管理控制台中，按一下「服務」>「Forms」。
1. 在「Forms快取控制設定」下，按一下「重置快取」。

## 配置快取設定 {#configuring-cache-settings}

您可以指定Forms用於快取的設定，這可以優化表單環境AEM的效能。

要訪問這些設定，請在管理控制台中按一下「服務」>「Forms」。

>[!NOTE]
>
>快取的磁碟要求應等於儲存庫。

### 指定全局快取設定 {#specifying-global-cache-settings}

中的設定 **全局快取設定** 區域會影響所有類型的快取。 如果更改了其中任一設定，請重新啟動Forms服務以使更改生效。 要重新啟動此服務，請使用Workbench或查看 [啟動或停止與表單模組關聯AEM的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 的雙曲餘切值。

**最大快取文檔大小(KB):** 表單設計或其他資源的最大大小（以KB為單位），可以儲存在任何記憶體快取中。 這是適用於所有記憶體快取的全局設定。 如果資源大於此值，則它不會快取在記憶體中。 預設值為1024千位元組。 此設定不影響磁碟快取。

**已啟用窗體呈現快取：** 預設情況下，此選項處於選中狀態，這意味著已呈現的表單將快取以用於後續檢索。 此設定提高了效能，因為Forms服務只需呈現一次特定表單，然後使用快取版本。 此選項與窗體設計的快取屬性一起使用。 有關在表單設計中配置此值的資訊，請參閱設計器幫助。

### 快取表單設計 {#caching-form-designs}

當Forms服務收到呈現請求時，它將從儲存庫中檢索表單設計並快取它。 此快取提高了效能，因為對於後續的呈現請求，Forms服務從快取而不是從儲存庫檢索表單設計。

Forms服務始終在磁碟上快取表單設計。 如果表單設計儲存在伺服器上，則這些檔案被視為磁碟快取。 Forms服務還根據中的設定將表單設計快取到記憶體中 **記憶體模板快取中** 的子菜單。 如果更改了這些設定中的任何一個，請重新啟動Forms服務以使更改生效。 要重新啟動此服務，請使用Workbench或查看 [啟動或停止與表單模組關聯AEM的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 的雙曲餘切值。

**模板配置快取大小：** 要保留在記憶體中的模板配置對象的最大數量。 預設值為 100。建議將此值設定為大於或等於「模板快取大小」值。 此設定不影響磁碟快取。

**模板快取大小：** 要保留在記憶體中的模板內容對象的最大數量。 預設值為 100。此設定不影響磁碟快取。

**已啟用：** 預設情況下，此複選框處於選中狀態，表示表單模板已快取到記憶體中。 如果未選擇此選項，則表單模板僅快取在磁碟上。

### 快取已呈現的表單 {#caching-rendered-forms}

Forms服務快取所呈現的表單，以便它不需要在後續請求中解析和呈現相同的表單。 呈現的表單在磁碟和記憶體中都被快取。

這些設定位於 **記憶體表單呈現快取** 的子菜單。 如果更改了其中任一設定，請重新啟動Forms服務以使更改生效。 要重新啟動此服務，請使用Workbench或查看 [啟動或停止與表單模組關聯AEM的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 的雙曲餘切值。

**快取大小：** 指定可駐留在記憶體快取中的最大呈現表單數。 預設值為 100。此設定不影響磁碟快取。

**已啟用：** 預設情況下，此選項處於選中狀態，表示已呈現的表單將快取在記憶體中。 如果未選擇此選項，則僅在磁碟上快取呈現的表單。

### 快取片段和影像 {#caching-fragments-and-images}

Forms服務在磁碟上快取用於表單設計的片段和影像。 這提高了效能，因為只有在第一個請求時才從儲存庫中讀取片段和影像。 然後，在隨後的請求中，Forms服務從磁碟快取中讀取片段和影像。 片段和影像只快取在磁碟上，而不快取在記憶體中。

可以使用以下設定來控製片段和映像的磁碟上快取。 這些設定位於 **模板資源快取設定** 區域：

**資源快取** 從清單中選擇以下選項之一：

**為片段和影像啟用：** Forms服務快取片段和影像。 這是預設選項。

**為片段啟用：** Forms服務快取片段，但不快取映像。

**已禁用：** Forms服務不快取片段或影像。

**清理間隔（秒）:** 指定Forms服務刪除舊的無效快取檔案的頻率。 Forms服務未刪除有效的快取檔案。 如果更改了清理間隔，請重新啟動Forms服務以使更改生效。 要重新啟動此服務，請使用Workbench或參閱啟動或停止與表單模組AEM關聯的服務。 預設值為600秒。

## 快取的群集注意事項 {#clustering-considerations-for-caches}

在群集環境中，每個節點維護其自己的記憶體和磁碟快取。 每個節點上的快取內容取決於該節點上已呈現的表單。

快取在群集的每個節點上的位置必須相同（磁碟和路徑相同）。 不要將快取放在共用儲存上。

如果您使用管理控制台中的「Forms」頁來更改特定節點的快取設定，則當請求到該節點時，其他節點上的快取設定會更新。 此行為也適用於「重置快取」按鈕。 如果按一下某個節點的「重置快取」按鈕，則會立即從該節點中刪除快取。 當請求進入該節點時，會清除其他節點上的快取。
