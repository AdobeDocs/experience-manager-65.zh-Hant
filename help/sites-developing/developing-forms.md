---
title: 開發Forms（傳統UI）
seo-title: Developing Forms (Classic UI)
description: 了解如何開發表單
seo-description: Learn how to develop forms
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: 4df14f837569997c3e4da8161ac2b099c39d89a6
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 0%

---

# 開發Forms（傳統UI）{#developing-forms-classic-ui}

表單的基本結構是：

* 表單開始
* 表單元素
* 表單端

所有這些都是以一系列預設值來實現的 [表單元件](/help/sites-authoring/default-components.md#form)，可在標準AEM安裝中使用。

除 [開發新元件](/help/sites-developing/developing-components-samples.md) 若要用於表單，您也可以：

* [使用值預先載入表單](#preloading-form-values)
* [使用多個值預載入（某些）欄位](#preloading-form-fields-with-multiple-values)
* [開發新動作](#developing-your-own-form-actions)
* [開發新的限制](#developing-your-own-form-constraints)
* [顯示或隱藏特定表單欄位](#showing-and-hiding-form-components)

[使用指令碼](#developing-scripts-for-use-with-forms) 視需要擴充功能。

>[!NOTE]
>
>本檔案著重於使用 [基礎元件](/help/sites-authoring/default-components-foundation.md) 在傳統UI中。 Adobe建議使用 [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 和 [隱藏條件](/help/sites-developing/hide-conditions.md) ，以在觸控式UI中開發表單。

## 預先載入表單值 {#preloading-form-values}

表單開始元件提供 **載入路徑**，此選用路徑指向儲存庫中的節點。

「載入路徑」是節點屬性的路徑，用於將預定義值載入到表單上的多個欄位中。

這是一個可選欄位，它指定儲存庫中節點的路徑。 如果此節點的屬性與欄位名稱匹配，則表單上的相應欄位將預載這些屬性的值。 如果不存在匹配項，則欄位包含預設值。

>[!NOTE]
>
>A [表單動作](#developing-your-own-form-actions) 也可以設定從中載入初始值的資源。 這是使用 `FormsHelper#setFormLoadResource` in `init.jsp`.
>
>只有在未設定時，作者才會從開始表單元件中設定的路徑填入表單。

### 預先載入多個值的表單欄位 {#preloading-form-fields-with-multiple-values}

各種表單欄位也提供 **項目載入路徑**，也是指向存放庫中節點的選用路徑。

此 **項目載入路徑** 是節點屬性的路徑，用於將預先定義的值載入到表單上的特定欄位，例如 [下拉清單](/help/sites-authoring/default-components-foundation.md#dropdown-list), [複選框組](/help/sites-authoring/default-components-foundation.md#checkbox-group) 或 [無線電組](/help/sites-authoring/default-components-foundation.md#radio-group).

#### 範例 — 預先載入包含多個值的下拉式清單 {#example-preloading-a-dropdown-list-with-multiple-values}

下拉式清單可以設定您要選取的值範圍。

此 **項目載入路徑** 可用來從存放庫的資料夾存取清單，並將這些項目預先載入欄位中：

1. 建立新的Sling資料夾( `sling:Folder`)，例如 `/etc/designs/<myDesign>/formlistvalues`

1. 新增屬性(例如 `myList`)，類型為多值字串( `String[]`)以包含下拉式項目清單。 也可以使用指令碼導入內容，例如使用JSP指令碼或shell指令碼中的cURL。

1. 在 **項目載入路徑** 欄位：例如， `/etc/designs/geometrixx/formlistvalues/myList`

請注意，若 `String[]` 格式如下：

* `AL=Alabama`
* `AK=Alaska`
* 等。

然後AEM會產生清單，如下所示：

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

例如，在多語言設定中，可以很好地使用此功能。

### 開發您自己的表單動作 {#developing-your-own-form-actions}

表單需要動作。 動作會定義當表單隨使用者資料提交時所執行的操作。

標準AEM安裝提供了一系列動作，您可在下方查看：

`/libs/foundation/components/form/actions`

和 **動作類型** 清單 **表單** 元件：

![chlimage_1-8](assets/chlimage_1-8.png)

本節說明如何開發您自己的表單動作，以納入此清單。

您可以在 `/apps` 如下所示：

1. 建立類型的節點 `sling:Folder`. 指定反映要實作之動作的名稱。

   例如：

   `/apps/myProject/components/customFormAction`

1. 在此節點上定義以下屬性，然後按一下 **全部儲存** 保留變更：

   * `sling:resourceType`  — 設定為 `foundation/components/form/action`

   * `componentGroup`  — 定義為 `.hidden`

   * （可選）:

      * `jcr:title`  — 指定您選擇的標題，此標題將顯示在下拉式選取清單中。 如果未設定，則顯示節點名稱

      * `jcr:description`  — 輸入您選擇的說明

1. 在資料夾中建立對話方塊節點：

   1. 新增欄位，讓作者在選擇動作後即可編輯表單對話方塊。

1. 在資料夾中建立以下任一項：

   1. 貼文指令碼。
指令碼的名稱為 `post.POST.<extension>`，例如 `post.POST.jsp`
提交表單以處理表單時，會叫用貼文指令碼，其中包含處理從表單送達之資料的程式碼 
`POST`。

   1. 添加在提交表單時調用的轉發指令碼。
指令碼的名稱為 `forward.<extension`>，例如 `forward.jsp`
此指令碼可定義路徑。 然後，將當前請求轉發到指定路徑。
   必要的呼叫是 `FormsHelper#setForwardPath` （2種變體）。 典型的案例是執行一些驗證或邏輯，以尋找目標路徑，然後轉送至該路徑，讓預設的SlingPOSTservlet執行JCR中的實際儲存。

   也可能會有其他servlet來執行實際處理，在這種情況下，表單動作和 `forward.jsp` 只能充當「膠水」密碼。 以下是的郵件動作範例： `/libs/foundation/components/form/actions/mail`，將詳細資訊轉發給 `<currentpath>.mail.html`郵件servlet的位置。

   因此：

   * a `post.POST.jsp` 對於由行動本身完全完成的小操作非常有用
   * 而 `forward.jsp` 僅需委派時即可使用。

   指令碼的執行順序為：

   * 轉譯表單時( `GET`):

      1. `init.jsp`
      1. 針對所有欄位的限制： `clientvalidation.jsp`
      1. 表單的validationRT: `clientvalidation.jsp`
      1. 如果已設定，則透過載入資源載入表單
      1. `addfields.jsp` 在內呈現 `<form></form>`
   * 處理表格時 `POST`:

      1. `init.jsp`
      1. 針對所有欄位的限制： `servervalidation.jsp`
      1. 表單的validationRT: `servervalidation.jsp`
      1. `forward.jsp`
      1. 如果已設定前進路徑( `FormsHelper.setForwardPath`)，轉送要求，然後呼叫 `cleanup.jsp`

      1. 如果未設定前進路徑，則呼叫 `post.POST.jsp` (此處結束，否 `cleanup.jsp` 呼叫)




1. 在資料夾中再次選擇新增：

   1. 用於添加欄位的指令碼。
指令碼的名稱為 `addfields.<extension>`，例如 `addfields.jsp`
安 
`addfields` 在寫入表單開始的HTML後，立即調用指令碼。 這可讓動作在表單內新增自訂輸入欄位或其他這類HTML。

   1. 初始化指令碼。
指令碼的名稱為 `init.<extension>`，例如 `init.jsp`
表單呈現時會叫用此指令碼。 它可用來初始化動作細節。

   1. 清除指令碼。
指令碼的名稱為 `cleanup.<extension>`，例如 `cleanup.jsp`
此指令碼可用於執行清除。

1. 使用 **Forms** parsys中的元件。 此 **動作類型** 下拉式清單現在會包含您的新動作。

   >[!NOTE]
   >
   >若要查看屬於產品一部分的預設動作：
   >
   >
   >`/libs/foundation/components/form/actions`

### 開發您自己的表單限制 {#developing-your-own-form-constraints}

可在兩個層面施加限制：

* 針對 [個別欄位（請參閱下列程式）](#constraints-for-individual-fields)
* As [表單全域驗證](#form-global-constraints)

#### 個別欄位的限制 {#constraints-for-individual-fields}

您可以為個別欄位新增自己的限制(在 `/apps`)，如下所示：

1. 建立類型的節點 `sling:Folder`. 指定反映要實施的約束的名稱。

   例如：

   `/apps/myProject/components/customFormConstraint`

1. 在此節點上定義以下屬性，然後按一下 **全部儲存** 保留變更：

   * `sling:resourceType`  — 設為 `foundation/components/form/constraint`

   * `constraintMessage`  — 根據限制，在提交表單時，如果欄位無效，則會顯示自訂訊息

   * （可選）:

      * `jcr:title`  — 指定您選擇的標題，此標題將顯示在選擇清單中。 如果未設定，則顯示節點名稱
      * `hint`  — 使用者如何使用欄位的其他資訊

1. 在此資料夾內，您可以需要下列指令碼：

   * 客戶端驗證指令碼：指令碼的名稱為 `clientvalidation.<extension>`，例如 `clientvalidation.jsp`
表單欄位呈現時會叫用此名稱。 它可用來建立用戶端javascript，以驗證用戶端上的欄位。

   * 伺服器驗證指令碼：指令碼的名稱為 `servervalidation.<extension>`，例如 `servervalidation.jsp`
提交表單時會叫用此名稱。 它可用來在提交後驗證伺服器上的欄位。

>[!NOTE]
>
>範例限制可在下方顯示：
>
>`/libs/foundation/components/form/constraints`

#### 表單全域限制 {#form-global-constraints}

通過在啟動表單元件( `validationRT`)。 例如：

`apps/myProject/components/form/validation`

然後您可以定義：

* a `clientvalidation.jsp`  — 在欄位的用戶端驗證指令碼之後插入
* 和 `servervalidation.jsp`  — 在對 `POST`.

### 顯示和隱藏表單元件 {#showing-and-hiding-form-components}

您可以設定表單，以根據表單中其他欄位的值顯示或隱藏表單元件。

只有在特定條件下才需要欄位時，變更表單欄位的可見性會很實用。 例如，在意見表單中，有問題詢問客戶是否希望在電子郵件中將產品資訊傳送給他們。 選取「是」時，會出現文字欄位，讓客戶輸入其電子郵件地址。

使用 **編輯顯示/隱藏規則** 對話框，指定在其中顯示或隱藏表單元件的條件。

![showhideeditor](assets/showhideeditor.png)

使用對話方塊頂端的欄位來指定下列資訊：

* 是否指定用於隱藏或顯示元件的條件。
* 要顯示或隱藏元件，任何或所有條件都必須為true。

這些欄位下方會顯示一或多個條件。 條件會比較其他表單元件（在相同表單上）的值與值。 如果欄位中的實際值滿足條件，則條件會評估為true。 條件包括下列資訊：

* 測試的表單欄位標題。
* 運算子。
* 會比較值與欄位值。

例如，標題為的「選項群組」元件 `Receive email notifications?`*包含 `Yes` 和 `No` 選項按鈕。 標題為 `Email Address` 會使用下列條件，以便在 `Yes` 已選取：

![showhidecondition](assets/showhidecondition.png)

在Javascript中，條件會使用「元素名稱」屬性的值來參考欄位。 在上一個示例中，單選按鈕組元件的「元素名稱」屬性為 `contact`. 下列程式碼就該範例而言是相等的Javascript程式碼：

`((contact == "Yes"))`

**要顯示或隱藏表單元件，請執行以下操作：**

1. 編輯特定表單元件。

1. 選擇 **顯示/隱藏** 開啟 **編輯顯示/隱藏規則** 對話框：

   * 在第一個下拉式清單中，選取 **顯示** 或 **隱藏** 指定條件是否決定要顯示或隱藏元件。

   * 在頂端行結尾的下拉式清單中選取：

      * **all**  — 如果所有條件都必須為true，才能顯示或隱藏元件
      * **any**  — 如果只有一或多個條件必須為true，則顯示或隱藏元件
   * 在條件行中（預設顯示一個），選取元件、運算子，然後指定值。
   * 視需要按一下，以新增更多條件 **新增條件**.

   例如：

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. 按一下 **確定** 以儲存定義。

1. 儲存定義後， **編輯規則** 連結會出現在 **顯示/隱藏** 選項（在表單元件屬性中）。 按一下此連結以開啟 **編輯顯示/隱藏規則** 對話框進行更改。

   按一下 **確定** 以儲存所有變更。

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >可查看和測試「顯示/隱藏」定義的效果：
   >
   >* in **預覽** 模式（首次切換為預覽時需要頁面重新載入）
   >
   >* 在發佈環境中


#### 處理中斷的元件參考 {#handling-broken-component-references}

顯示/隱藏條件使用「元素名稱」屬性的值來參照表單中的其他元件。 當任何條件都參考已刪除或已變更元素名稱屬性的元件時，顯示/隱藏設定無效。 發生此情況時，您必須手動更新條件，或表單載入時發生錯誤。

當「顯示/隱藏」設定無效時，只會以JavaScript程式碼的形式提供設定。 編輯代碼以更正問題。該代碼使用原本用於引用元件的Element Name屬性。

### 開發與Forms搭配使用的指令碼 {#developing-scripts-for-use-with-forms}

如需撰寫指令碼時可使用的API元素詳細資訊，請參閱 [與表單相關的javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

您可以將此功能用於下列動作，例如在提交表單前呼叫服務，以及在服務失敗時取消服務：

* 定義驗證資源類型
* 納入指令碼以進行驗證：

   * 在JSP中，調用Web服務並建立 `com.day.cq.wcm.foundation.forms.ValidationInfo` 包含錯誤訊息的物件。 如果發生錯誤，則不會張貼表單資料。
