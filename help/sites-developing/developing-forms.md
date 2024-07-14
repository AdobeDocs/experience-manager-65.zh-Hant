---
title: 開發Forms (Classic UI)
description: 瞭解如何為Adobe Experience Manager的Classic UI開發表單
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 0%

---

# 開發Forms (Classic UI){#developing-forms-classic-ui}

表單的基本結構為：

* 表單開始
* 表單元素
* 表單結尾

所有這些都是透過一系列預設[表單元件](/help/sites-authoring/default-components.md#form)實現的，這些元件可在標準AEM安裝中使用。

除了[開發新元件](/help/sites-developing/developing-components-samples.md)以用於您的表單之外，您還可以：

* [使用值預先載入您的表單](#preloading-form-values)
* [預先載入（特定）具有多個值的欄位](#preloading-form-fields-with-multiple-values)
* [開發新動作](#developing-your-own-form-actions)
* [開發新的限制](#developing-your-own-form-constraints)
* [顯示或隱藏特定表單欄位](#showing-and-hiding-form-components)

[在必要時使用指令碼](#developing-scripts-for-use-with-forms)來擴充功能。

>[!NOTE]
>
>本檔案著重於在傳統UI中使用[Foundation元件](/help/sites-authoring/default-components-foundation.md)來開發表單。 Adobe建議在觸控式UI中使用新的[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)和[隱藏條件](/help/sites-developing/hide-conditions.md)進行表單開發。

## 預先載入表單值 {#preloading-form-values}

表單開始元件提供&#x200B;**載入路徑**&#x200B;的欄位，此路徑為指向存放庫中節點的選用路徑。

載入路徑是節點屬性的路徑，用來將預先定義的值載入表單上的多個欄位中。

此選擇性欄位指定存放庫中節點的路徑。 當此節點具有符合欄位名稱的屬性時，則表單上的適當欄位將使用這些屬性的值預先載入。 如果不存在相符專案，則欄位會包含預設值。

>[!NOTE]
>
>[表單動作](#developing-your-own-form-actions)也可以設定載入初始值的資源。 這是使用`init.jsp`中的`FormsHelper#setFormLoadResource`完成的。
>
>唯有未設定時，作者才會從起始表單元件中設定的路徑填入表單。

### 預先載入具有多個值的表單欄位 {#preloading-form-fields-with-multiple-values}

各種表單欄位也有&#x200B;**專案載入路徑**，同樣是指向存放庫中的節點的選用路徑。

**專案載入路徑**&#x200B;是節點屬性的路徑，用來將預先定義的值載入表單上的特定欄位，例如[下拉式清單](/help/sites-authoring/default-components-foundation.md#dropdown-list)、[核取方塊群組](/help/sites-authoring/default-components-foundation.md#checkbox-group)或[選項群組](/help/sites-authoring/default-components-foundation.md#radio-group)。

#### 範例 — 預先載入含有多個值的下拉式清單 {#example-preloading-a-dropdown-list-with-multiple-values}

下拉式清單可以設定您選取的值範圍。

**專案載入路徑**&#x200B;可用於從存放庫中的資料夾存取清單，並將它們預先載入欄位中：

1. 建立Sling資料夾( `sling:Folder`)
例如，`/etc/designs/<myDesign>/formlistvalues`

1. 新增多值字串( `String[]`)型別的新屬性（例如`myList`），以包含下拉式清單專案的清單。 也可以使用指令碼匯入內容，例如使用JSP指令碼或shell指令碼中的cURL。

1. 在&#x200B;**專案載入路徑**欄位中使用完整路徑：
例如，`/etc/designs/geometrixx/formlistvalues/myList`

請注意，如果`String[]`中的值格式如下：

* `AL=Alabama`
* `AK=Alaska`

依此類推，則AEM產生清單為：

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

舉例來說，這項功能在多語言設定中可以妥善運用。

### 開發您自己的表單動作 {#developing-your-own-form-actions}

表單需要動作。 動作會定義隨使用者資料提交表單時所執行的操作。

標準AEM安裝會提供一系列動作，您可以在下列位置看到這些動作：

`/libs/foundation/components/form/actions`

在&#x200B;**表單**&#x200B;元件的&#x200B;**動作型別**&#x200B;清單中：

![chlimage_1-8](assets/chlimage_1-8.png)

本節說明如何開發自己的表單動作以包含在此清單中。

您可以在`/apps`下新增您自己的動作，如下所示：

1. 建立型別`sling:Folder`的節點。 指定可反映要實作之動作的名稱。

   例如：

   `/apps/myProject/components/customFormAction`

1. 在此節點上定義下列屬性，然後按一下[儲存全部] **以保留您的變更：**

   * `sling:resourceType` — 設為`foundation/components/form/action`

   * `componentGroup` — 定義為`.hidden`

   * 選擇性：

      * `jcr:title` — 指定您選擇的標題，這會顯示在下拉式選擇清單中。 如果未設定，則會顯示節點名稱

      * `jcr:description` — 輸入您選擇的說明

1. 在資料夾中建立對話方塊節點：

   1. 新增欄位，以便在選擇動作後，作者可以編輯表單對話方塊。

1. 在資料夾中建立：

   1. 後置指令碼。
指令碼的名稱為`post.POST.<extension>`，例如`post.POST.jsp`
在提交表單以處理表單時，會叫用後置指令碼，其中包含處理來自表單`POST`之資料的程式碼。

   1. 新增在提交表單時叫用的轉寄指令碼。
指令碼的名稱為`forward.<extension`>，例如`forward.jsp`
此指令碼可定義路徑。 接著會將目前的請求轉送至指定的路徑。

   必要的呼叫是`FormsHelper#setForwardPath` （2個變體）。 典型案例是執行一些驗證或邏輯來尋找目標路徑，然後前進到該路徑，讓預設的SlingPOSTservlet實際執行JCR中的儲存。

   也可能有另一個servlet執行實際處理，在這種情況下，表單動作和`forward.jsp`將只當作「貼上」程式碼。 這方面的範例是位於`/libs/foundation/components/form/actions/mail`的郵件動作，其會將詳細資料轉寄給郵件servlet所在的`<currentpath>.mail.html`。

   所以：

   * `post.POST.jsp`對於完全由動作本身完成的小型作業非常有用
   * 而`forward.jsp`在只需要委派時很有用。

   指令碼的執行順序為：

   * 轉譯表單( `GET`)時：

      1. `init.jsp`
      1. 所有欄位的限制： `clientvalidation.jsp`
      1. 表單的validationRT： `clientvalidation.jsp`
      1. 表單已透過載入資源載入（如果已設定）
      1. `addfields.jsp` （在演算`<form></form>`內）

   * 處理表單`POST`時：

      1. `init.jsp`
      1. 所有欄位的限制： `servervalidation.jsp`
      1. 表單的validationRT： `servervalidation.jsp`
      1. `forward.jsp`
      1. 如果已設定轉寄路徑( `FormsHelper.setForwardPath`)，則轉寄要求，然後呼叫`cleanup.jsp`

      1. 如果未設定轉送路徑，請呼叫`post.POST.jsp` （在此結束，未呼叫`cleanup.jsp`）

1. 再次在資料夾中選擇性地新增：

   1. 用於新增欄位的指令碼。
指令碼的名稱為`addfields.<extension>`，例如`addfields.jsp`
在寫入表單起始HTML後，會立即叫用`addfields`指令碼。 這可讓動作在表單內新增自訂輸入欄位或其他此類HTML。

   1. 初始化指令碼。
指令碼的名稱為`init.<extension>`，例如`init.jsp`
此指令碼會在表單轉譯時叫用。 這可用來初始化動作細節。

   1. 清除指令碼。
指令碼的名稱為`cleanup.<extension>`，例如`cleanup.jsp`
此指令碼可用於執行清理。

1. 在parsys中使用&#x200B;**Forms**&#x200B;元件。 **動作型別**&#x200B;下拉式清單現在會包含您的新動作。

   >[!NOTE]
   >
   >若要檢視屬於產品一部分的預設動作：
   >
   >
   >`/libs/foundation/components/form/actions`

### 開發您自己的表單限制 {#developing-your-own-form-constraints}

可在兩個層級施加限制：

* 針對[個別欄位（請參閱下列程式）](#constraints-for-individual-fields)
* 作為[表單全域驗證](#form-global-constraints)

#### 個別欄位的限制 {#constraints-for-individual-fields}

您可以為個別欄位（`/apps`下）新增自己的條件約束，如下所示：

1. 建立型別`sling:Folder`的節點。 指定反映要實作之限制的名稱。

   例如：

   `/apps/myProject/components/customFormConstraint`

1. 在此節點上定義下列屬性，然後按一下[儲存全部] **以保留您的變更：**

   * `sling:resourceType` — 設定為`foundation/components/form/constraint`

   * `constraintMessage` — 提交表單時，如果欄位無效，根據限制，會顯示自訂訊息

   * 選擇性：

      * `jcr:title` — 指定您選取的標題，這會顯示在選取專案清單中。 如果未設定，則會顯示節點名稱
      * `hint` — 使用者如何使用該欄位的額外資訊

1. 在此資料夾中，您需要下列指令碼：

   * 使用者端驗證指令碼：
指令碼的名稱為`clientvalidation.<extension>`，例如`clientvalidation.jsp`
這會在表單欄位轉譯時叫用。 它可用來建立使用者端JavaScript，以驗證使用者端上的欄位。

   * 伺服器驗證指令碼：
指令碼的名稱為`servervalidation.<extension>`，例如`servervalidation.jsp`
這會在表單提交時叫用。 它可用於在提交欄位後驗證伺服器上的欄位。

>[!NOTE]
>
>範例限制可見於：
>
>`/libs/foundation/components/form/constraints`

#### 表單全域限制 {#form-global-constraints}

透過在起始表單元件( `validationRT`)中設定資源型別來指定表單全域驗證。 例如：

`apps/myProject/components/form/validation`

接著，您可以定義：

* `clientvalidation.jsp` — 插入欄位的使用者端驗證指令碼之後
* 和`servervalidation.jsp` — 也在`POST`上的個別欄位伺服器驗證之後呼叫。

### 顯示和隱藏表單元件 {#showing-and-hiding-form-components}

您可以根據表單中其他欄位的值，設定表單以顯示或隱藏表單元件。

只有在特定條件下才需要表單欄位時，變更欄位的可見度會很有用。 例如，在意見回饋表單上，系統會詢問客戶是否希望以電子郵件傳送產品資訊。 選取「是」後，會出現文字欄位，讓客戶輸入其電子郵件地址。

使用&#x200B;**編輯顯示/隱藏規則**&#x200B;對話方塊來指定顯示或隱藏表單元件的條件。

![showhideeditor](assets/showhideeditor.png)

使用對話方塊頂端的欄位來指定下列資訊：

* 指定隱藏或顯示元件的條件。
* 是否需有任何或所有條件必須為true才能顯示或隱藏元件。

一或多個條件會顯示在這些欄位下方。 條件會將另一個表單元件（位於相同表單）的值與一個值比較。 如果欄位中的實際值符合條件，則條件的評估結果為true。 條件包括下列資訊：

* 測試的表單欄位的標題。
* 運運算元。
* 比對的值會與欄位值比較。

例如，標題為`Receive email notifications?`* *的選項群組元件包含`Yes`和`No`選項按鈕。 標題為`Email Address`的文字欄位元件會使用以下條件，以便在選取`Yes`時可見：

![showhidecondition](assets/showhidecondition.png)

在JavaScript中，條件會使用Element Name屬性的值來參照欄位。 在上一個範例中，Radio Group元件的Element Name屬性是`contact`。 下列程式碼與該範例的JavaScript程式碼相同：

`((contact == "Yes"))`

**若要顯示或隱藏表單元件：**

1. 編輯特定的表單元件。

1. 選取&#x200B;**顯示/隱藏**&#x200B;以開啟&#x200B;**編輯顯示/隱藏規則**&#x200B;對話方塊：

   * 在第一個下拉式清單中選取&#x200B;**顯示**&#x200B;或&#x200B;**隱藏**，以指定您的條件是否決定要顯示或隱藏元件。

   * 在上行末端的下拉式清單中選取：

      * **all** — 如果所有條件都必須為true才能顯示或隱藏元件
      * **any** — 如果只有一個或多個條件必須為true才能顯示或隱藏元件

   * 在條件行（其中一個顯示為預設值）中，選取元件、運運算元，然後指定值。
   * 視需要按一下&#x200B;**新增條件**，以新增更多條件。

   例如：

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. 按一下&#x200B;**確定**&#x200B;以儲存定義。

1. 儲存定義後，表單元件屬性中的&#x200B;**顯示/隱藏**&#x200B;選項旁邊會顯示&#x200B;**編輯規則**&#x200B;連結。 按一下此連結以開啟&#x200B;**編輯顯示/隱藏規則**&#x200B;對話方塊以進行變更。

   按一下&#x200B;**確定**&#x200B;以儲存所有變更。

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >可以看見並測試「顯示/隱藏」定義的效果：
   >
   >* 在作者環境上的&#x200B;**預覽**&#x200B;模式中（第一次切換為預覽時需要重新載入頁面）
   >
   >* 在發佈環境中

#### 處理中斷的元件參照 {#handling-broken-component-references}

顯示/隱藏條件會使用Element Name屬性的值來參照表單中的其他元件。 當任何條件引用已刪除或已變更Element Name屬性的元件時，顯示/隱藏設定無效。 發生這種情況時，您需要手動更新條件，否則表單載入時發生錯誤。

顯示/隱藏設定無效時，系統只會以JavaScript程式碼的形式提供設定。 編輯程式碼以修正問題。程式碼使用原本用來參考元件的Element Name屬性。

### 開發指令碼以與Forms搭配使用 {#developing-scripts-for-use-with-forms}

如需可在編寫指令碼時使用的API元素的詳細資訊，請參閱與表單](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html)相關的[javadocs。

您可以將此用於動作，例如在提交表單前呼叫服務，以及在服務失敗時取消服務：

* 定義驗證資源型別
* 包含用於驗證的指令碼：

   * 在您的JSP中，呼叫您的Web服務並建立包含錯誤訊息的`com.day.cq.wcm.foundation.forms.ValidationInfo`物件。 如果發生錯誤，將不會張貼表單資料。
