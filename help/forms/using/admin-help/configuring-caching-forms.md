---
title: 設定Forms的快取
seo-title: Configuring caching for Forms
description: 瞭解如何設定快取設定，以及如何叢集考量快取的情形。
seo-description: Learn how to configure cache settings and how to cluster considerations for caches.
uuid: 70f36191-4163-410b-991a-e1481488aea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8a07dddf-1281-45ac-a55e-4333b860a261
exl-id: 6b57d00e-5ba0-41ee-8497-49ecfec5b9ed
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 0%

---

# 設定Forms的快取{#configuring-caching-for-forms}

Forms服務採用在Designer中建立的表單設計，並以各種格式轉譯。

管理控制檯中的「Forms」頁面包含可控制Forms服務快取專案方式的設定。 您可以調整這些設定，以最佳化Forms服務的效能。

Forms服務快取下列專案：

* **表單設計：** Forms服務會快取從存放庫或HTTP來源擷取的表單設計。 此快取可改善效能，因為對於後續的轉譯要求，Forms服務會從快取中擷取表單設計，而非從存放庫擷取。
* **片段與影像：** Forms服務可以快取表單設計中使用的片段和影像。 Forms服務快取這些物件時，會改善效能，因為片段和影像只會在第一次請求時從存放庫讀取。
* **表單：** Forms服務會快取其轉譯的表單。 這類快取可改善效能，因為Forms服務不需要在後續請求中解析及轉譯相同表單。

Forms會將快取儲存在兩個位置：

* **在記憶體中：** 專案儲存在記憶體中以便快速存取。 記憶體中的快取記憶體大小有限，當您重新啟動伺服器時會將其刪除。
* **在磁碟上：** 專案儲存在伺服器的檔案系統中。 磁碟快取記憶體的容量大於記憶體中的快取記憶體，當您重新啟動伺服器時，會保留磁碟快取記憶體。 磁碟快取的位置取決於您的應用程式伺服器。 如需有關變更磁碟快取位置的資訊，請參閱 [設定Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## 指定快取模式 {#specifying-the-cache-mode}

Forms支援兩種快取模式：

* 無條件
* 使用快取檢查點

如果您在快取模式之間切換，請重新啟動Forms服務以使變更生效。 若要重新啟動此服務，請使用Workbench或 [啟動或停止與AEM表單模組關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以取得指示。

當您在模式之間切換時，會自動重設快取檢查點時間。

### 使用無條件快取 {#using-unconditional-caching}

在此模式中，Forms服務收到請求時，會驗證所需的資源（表單設計和任何相關資產，例如片段和影像）。 Forms服務會將存放庫中的資源時間戳記與快取中的資源時間戳記進行比較。 如果快取中的資源較舊，Forms服務會進行更新。

此快取模式可確保使用最近的資源。 但是，效能會受到影響，因為Forms服務會在每個請求中根據存放庫驗證快取的專案。 此快取模式適用於開發和中繼環境，因為這類環境會經常更新資源，而且不會將效能作為首要考量。

**指定無條件快取**

1. 在Administration Console中，按一下「服務> Forms」。
1. 在Forms快取控制設定下，無條件選取並按一下儲存。

### 使用快取檢查點 {#use-the-cache-check-point}

在此模式中，當快取資源的時間戳記早於快取檢查點時間時，Forms服務只會檢查存放庫是否有較新版本的資源。 最後快取檢查點時間會顯示在管理控制檯的Forms頁面上。

在高效能生產環境中，使用這個快取模式時，會考量效能問題，而且資源的變更並不頻繁。 當您想要部署對存放庫資源所做的任何變更時，可以重設快取檢查點。

**指定使用快取檢查點**

1. 在Administration Console中，按一下服務> Forms。
1. 在「Forms快取控制設定」中，只有當最後一次驗證是在快取檢查點時間之前完成時，才會選取，然後按一下「儲存」。

**重設快取檢查點**

1. 在Administration Console中，按一下「服務> Forms」。
1. 在「Forms快取控制設定」下，按一下「快取檢查點」 。

**重設快取內容**

您可以隨時清除快取的內容。 快取重設後，每個表單的第一個請求速度會變慢，因為Forms服務會執行完整的轉譯並建立新的快取內容。

1. 在Administration Console中，按一下「服務> Forms」。
1. 在Forms快取控制設定下，按一下重設快取。

## 正在設定快取設定 {#configuring-cache-settings}

您可以指定Forms用於快取的設定，以最佳化AEM表單環境的效能。

若要存取這些設定，請在Administration Console中按一下「服務> Forms」 。

>[!NOTE]
>
>快取的磁碟需求應等於存放庫。

### 指定全域快取設定 {#specifying-global-cache-settings}

中的設定 **全域快取設定** 區域會影響所有型別的快取。 如果您變更其中一項設定，請重新啟動Forms服務，變更才會生效。 若要重新啟動此服務，請使用Workbench或 [啟動或停止與AEM表單模組關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以取得指示。

**快取檔案大小上限(KB)：** 可儲存在任何記憶體快取中的表單設計或其他資源大小上限（以KB為單位）。 此為全域設定，適用於所有記憶體中的快取。 如果資源大於此值，則不會在記憶體中快取。 預設值為1024 KB。 此設定不會影響磁碟快取。

**表單轉譯快取已啟用：** 依預設，會選取此選項，這表示會快取呈現的表單以供後續擷取。 此設定可改善效能，因為Forms服務只需轉譯特定表單一次，然後使用快取版本。 此選項適用於表單設計的快取屬性。 如需有關在表單設計中設定此值的資訊，請參閱設計工具說明。

### 快取表單設計 {#caching-form-designs}

Forms服務收到轉譯請求時，會從存放庫擷取表單設計並加以快取。 此快取可改善效能，因為對於後續的轉譯要求，Forms服務會從快取中擷取表單設計，而非從存放庫擷取。

Forms服務一律會在磁碟上快取表單設計。 如果表單設計儲存在伺服器上，則這些檔案會被視為磁碟快取。 Forms服務也會根據中的設定，在記憶體中快取表單設計 **在記憶體範本快取中** 區域。 如果您變更其中任何設定，請重新啟動Forms服務，變更才會生效。 若要重新啟動此服務，請使用Workbench或 [啟動或停止與AEM表單模組關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以取得指示。

**範本組態快取大小：** 要保留在記憶體中的範本組態物件數目上限。 預設值為 100。建議您將此值設定為大於或等於「範本快取大小」值。 此設定不會影響磁碟快取。

**範本快取大小：** 要保留在記憶體中的範本內容物件最大數量。 預設值為 100。此設定不會影響磁碟快取。

**已啟用：** 預設會選取此核取方塊，表示在記憶體中快取表單範本。 未選取此選項時，表單範本只會快取在磁碟上。

### 快取轉譯的表單 {#caching-rendered-forms}

Forms服務會快取轉譯的表單，因此不需要在後續請求中解析及轉譯相同的表單。 呈現的表單會快取在磁碟和記憶體中。

這些設定位於 **在記憶體表單轉譯快取中** 區域。 如果您變更其中一項設定，請重新啟動Forms服務，變更才會生效。 若要重新啟動此服務，請使用Workbench或 [啟動或停止與AEM表單模組關聯的服務](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) 以取得指示。

**快取大小：** 指定記憶體內部快取中可容納的已轉譯表單數上限。 預設值為 100。此設定不會影響磁碟快取。

**已啟用：** 依預設，此選項是選取的，表示演算後的表單會快取在記憶體中。 未選取此選項時，轉譯的表單僅會快取在磁碟上。

### 快取片段和影像 {#caching-fragments-and-images}

Forms服務會快取磁碟上表單設計中所使用的片段和影像。 這麼做可改善效能，因為片段和影像僅在第一次請求時才會從存放庫讀取。 接著，在後續的請求中，Forms服務會從磁碟快取讀取片段和影像。 片段和影像隻會快取在磁碟上，而不會在記憶體中。

您可以使用以下設定來控制磁碟上片段和影像的快取。 這些設定位於 **範本資源快取設定** 區域：

**資源快取** 從清單中選取下列其中一個選項：

**已啟用片段和影像：** Forms服務可快取片段和影像。 這是預設選項。

**為片段啟用：** Forms服務快取片段，但不快取影像。

**已停用：** Forms服務不會快取片段或影像。

**清除間隔（秒）：** 指定Forms服務移除舊版無效快取檔案的頻率。 Forms服務沒有移除有效的快取檔案。 如果您變更清除間隔，請重新啟動Forms服務，變更才會生效。 若要重新啟動此服務，請使用Workbench，或參閱啟動或停止與AEM表單模組相關聯的服務以取得指示。 預設值為600秒。

## 快取的叢集考量事項 {#clustering-considerations-for-caches}

在叢集環境中，每個節點都會維護自己的記憶體內部和磁碟快取。 每個節點上的快取內容取決於該節點上已轉譯的表單。

叢集的每個節點上的快取位置必須相同（相同的磁碟和路徑）。 請勿將快取放在共用存放裝置上。

如果您使用管理控制檯中的「Forms」頁面來變更特定節點的快取設定，則當請求進入其他節點時，也會更新該節點上的快取設定。 此行為也會套用至「重設快取」按鈕。 如果您按一下某個節點的「重設快取」按鈕，快取會立即從該節點中移除。 當請求進入其他節點時，會清除該節點上的快取。
