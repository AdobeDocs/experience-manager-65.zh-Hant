---
title: 儲存庫中的模型
seo-title: 儲存庫中的模型
description: 'null'
seo-description: 'null'
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# 儲存庫中的模型{#models-in-repository}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

模型包含一組資料類型，可定義內容服務最終將呈現的屬性。 模型還定義了其他模型之間的關係，以強化資料完整性。

身為開發人員，您應熟悉儲存庫中的模型結構。 您可以根據應用程式需求建立自己的模型和實體。

## 建立模型類型 {#creating-model-types}

在 */libs/settings/mobileapps/model-types下有兩種系統提供的型號類型*。 如果要覆蓋系統模型類型， *Mobileapps/model-types* node will need to be created under the configuration node you wish the override to on.

例如，如果您已在 */conf/myconf1* 和 */conf/myconf2* 上建立配置，並且希望僅覆蓋 *conf1上的系統模型類型，則您會在Conf1的設定下建立***** mobileapps/model-nodeNode。

如果要允許將資料類型添加到模型中，模型類型必須有一個名為「scq:Page」類型的子節點和資源類型為 *wcm/swables/components/swables*。

支架頁面也必須包含 *PageContent節點上的dataTypesConfig* 屬性，指出將允許使用此類型建立的資料類型模型。

>[!NOTE]
>
>「支 **架** 」是定義實體可根據模型編輯的資料類型的頁面。 您也可以設定每個資料類型，以定義欄位在UI中的呈現方式，以及資料值的保存方式。

### 資料類型設定 {#data-types-config}

資料類型配置節點包含資料類型項的清單。 每個資料類型項指定資料類型在模型編輯器中的顯示方式，以及資料類型在最終由實體呈現時需要如何保存。

| **屬性名稱** | **說明** |
|---|---|
| fieldIcon | coralUI圖示類別，以表示資料類型 |
| fieldPropResourceType | 用於顯示配置資料類型的所有屬性的元件 |
| fieldProperties | fieldPropResourceType為 *mobileapps/caas/gui/components/models/editor/datatypes/field時使用的屬性元件多值清單* |
| fieldResourceType | resourceData類型（即將在實體編輯器中呈現屬性的元件）的持續節點類型 |
| fieldViewResourceType | 元件，用於在模型編輯器視圖中呈現資料類型（如果省略此屬性，將使用fieldResourceType） |
| fieldTitle | 將在模型編輯器中顯示的資料類型的名稱 |
| multiFieldResourceType | 在選擇多值時用於持久節點的資源類型 |
| renderType | 用戶端轉換提示 |

### 資料類型設定覆蓋 {#data-types-config-overlay}

&#39;dataTypesConfig&#39;屬性支援Sling資源合併。 這表示系統模型類型（甚至自訂模型類型）所使用的資料類型，可使用覆蓋節點加以自訂。

需要建 *立/libs/settings/mobileapps/models/formbuilderconfig/datatypes的覆蓋* ，然後視需要自訂。

例如，可新增字串資料類型的覆蓋，以便將fieldResourceType變更為自訂元件。

如需Sling Resource Merging的詳細資訊，請參閱 [Using Sling Resource Merger in AEM](/help/sites-developing/sling-resource-merger.md)。

![chlimage_1-7](assets/chlimage_1-7.png)

### 資料類型 {#data-types}

模型資料類型是一種表單元件，能夠包括發佈表單時要包括的資料。 資料類型元件可視需要變得複雜。 自訂資料類型的範例可以是特定國家／地區的位址區塊，以避免使用基本資料類型隨時重新建立。

請參閱「/libs/mobileapps/caas/components/form/contentreference」作為自訂資料類型的範例。

所有原始資料類型都使用現有的Granite表格元件。 請參閱： [https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

然後，任何自訂資料類型都可新增至資料類型設定，供模型編輯器使用。

## 建立模型 {#creating-models}

所有所需的模型類型和資料類型都開發完成後，您就可以開始建立模型。 作者最終將使用模型來建立實體，內容服務會使用這些實體來轉換其資料。

建立模型包括根據當前配置選擇允許的模型類型，然後提供標題和說明。

若要瞭解如何從儀表板建立和管理模型，請參閱「行動應 [用程式」的編寫章節下的「建立模型](/help/mobile/administer-mobile-apps.md) 」。

### 模型的屬性 {#properties-of-a-model}

下表顯示為模型定義的屬性：

| **屬性名稱** | **說明** |
|---|---|
| 模型標題 | 模型名稱 |
| 說明 | 模型說明 |
| 縮圖 | 模型的縮圖影像 |
| 模型類型 | 模型類型（這可以是簡單字串或實際元件的路徑） |
| 允許的子項 | 允許作為此模板子項的模板的路徑 |
| 允許的父項 | 允許作為此模板父項的模板的路徑 |

>[!NOTE]
>
>允 *許的子項*** 和允許的父項屬性遵循與「頁面」模板相同的規則。 如需詳細資訊，請參 [閱頁面範本](/help/sites-developing/page-templates-static.md)。
>
>參照 *Model Type* 屬性，所有模型都必須有超類型的 *mobileapps/caas/components/data/entity* ，但可以有允許自訂內容傳送的子類型。 確保所有模型類型都是獨一無二的，也有助於內容服務的客戶區分資料中的物件。

### 編輯模型 {#editing-a-model}

編輯模型時，需要開啟與模型相關的支架對話框表單以進行編輯。 通常，腳手架是模型的子節點，但如果需要，它可以使用&#39;cq:swatherble&#39;屬性指定其路徑，以定位在模型外。 如果您想要在多個需要不同屬性的模型之間共用相同的支架，這是很有用的。

當模型的支架位置時，模型編輯器將會呈現「jcr:content/cq:dialog/content」下的任何內容。 用戶端表單產生器引擎目前僅支援最多3欄的固定版面。 在渲染的表單對話框的右側，將列出資料類型配置中指定的所有資料類型。 您可以按一下資料類型來編輯。 然後，右邊欄將切換至所選資料類型的屬性頁籤。 將新的資料類型拖曳至預覽畫布，即可新增這些資料類型。 按一下「保存」(Save)將更改傳播到伺服器。 按一下「取消」(Cancel)關閉模型編輯器。

>[!NOTE]
>
>所有模型都是範本，因此它們會遵循所有AEM範本規則。 這允許使用屬性，如 ** allowedParent和 *allowedChildren* properties。 這些在基於模型建立新圖元時是有效的。 模板規則將確保實體只能基於某些模型（取決於其層次）。
>
>若要瞭解如何從控制面板編輯模型，請參閱「行 [動應用程式」的「編寫」區段下的「建立模型](/help/mobile/administer-mobile-apps.md) 」。

### 系統型號 {#system-models}

提供兩種預定義的系統模型，以便簡單地重複使用。 無法編輯這些模型。

**頁面模型** 「頁面」模型提供快速方法，可重複使用網站中的現有內容，以便透過內容服務傳送。

基於「頁面」模型的ersourceType實體為：mobileapps/caas/components/data/pages

路徑：「網站」頁面的路徑。 內容服務處理常式會呈現此路徑（及其子系）的內容。

**資產模型** 「資產」模型提供快速方法，可重複使用Assets中的現有內容，以便透過內容服務傳遞。

基於「頁面」模型的ersourceType實體為： *mobileapps/caas/components/data/assets。*

資產清單：資產的路徑清單。 每個資產都會新增為子實體節點，其resourceType為 *wcm/foundation/components/image*。

>[!NOTE]
>
>若要進一步瞭解如何使用這些範本從儀表板建立模型，請參閱「行動應 [用程式」的「製作」區段下的「建立模型](/help/mobile/administer-mobile-apps.md) 」。
