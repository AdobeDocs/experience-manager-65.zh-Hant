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
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 1%

---


# 儲存庫{#models-in-repository}中的模型

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

模型包含一組資料類型，定義內容服務最終將呈現的屬性。 模型也定義了其他模型之間的關係，以強化資料完整性。

身為開發人員，您應熟悉存放庫中的模型結構。 您可以根據應用程式需求建立自己的模型和實體。

## 建立模型類型{#creating-model-types}

在&#x200B;*/libs/settings/mobileapps/model-types*&#x200B;下有兩種系統提供的型號。 如果要覆蓋系統模型類型，則需要在您希望覆蓋發生的配置節點下建立&#x200B;*mobileapps/model-types*&#x200B;節點。

例如，如果您已在&#x200B;*/conf/myconf1*&#x200B;和&#x200B;*/conf/myconf2*&#x200B;建立配置，並且只想在&#x200B;*conf1*&#x200B;上覆蓋系統模型類型，則應在&#x200B;*conf1*&#x200B;的設定下建立&#x200B;*mobileapps/model-types*&#x200B;節點。

若要允許將資料類型新增至模型，模型類型必須有名為「scq:Page」類型的「swarge」子節點，以及&#x200B;*wcm/swarge/components/swarge*&#x200B;的資源類型。

架構頁面也必須在PageContent節點上包含&#x200B;*dataTypesConfig*&#x200B;屬性，指出從此類型建立的資料類型模型將允許使用。

>[!NOTE]
>
>**Stware**&#x200B;是定義實體可根據模型編輯的資料類型的頁面。 也可以設定每個資料類型，以定義UI中欄位的呈現方式，以及資料值的保存方式。

### 資料類型配置{#data-types-config}

資料類型配置節點包含資料類型項的清單。 每個資料類型項目都指定資料類型在模型編輯器中的顯示方式，以及資料類型在實體最終呈現時需要如何持續保存。

| **屬性名稱** | **說明** |
|---|---|
| fieldIcon | 代表資料類型的CoralUI圖示類別 |
| fieldPropResourceType | 會輸出所有屬性以設定資料類型的元件 |
| fieldProperties | 欄位PropResourceType為&#x200B;*mobileapps/caas/gui/components/models/editor/datatypes/field*&#x200B;時使用的屬性元件的多值清單 |
| fieldResourceType | resource資料類型的持續節點類型（即將在實體編輯器中呈現屬性的元件） |
| fieldViewResourceType | 用於在模型編輯器視圖中呈現資料類型的元件（如果省略此屬性，將使用fieldResourceType） |
| fieldTitle | 將在模型編輯器中顯示的資料類型的名稱 |
| multiFieldResourceType | 選取多值時要在持續節點上使用的資源類型 |
| renderType | 用戶端轉譯提示 |

### 資料類型設定覆蓋{#data-types-config-overlay}

&#39;dataTypesConfig&#39;屬性支援Sling資源合併。 這表示系統模型類型（甚至自訂模型類型）所使用的資料類型，可透過使用覆蓋節點加以自訂。

需要建立&#x200B;*/libs/settings/mobileapps/models/formbuilderconfig/datatypes*&#x200B;的覆蓋，然後視需要自訂。

例如，可以新增字串資料類型的覆蓋圖，以將fieldResourceType變更為自訂元件。

如需Sling資源合併的詳細資訊，請參閱[在AEM](/help/sites-developing/sling-resource-merger.md)中使用Sling資源合併。

![chlimage_1-7](assets/chlimage_1-7.png)

### 資料類型 {#data-types}

模型資料類型是表單元件，可在發佈表單時包含要包含的資料。 資料類型元件可視需要而複雜。 自訂資料類型的範例可能是特定國家/地區的位址區塊，以避免每次都使用原始資料類型重新建立。

如需自訂資料類型的範例，請參閱「/libs/mobileapps/caas/components/form/contentreference」。

所有原始資料類型都利用現有的Granite表單元件。 請參閱：[https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

然後，任何自訂資料類型都可新增至資料類型設定，以供模型編輯器使用。

## 建立模型{#creating-models}

開發完所有所需的模型類型和資料類型後，就可以開始建立模型。 最終，作者將使用模型來建立實體，內容服務將透過這些實體來轉譯其資料。

建立模型包括根據當前配置選擇允許的模型類型，然後提供標題和說明。

若要了解如何從控制面板建立和管理模型，請參閱「行動應用程式」編寫區段下的[建立模型](/help/mobile/administer-mobile-apps.md)。

### 模型{#properties-of-a-model}的屬性

下表顯示為模型定義的屬性：

| **屬性名稱** | **說明** |
|---|---|
| 模型標題 | 模型名稱 |
| 說明 | 模型說明 |
| 縮圖 | 模型的縮圖影像 |
| 模型類型 | 模型類型（可以是簡單字串或實際元件的路徑） |
| 允許的子項 | 允許作為此模板子項的模板的路徑 |
| 允許的父項 | 允許作為此模板父項的模板的路徑 |

>[!NOTE]
>
>*允許的子項*&#x200B;和&#x200B;*允許的父項*&#x200B;屬性遵循與頁面模板相同的規則。 如需詳細資訊，請參閱[頁面範本](/help/sites-developing/page-templates-static.md)。
>
>參考&#x200B;*模型類型*&#x200B;屬性時，所有模型都必須具有超類型&#x200B;*mobileapps/caas/components/data/entity*，但可以具有允許自訂內容傳送的子類型。 確保所有模型類型都是唯一的，也可能有助於內容服務的客戶區分資料中的對象。

### 編輯模型{#editing-a-model}

編輯模型時，需要開啟與模型相關聯的架構對話方塊表單以進行編輯。 通常架構是模型的子節點，但如有需要，可使用&#39;cq:swarker&#39;屬性指定其路徑，以將其置於模型之外。 如果您想要在需要不同屬性的多個模型之間共用相同的架構，這個方法很實用。

找到模型的支架時，模型編輯器會轉譯「jcr:content/cq:dialog/content」下的任何內容。 用戶端表單產生器引擎目前僅支援最多3欄的固定版面。 呈現的表單對話方塊的右側會是資料類型設定中指定的所有資料類型的清單。 按一下資料類型即可加以編輯。 接著，右側邊欄會切換至所選資料類型的屬性索引標籤。 將新資料類型拖曳至預覽畫布即可新增。 按一下「保存」(Save)可將更改傳播到伺服器。 按一下「取消」(Cancel)可關閉模型編輯器。

>[!NOTE]
>
>所有模型都是範本，因此會遵循所有AEM範本規則。 這允許使用屬性，如&#x200B;*allowedParents*&#x200B;和&#x200B;*allowedChildrens*&#x200B;屬性。 在根據模型建立新圖元時，這些參數是有效的。 範本規則將確保實體只能根據某些模型（取決於其階層）。
>
>若要了解如何從控制面板編輯模型，請參閱「行動應用程式」編寫區段下的[建立模型](/help/mobile/administer-mobile-apps.md)。

### 系統型號{#system-models}

提供了兩種預定義的系統模型，以便簡單地重複使用內容。 無法編輯這些模型。

**頁** 面模型頁面模型提供快速方法，可重新使用Sites中的現有內容，以供內容服務傳送。

基於頁面模型的圖元的resourceType為：mobileapps/caas/components/data/pages

路徑：Sites頁面的路徑。 此路徑中的內容（及其子項）將由內容服務處理程式呈現。

**資產** 模型資產模型提供快速方法，可重複使用資產中的現有內容，以便依內容服務傳送。

基於頁面模型的圖元的resourceType為：*mobileapps/caas/components/data/assets*

資產清單：從Assets建立的路徑清單。 每個資產都會新增為子實體節點，其resourceType為&#x200B;*wcm/foundation/components/image*。

>[!NOTE]
>
>若要進一步了解如何使用這些範本從控制面板建立模型，請參閱行動應用程式編寫區段下的[建立模型](/help/mobile/administer-mobile-apps.md) 。
