---
title: 開發Forms（經典UI）
seo-title: Developing Forms (Classic UI)
description: 瞭解如何開發表單
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

# 開發Forms（經典UI）{#developing-forms-classic-ui}

形式的基本結構是：

* 窗體開始
* 窗體元素
* 表單結束

所有這些都是通過一系列預設 [窗體元件](/help/sites-authoring/default-components.md#form)，在標準安裝中AEM提供。

除 [開發新元件](/help/sites-developing/developing-components-samples.md) 在表單上使用，您還可以：

* [使用值預載入窗體](#preloading-form-values)
* [具有多個值的預載入（某些）欄位](#preloading-form-fields-with-multiple-values)
* [制定新操作](#developing-your-own-form-actions)
* [制定新約束](#developing-your-own-form-constraints)
* [顯示或隱藏特定表單域](#showing-and-hiding-form-components)

[使用指令碼](#developing-scripts-for-use-with-forms) 在必要時擴展功能。

>[!NOTE]
>
>本文檔重點介紹使用 [基礎元件](/help/sites-authoring/default-components-foundation.md) 的子菜單。 Adobe建議利用新 [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 和 [隱藏條件](/help/sites-developing/hide-conditions.md) 用於在啟用觸摸的UI中開發表單。

## 預載入窗體值 {#preloading-form-values}

表單啟動元件為 **載入路徑**，指向儲存庫中節點的可選路徑。

「載入路徑」是指向節點屬性的路徑，用於將預定義值載入到窗體上的多個欄位中。

這是一個可選欄位，它指定儲存庫中節點的路徑。 如果此節點具有與欄位名稱匹配的屬性，則表單上的相應欄位將預先載入這些屬性的值。 如果不存在匹配項，則欄位包含預設值。

>[!NOTE]
>
>A [表單操作](#developing-your-own-form-actions) 也可以設定從中載入初始值的資源。 這是使用 `FormsHelper#setFormLoadResource` 內 `init.jsp`。
>
>僅當未設定時，作者才會從起始表單元件中設定的路徑填充表單。

### 預載入具有多個值的表單域 {#preloading-form-fields-with-multiple-values}

各種表單域也 **項目載入路徑**，也是指向儲存庫中節點的可選路徑。

的 **項目載入路徑** 是節點屬性的路徑，用於將預定義值載入到窗體上的該特定欄位中，例如， [下拉清單](/help/sites-authoring/default-components-foundation.md#dropdown-list)。 [複選框組](/help/sites-authoring/default-components-foundation.md#checkbox-group) 或 [無線電組](/help/sites-authoring/default-components-foundation.md#radio-group)。

#### 示例 — 預載入具有多個值的下拉清單 {#example-preloading-a-dropdown-list-with-multiple-values}

可以使用選擇值範圍配置下拉清單。

的 **項目載入路徑** 可用於從儲存庫中的資料夾訪問清單，並將這些清單預載入到欄位中：

1. 建立新的吊帶資料夾( `sling:Folder`)例如， `/etc/designs/<myDesign>/formlistvalues`

1. 添加新屬性(例如， `myList`)類型多值字串( `String[]`)以包含下拉項的清單。 也可以使用指令碼導入內容，如使用JSP指令碼或shell指令碼中的cURL。

1. 使用 **項目載入路徑** 欄位：比如說， `/etc/designs/geometrixx/formlistvalues/myList`

請注意，如果 `String[]` 格式如下：

* `AL=Alabama`
* `AK=Alaska`
* 等。

然AEM後生成清單：

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

例如，可以在多語言設定中使用此功能。

### 開發您自己的表單操作 {#developing-your-own-form-actions}

表單需要操作。 操作定義當表單與用戶資料一起提交時執行的操作。

標準安裝提供了一系列操作AEM，這些操作可在以下位置查看：

`/libs/foundation/components/form/actions`

在 **操作類型** 清單 **窗體** 元件：

![chlimage_1-8](assets/chlimage_1-8.png)

本節介紹如何開發您自己的表單操作，以便包括在此清單中。

您可以在 `/apps` 如下：

1. 建立類型的節點 `sling:Folder`。 指定反映要實施的操作的名稱。

   例如：

   `/apps/myProject/components/customFormAction`

1. 在此節點上定義以下屬性，然後按一下 **全部保存** 要保留您的更改：

   * `sling:resourceType`  — 設定為 `foundation/components/form/action`

   * `componentGroup`  — 定義為 `.hidden`

   * （可選）:

      * `jcr:title`  — 指定您選擇的標題，該標題將顯示在下拉清單中。 如果未設定，則顯示節點名稱

      * `jcr:description`  — 輸入您選擇的說明

1. 在資料夾中建立對話節點：

   1. 添加欄位，以便在選擇操作後，作者可以編輯表單對話框。

1. 在資料夾中建立以下任一項：

   1. 帖子指令碼。
指令碼的名稱為 `post.POST.<extension>`，例如 `post.POST.jsp`
在提交表單以處理表單時調用後指令碼，它包含處理從表單到達的資料的代碼 
`POST`。

   1. 添加提交表單時調用的轉發指令碼。
指令碼的名稱為 `forward.<extension`>，例如 `forward.jsp`
此指令碼可以定義路徑。 然後，將當前請求轉發到指定路徑。
   必要的呼叫是 `FormsHelper#setForwardPath` (2)變型。 一個典型的案例是執行一些驗證或邏輯，以查找目標路徑，然後轉發到該路徑，讓預設的SlingPOSTservlet在JCR中執行實際儲存。

   還可能有另一個執行實際處理的servlet，在這種情況下，表單操作和 `forward.jsp` 只能充當&quot;膠&quot;代碼。 此操作的示例為： `/libs/foundation/components/form/actions/mail`，將詳細資訊轉發到 `<currentpath>.mail.html`郵件servlet所在的位置。

   所以：

   * a `post.POST.jsp` 對於由操作本身完全完成的小操作非常有用
   * 的 `forward.jsp` 僅在需要委派時有用。

   指令碼的執行順序為：

   * 在呈現窗體( `GET`):

      1. `init.jsp`
      1. 對於所有欄位的約束： `clientvalidation.jsp`
      1. 表單的validationRT: `clientvalidation.jsp`
      1. 如果已設定，則通過載入資源載入表單
      1. `addfields.jsp` 在內部渲染 `<form></form>`
   * 處理表格 `POST`:

      1. `init.jsp`
      1. 對於所有欄位的約束： `servervalidation.jsp`
      1. 表單的validationRT: `servervalidation.jsp`
      1. `forward.jsp`
      1. 如果設定了前進路徑( `FormsHelper.setForwardPath`)，轉發請求，然後呼叫 `cleanup.jsp`

      1. 如果未設定前進路徑，則調用 `post.POST.jsp` (結束於此，不 `cleanup.jsp` 調用)




1. 在資料夾中（可選）再次添加：

   1. 用於添加欄位的指令碼。
指令碼的名稱為 `addfields.<extension>`，例如 `addfields.jsp`
安 
`addfields` 在寫入表單啟動的HTML後立即調用指令碼。 這允許操作在表單中添加自定義輸入欄位或其他此類HTML。

   1. 初始化指令碼。
指令碼的名稱為 `init.<extension>`，例如 `init.jsp`
在呈現表單時調用此指令碼。 它可用於初始化操作細節。

   1. 清除指令碼。
指令碼的名稱為 `cleanup.<extension>`，例如 `cleanup.jsp`
此指令碼可用於執行清除。

1. 使用 **Forms** 零件中的元件。 的 **操作類型** 下拉框將包含您的新操作。

   >[!NOTE]
   >
   >要查看屬於產品的預設操作：
   >
   >
   >`/libs/foundation/components/form/actions`

### 開發您自己的表單約束 {#developing-your-own-form-constraints}

限制可分兩個層次：

* 對於 [單個欄位（請參閱以下過程）](#constraints-for-individual-fields)
* 作為 [表單全局驗證](#form-global-constraints)

#### 單個欄位的約束 {#constraints-for-individual-fields}

您可以為單個欄位添加您自己的約束(在 `/apps`)，如下所示：

1. 建立類型的節點 `sling:Folder`。 指定反映要實現的約束的名稱。

   例如：

   `/apps/myProject/components/customFormConstraint`

1. 在此節點上定義以下屬性，然後按一下 **全部保存** 要保留您的更改：

   * `sling:resourceType`  — 設定為 `foundation/components/form/constraint`

   * `constraintMessage`  — 根據約束條件，在提交表單時，如果欄位無效將顯示自定義消息

   * （可選）:

      * `jcr:title`  — 指定您選擇的標題，該標題將顯示在選擇清單中。 如果未設定，則顯示節點名稱
      * `hint`  — 有關如何使用欄位的其他資訊，請向用戶提供

1. 在此資料夾中，您需要以下指令碼：

   * 客戶端驗證指令碼：指令碼的名稱為 `clientvalidation.<extension>`，例如 `clientvalidation.jsp`
在呈現表單欄位時將調用此選項。 它可用於建立客戶端javascript以驗證客戶端上的欄位。

   * 伺服器驗證指令碼：指令碼的名稱為 `servervalidation.<extension>`，例如 `servervalidation.jsp`
在提交表單時將調用此選項。 它可用於在提交後驗證伺服器上的欄位。

>[!NOTE]
>
>示例約束可在以下位置查看：
>
>`/libs/foundation/components/form/constraints`

#### 窗體全局約束 {#form-global-constraints}

通過在啟動表單元件( `validationRT`)。 例如：

`apps/myProject/components/form/validation`

然後，您可以定義：

* a `clientvalidation.jsp`  — 在欄位的客戶端驗證指令碼後注入
* 和 `servervalidation.jsp`  — 也在對 `POST`。

### 顯示和隱藏窗體元件 {#showing-and-hiding-form-components}

您可以根據表單中其他欄位的值配置表單以顯示或隱藏表單元件。

僅在特定條件下需要更改表單域的可見性時，更改表單域的可見性非常有用。 例如，在反饋表上，有一個問題詢問客戶是否希望通過電子郵件將產品資訊發送給他們。 選擇「是」後，將顯示一個文本欄位，使客戶能夠鍵入其電子郵件地址。

使用 **編輯顯示/隱藏規則** 對話框，指定顯示或隱藏窗體元件的條件。

![鞋基編輯器](assets/showhideeditor.png)

使用對話框頂部的欄位指定以下資訊：

* 是否指定隱藏或顯示元件的條件。
* 顯示或隱藏元件時，是否需要任何或所有條件都為true。

這些欄位下面顯示一個或多個條件。 條件將另一個窗體元件（在同一窗體上）的值與值進行比較。 如果欄位中的實際值滿足該條件，則該條件將計算為true。 條件包括以下資訊：

* 測試的表單域的標題。
* 操作員。
* 將值與欄位值進行比較。

例如，帶標題的Radio Group元件 `Receive email notifications?`* *包含 `Yes` 和 `No` 單選按鈕。 標題為 `Email Address` 使用以下條件，以便在 `Yes` 已選中：

![毀滅](assets/showhidecondition.png)

在Javascript中，條件使用「元素名稱」屬性的值來引用欄位。 在上例中，Radio Group元件的Element Name屬性為 `contact`。 以下代碼是該示例的等效Javascript代碼：

`((contact == "Yes"))`

**要顯示或隱藏表單元件：**

1. 編輯特定窗體元件。

1. 選擇 **顯示/隱藏** 開啟 **編輯顯示/隱藏規則** 對話框：

   * 在第一個下拉清單中，選擇 **顯示** 或 **隱藏** 指定條件是否確定是顯示還是隱藏元件。

   * 在頂行末尾的下拉清單中，選擇：

      * **全部**  — 如果要顯示或隱藏元件，所有條件必須為真
      * **任何**  — 如果只有一個或多個條件必須為true才能顯示或隱藏元件
   * 在條件行（一個顯示為預設值）中，選擇元件、運算子，然後指定值。
   * 如果需要，可通過按一下添加更多條件 **添加條件**。

   例如：

   ![chlimage-1-9](assets/chlimage_1-9.png)

1. 按一下 **確定** 的子菜單。

1. 保存定義後， **編輯規則** 連結出現在 **顯示/隱藏** 的子菜單。 按一下此連結以開啟 **編輯顯示/隱藏規則** 對話框。

   按一下 **確定** 的子菜單。

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >可以查看和測試「顯示/隱藏」定義的效果：
   >
   >* 在 **預覽** 模式（首次切換到預覽時需要重新載入頁面）
   >
   >* 在發佈環境上


#### 處理斷開的元件參照 {#handling-broken-component-references}

顯示/隱藏條件使用「元素名稱」屬性的值來引用窗體中的其他元件。 如果任何條件都引用已刪除或已更改元素名稱屬性的元件，則顯示/隱藏配置無效。 出現這種情況時，需要手動更新條件，或在載入表單時出現錯誤。

當「顯示/隱藏」配置無效時，該配置僅作為JavaScript代碼提供。 編輯代碼以更正問題。代碼使用最初用於引用元件的「元素名稱」屬性。

### 開發用於Forms的指令碼 {#developing-scripts-for-use-with-forms}

有關編寫指令碼時可使用的API元素的詳細資訊，請參見 [javadoc與表單相關](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html)。

您可以將此功能用於以下操作：在提交表單之前調用服務；如果服務失敗，則取消服務：

* 定義驗證資源類型
* 包括用於驗證的指令碼：

   * 在JSP中，調用Web服務並建立 `com.day.cq.wcm.foundation.forms.ValidationInfo` 包含錯誤消息的對象。 如果有錯誤，則不會發佈表單資料。
