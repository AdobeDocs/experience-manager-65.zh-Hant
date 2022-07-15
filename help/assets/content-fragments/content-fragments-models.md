---
title: 內容片段模型
description: 瞭解內容片段模型如何作為您的無頭內容的基礎AEM，以及如何使用結構化內容建立內容片段。
feature: Content Fragments
role: User
exl-id: 6fd1fdb2-d1d3-4f97-b119-ecfddcccec9e
source-git-commit: 9b3e30f7523ff86fd1ed1b5fc55ce22b8e9f3429
workflow-type: tm+mt
source-wordcount: '2338'
ht-degree: 6%

---

# 內容片段模型 {#content-fragment-models}

定義內容AEM結構中的內容片段模型 [內容片段，](/help/assets/content-fragments/content-fragments.md) 作為無頭內容的基礎。

要使用內容片段模型，請執行以下操作：

1. [為實例啟用內容片段模型功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [建立](#creating-a-content-fragment-model), [配置](#defining-your-content-fragment-model)，內容片段模型
1. [啟用內容片段模型](#enabling-disabling-a-content-fragment-model) 在建立內容片段時使用，以在建立內容片段時使用
1. [允許在所需資產資料夾上使用內容片段模型](#allowing-content-fragment-models-assets-folder) 通過配置 **策略**。

## 建立內容片段模型 {#creating-a-content-fragment-model}

1. 導航到 **工具**。 **資產**，然後開啟 **內容片段模型**。
1. 導航到適合您的資料夾 [配置](/help/assets/content-fragments/content-fragments-configuration-browser.md)。
1. 使用 **建立** 的子菜單。

   >[!CAUTION]
   >
   >如果 [未啟用內容片段模型的使用](/help/assets/content-fragments/content-fragments-configuration-browser.md)，也請參見Wiki頁。 **建立** 選項。

1. 指定「模 **型標題」**。也可以添加 **標籤**&#x200B;的 **說明**，然後選擇 **啟用模型** 至 [啟用模型](#enabling-disabling-a-content-fragment-model) 的子菜單。

   ![標題和說明](assets/cfm-models-02.png)

1. 使用 **建立** 的子菜單。 消息將指示操作成功，您可以選擇 **開啟** 以立即編輯模型，或 **完成** 返回控制台。

## 定義內容片段模型 {#defining-your-content-fragment-model}

所述內容片段模型使用選擇有效地定義所得內容片段的結構 **[資料類型](#data-types)**。 使用模型編輯器，可以添加資料類型的實例，然後配置它們以建立必填欄位：

>[!CAUTION]
>
>編輯現有內容片段模型可能會影響相關片段。

1. 導航到 **工具**。 **資產**，然後開啟 **內容片段模型**。

1. 導航到保存內容片段模型的資料夾。

1. 開啟所需的模型 **編輯**;使用快速操作，或從工具欄中選擇模型，然後選擇操作。

   開啟模型編輯器後，將顯示：

   * 左：已定義
   * 右：資 **料類型** ，可用於建立欄位( **和屬性** ，以供建立欄位後使用)

   >[!NOTE]
   >
   >當欄位為 **必需**，也請參見Wiki頁。 **標籤** 在左窗格中指示，將標有標注符(**&#42;**)。

   ![屬性](assets/cfm-models-03.png)

1. **添加欄位**

   * 將所需資料類型拖到欄位的所需位置：

      ![資料類型到欄位](assets/cfm-models-04.png)

   * 將欄位添加到模型後，右面板將顯示 **屬性** 可為該特定資料類型定義的。 在此，您可以定義該欄位的必需內容。

      * 許多屬性不言自明，有關詳細資訊，請參閱 [屬性](#properties)。
      * 鍵入 **欄位標籤** 將自動完成 **屬性名稱**   — 如果為空，則可以隨後手動更新。

         >[!CAUTION]
         >
         >手動更新屬性時 **屬性名稱** 對於資料類型，請注意，名稱必須僅包含A-Z、a-z、0-9和下划線「_」作為特殊字元。
         >
         >如果在早期版本中建立的模AEM型包含非法字元，請刪除或更新這些字元。
      例如：

      ![欄位屬性](assets/cfm-models-05.png)


1. **刪除欄位**

   選擇必填欄位，然後按一下/點擊垃圾桶表徵圖。 系統將要求您確認操作。

   ![刪除](assets/cfm-models-06.png)

1. 根據需要添加所有必需欄位並定義相關屬性。 例如：

   ![保存](assets/cfm-models-07.png)

1. 選擇 **保存** 來堅持定義。

## 資料類型 {#data-types}

選擇資料類型可用於定義模型：

* **單行文字**
   * 添加一行文本的一個或多個欄位；可以定義最大長度
* **多行文字**
   * 可以是富格文本、純文字檔案或標籤的文本區域
* **數量**
   * 添加一個或多個數字欄位
* **布林值**
   * 添加布爾複選框
* **日期時間**
   * 添加日期和/或時間
* **列舉**
   * 添加一組複選框、單選按鈕或下拉欄位
* **標記**
   * 允許片段作者訪問和選擇標籤區域
* **內容參考資料**
   * 參考任何類型的其他內容；可以用來 [建立嵌套內容](#using-references-to-form-nested-content)
   * 如果引用了影像，則可以選擇顯示縮略圖
* **片段引用**
   * 引用其他內容片段；可以用來 [建立嵌套內容](#using-references-to-form-nested-content)
   * 可以將資料類型配置為允許片段作者：
      * 直接編輯引用的片段。
      * 根據適當的模型建立新內容片段
* **JSON 物件**
   * 允許內容片段作者將JSON語法輸入到片段的相應元素中。
      * 允許存AEM儲從其他服務複製/貼上的直接JSON。
      * JSON將傳遞，並在GraphQL中輸出為JSON。
      * 在內容片段編輯器中包括JSON語法突出顯示、自動完成和錯誤突出顯示。
* **標籤預留位置**
   * 允許在編輯內容片段內容時使用頁籤。
這將在模型編輯器中顯示為分隔符，分隔內容資料類型清單的各節。 每個實例表示新頁籤的開始。
在片段編輯器中，每個實例將顯示為一個頁籤。

      >[!NOTE]
      >
      >此資料類型純粹用於格式設定，GraphQL架AEM構忽略它。

## 屬性 {#properties}

許多屬性不言自明，對於某些屬性，其他詳細資訊如下：


* **屬性名稱**

   手動更新資料類型的此屬性時，請注意名稱 **必須** 含 *僅* A-Z、a-z、0-9和下划線「_」作為特殊字元。

   >[!CAUTION]
   >
   >如果在早期版本中建立的模AEM型包含非法字元，請刪除或更新這些字元。

* **呈現為**
用於在片段中實現/呈現該欄位的各種選項。 這通常允許您定義作者是將看到該欄位的單個實例，還是允許建立多個實例。

* **欄位標籤**
輸入 
**欄位標籤** 將自動生成 **屬性名稱**，如果需要，可手動更新。

* **驗證**
基本驗證可由以下機制提供： **必需** 屬性。 某些資料類型具有附加驗證欄位。 請參閱 [驗證](#validation) 的上界。

* 對於「多行」 **資料類型** ，可將「預設類型 **** 」定義為：

   * **RTF**
   * **Markdown**
   * **純文字**

   如果未指定，則預設值 **富文本** 欄位。

   在內容 **片段模型中變更「預設類型** 」，只會在編輯器中開啟並儲存該片段後，對現有、相關的內容片段生效。

* **唯一**
內容（對於特定欄位）必須在從當前模型建立的所有內容片段中是唯一的。

   這用於確保內容作者不能重複已添加到同一模型另一個片段中的內容。

   例如， **單行文本** 欄位 `Country` 內容片段模型中不能具有 `Japan` 的子目錄。 當嘗試第二個實例時將發出警告。

   >[!NOTE]
   >
   >確保每個語言根的唯一性。

   >[!NOTE]
   >
   >變體可以具有相同 *獨特* 值作為同一片段的變體，但與用於其它片段的任何變體的值不相同。

* 請參閱 **[內容引用](#content-reference)** 的子菜單。

* 請參閱 **[片段引用（嵌套片段）](#fragment-reference-nested-fragments)** 的子菜單。

<!--
* **Translatable**
  Checking the **Translatable** checkbox on a field in the Content Fragment Model editor will:

  * Ensure the field's property name is added to the translation configuration, context `/content/dam/<sites-configuration>`, if not already present. 
  * For GraphQL: set a `<translatable>` property on the Content Fragment field to `yes`, to allow GraphQL query filter for JSON output with only translatable content.
-->

## 驗證 {#validation}

各種資料類型現在都包括定義在結果片段中輸入內容的驗證要求的可能性：

* **單行文字**
   * 與預定義規則運算式進行比較。
* **數量**
   * 檢查特定值。
* **內容參考資料**
   * Test特定類型的內容。
   * 只能引用指定檔案大小或更小的資產。
   * 只能引用預定義寬度和/或高度範圍內（以像素為單位）的影像。
* **片段引用**
   * Test特定內容片段模型。

## 使用引用形成嵌套內容 {#using-references-to-form-nested-content}

內容片段可以使用下列資料類型之一形成嵌套內容：

* **[內容參考資料](#content-reference)**
   * 提供對其他內容的簡單引用；任何類型。
   * 可以為一個或多個參照（在生成的片段中）配置。

* **[片段引用](#fragment-reference-nested-fragments)** （嵌套片段）
   * 參照其它片段，取決於指定的特定模型。
   * 允許您包括/檢索結構化資料。

      >[!NOTE]
      >
      >該方法與 [使用GraphQL的內容片段進行無頭內容傳遞](/help/assets/content-fragments/content-fragments-graphql.md)。
   * 可以為一個或多個引用（在生成的片段中）配置。

>[!NOTE]
>
>具AEM有以下項的重複保護：
>
>* 內容參考資料
   >  這防止用戶添加對當前片段的引用。 這可能導致「片段引用選取器」對話框為空。
>
>* GraphQL中的片段引用
   >  如果建立一個深度查詢，該查詢返回彼此引用的多個內容片段，則它將在第一次出現時返回null。


### 內容參考資料 {#content-reference}

「內容引用」允許您從另一個源中呈現內容；例如，影像或內容片段。

除了標準屬性外，您還可以指定：

* 的 **根路徑** 用於任何引用內容
* 可引用的內容類型
* 檔案大小限制
* 如果引用了影像：
   * 顯示縮圖
   * 高度和寬度的影像約束

![內容參考資料](assets/cfm-content-reference.png)

### 片段引用（嵌套片段） {#fragment-reference-nested-fragments}

片段引用引用一個或多個內容片段。 在檢索內容以供您的應用程式使用時，此功能特別受關注，因為它允許您檢索具有多層的結構化資料。

例如：

* 定義員工詳細資訊的模型；這些包括：
   * 對定義雇主（公司）的模型的引用

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
>
>這與 [使用GraphQL的內容片段進行無頭內容傳遞](/help/assets/content-fragments/content-fragments-graphql.md)。

除了標準屬性外，您還可以定義：

* **呈現為**:

   * **多場**  — 片段作者可以建立多個、單個、引用

   * **碎片**  — 允許片段作者選擇對片段的單個引用

* **模型類型**
可以選擇多個模型。 創作內容片段時，必須使用這些模型建立任何引用的片段。

* **根路徑**
這為引用的任何片段指定根路徑。

* **允許建立片段**

   這將允許片段作者基於相應的模型建立新片段。

   * **碎片組合**  — 允許片段作者通過選擇多個片段來構建複合

   ![片段引用](assets/cfm-fragment-reference.png)

>[!NOTE]
>
>已建立重複保護機制。 它禁止用戶在片段引用中選擇當前內容片段。 這可能導致「片段引用選取器」對話框為空。
>
>GraphQL中還對片段引用提供重複保護。 如果跨兩個相互引用的內容片段建立深度查詢，則它將返回空值。

## 啟用或禁用內容片段模型 {#enabling-disabling-a-content-fragment-model}

要完全控制內容片段模型的使用，您可以設定這些模型的狀態。

### 啟用內容片段模型 {#enabling-a-content-fragment-model}

建立模型後，需要啟用它，以便：

* 在建立新內容片段時可供選擇。
* 可以從內容片段模型中引用。
* 可用於GraphQL;因此生成模式。

要啟用標籤為以下任一模型：

* **草稿** :mew（從未啟用）。
* **已禁用** :已特別禁用。

使用 **啟用** 選項：

* 選取所需的「模型」(Model)時，頂部工具欄。
* 相應的「快速操作」(Quick Action)（滑鼠懸停於所需的模型上）。

![啟用繪製或禁用模型](assets/cfm-status-enable.png)

### 禁用內容片段模型 {#disabling-a-content-fragment-model}

還可以禁用模型，以便：

* 模型不再可用作建立 *新* 內容片段。
* 但是：
   * GraphQL架構仍在生成中且仍可查詢（以避免影響JSON API）。
   * 仍然可以查詢基於模型的任何內容片段並從GraphQL終結點返回。
* 模型不能再被引用，但現有的引用保持不變，仍可查詢並從GraphQL端點返回。

禁用標籤為 **已啟用** 使用 **禁用** 選項：

* 選取所需的「模型」(Model)時，頂部工具欄。
* 相應的「快速操作」(Quick Action)（滑鼠懸停於所需的模型上）。

![禁用已啟用的模型](assets/cfm-status-disable.png)

## 允許在資產資料夾上建立內容片段模型 {#allowing-content-fragment-models-assets-folder}

要實施內容治理，您可以配置 **策略** 在「資產」資料夾上，以控制允許在該資料夾中建立片段的內容片段模型。

>[!NOTE]
>
>該機制類似於 [允許頁面模板](/help/sites-authoring/templates.md#allowing-a-template-author) 的子級。

配置 **策略** 為 **允許的內容片段模型**:

1. 導航並開啟 **屬性** 的子菜單。

1. 開啟 **策略** 頁籤，您可以在其中配置：

   * **繼承自`<folder>`**

      建立新子資料夾時，策略會自動繼承；如果子資料夾需要允許不同於父資料夾的模型，則可以重新配置策略（並斷開繼承）。

   * **允許的內容片段模型 (依路徑)**

      允許使用多個模型。

   * **允許的內容片段模型（按標籤）**

      允許使用多個模型。
   ![內容片段模型策略](assets/cfm-model-policy-assets-folder.png)

1. **保存** 任何更改。

資料夾允許的內容片段模型解析如下：
* 的 **策略** 為 **允許的內容片段模型**。
* 如果為空，則嘗試使用繼承規則確定策略。
* 如果繼承鏈未傳遞結果，請查看 **Cloud Services** 該資料夾的配置（也先直接配置，然後通過繼承）。
* 如果以上所有項都未提供任何結果，則該資料夾不允許使用任何模型。

## 刪除內容片段模型 {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>刪除內容片段模型可能會影響相關片段。

要刪除內容片段模型：

1. 導航到 **工具**。 **資產**，然後開啟 **內容片段模型**。

1. 導航到保存內容片段模型的資料夾。
1. 選擇模型，然後 **刪除** 的子菜單。

   >[!NOTE]
   >
   >如果參照了模型，則會給出警告。 採取適當行動。

## 發佈內容片段模型 {#publishing-a-content-fragment-model}

在發佈任何相關內容片段時/之前，需要發佈內容片段模型。

要發佈內容片段模型，請執行以下操作：

1. 導航到 **工具**。 **資產**，然後開啟 **內容片段模型**。

1. 導航到保存內容片段模型的資料夾。
1. 選擇模型，然後 **發佈** 的子菜單。
發佈狀態將在控制台中指示。

   >[!NOTE]
   >
   >如果發佈模型尚未發佈的內容片段，則選擇清單將指示此情況，並且模型將隨片段一起發佈。

## 取消發佈內容片段模型 {#unpublishing-a-content-fragment-model}

如果內容片段模型未被任何片段引用，則可以取消發佈這些模型。

取消發佈內容片段模型：

1. 導航到 **工具**。 **資產**，然後開啟 **內容片段模型**。

1. 導航到保存內容片段模型的資料夾。
1. 選擇模型，然後 **取消發佈** 的子菜單。
發佈狀態將在控制台中指示。

## 內容片段模型 — 屬性 {#content-fragment-model-properties}

可以編輯 **屬性** 內容片段模型：

* **基本**
   * **模型標題**
   * **標記**
   * **說明**
   * **上傳影像**
