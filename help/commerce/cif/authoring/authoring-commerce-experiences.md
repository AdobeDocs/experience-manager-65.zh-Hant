---
title: 編寫商務體驗
description: 工作商務體驗
exl-id: 2db51bd7-8fc7-4ae8-8d6f-e5035fbe954d
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# 編寫商務體驗 {#authoring-commerce-experiences}

## 總覽 {#overview}

CIF附加元件運用商務專用功能擴充AEM的製作功能。 這可讓作者不需離開內容，就能存取產品資料和內容，以有效率地建立及管理商務相關體驗。

## 選手 {#pickers}

產品和類別選擇器是強制回應UI對話方塊，可讓AEM作者視需要以舒適的方式尋找和選取產品或類別。 核心元件、內容關聯和產品範本是配置中需要產品目錄資料的典型區域。 選擇器支援各種設定選項，例如多選、變異選和預選值。

### 產品挑選器 {#product-picker}

此選擇器提供瀏覽目錄結構或全文搜索以查找產品的功能。 具有變異的產品在「類型」欄中提供資料夾圖示。 按一下資料夾圖示會開啟所選產品的變體。

![產品選擇器](/help/commerce/cif/assets/authoring/product-picker.png)

按一下上層類別會將作者帶回產品層級。

![產品選擇器](/help/commerce/cif/assets/authoring/product-picker-variation.png)

**範例產品預告**

![未選擇預告元件](/help/commerce/cif/assets/authoring/teaser_component_without_selection.png)

此元件的配置對話框需要產品。 CIF會以SKU作為產品識別碼。 作者可以手動輸入SKU，或按一下資料夾圖示以開啟產品選擇器。 選取並關閉選擇器後，元件對話方塊會顯示所選產品的名稱

![具有選擇的預告元件](/help/commerce/cif/assets/authoring/teaser_component_with_selection.png)

### 類別選擇器 {#category-picker}

此選擇器提供瀏覽目錄結構以查找類別的選件。

![類別選擇器](/help/commerce/cif/assets/authoring/category-picker.png)

**類別輪播範例**

![無選取的輪播元件](/help/commerce/cif/assets/authoring/carousel_component_without_selection.png)

此元件的設定對話方塊需要1 :n類別。 CIF使用UID / ID作為類別識別碼。 作者可以手動輸入UID或按一下資料夾圖示以開啟類別選擇器。 選擇和關閉選擇器後，元件對話框將顯示所選類別的名稱。

![具有選取項目的轉盤元件](/help/commerce/cif/assets/authoring/carousel_component_with_selection.png)

## 通用編輯器 {#universal-editor}

通用編輯器經過擴充，具備存取即時產品資料和相關產品內容的功能。

### 存取產品資料 {#access-product-data}

編輯器的「側」面板中的「資產」索引標籤會選取「產品」類型，以供存取產品資料。 資料會從設定的商務端點擷取為即時。 此篩選器是商務端點的全文搜尋，可尋找特定產品。

![產品資料側面板](/help/commerce/cif/assets/authoring/products-side-panel.png)

與資產類似，產品可以在頁面上傳送（這會建立產品預告元件作為預設值）或元件（目前支援的是產品預告和產品轉盤）。

### 使用RTE在文本欄位中新增連結 {#rte}

CIF產品目錄頁面是即時轉譯的虛擬頁面。 因此，無法內嵌一般AEM頁面的超連結（例如）。 CIF將新動作「商務連結」新增至RTE（RTF編輯器）。 此動作的運作方式與一般的「超連結」動作完全相同，但可讓作者使用選擇器來選取產品或類別。

![RTE](/help/commerce/cif/assets/authoring/RTE.png)

    >[!NOTE]
    >
    >如果同時選取類別和產品，則會採用產品。

這會建立預留位置連結，在轉譯頁面時，該連結會以實際連結取代。

### 存取相關聯的產品內容 {#associated-content}

如果通用編輯器辨識頁面上的1:n產品，側面板會自動顯示「關聯商務內容」索引標籤。 此索引標籤可讓作者快速存取已使用產品加上標籤的AEM內容(請參閱 [使產品資料更豐富，與AEM內容相關聯](./enrich-product-associated-content.md) 以取得詳細資訊)。 如果頁面上有多個產品，此索引標籤會提供下拉式清單，以篩選內容類型和特定產品。 使用內容的運作方式與使用「資產」標籤中的內容完全相同。

![產品資料側面板](/help/commerce/cif/assets/authoring/associated-commerce-content-tab.png)

### 預覽階段產品資料 {#staged-data}

編輯器中的「時間扭曲」模式可讓作者根據「時間扭曲」日期，預覽及瀏覽具有預備產品目錄資料的AEM體驗。

![Timewarp](/help/commerce/cif/assets/authoring/timewarp.png)

如果分段使用的日期，元件會顯示視覺指標。

![分級指標](/help/commerce/cif/assets/authoring/staged-indicator.png)

## Omnisearch {#omnisearch}

使用Omnisearch是從業人員使用全文搜尋來尋找AEM內容和產品目錄資料的簡單方式。 Omnisearch會在AEM和商務後端中執行全文搜尋，以在商務後端和AEM內容中尋找產品目錄物件。 AEM結果也包含以產品/類別資料標籤的內容。

![Omnisearch](/help/commerce/cif/assets/authoring/omnisearch.png)

結果按類型分組。

    >[!NOTE]
    >
    >Omnisearch中的全文搜尋不支援相關聯的內容片段。 使用SKU或UID來尋找相關的內容片段。
