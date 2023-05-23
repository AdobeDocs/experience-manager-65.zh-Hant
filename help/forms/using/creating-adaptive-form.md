---
title: 如何建立自適應窗體
description: 瞭解如何使用 [!DNL Experience Manager Forms]。 自適應表單是響應性HTML5表單，可簡化資訊收集和處理。 更深入地瞭解如何根據表單資料模型、XFA表單模板和XML或JSON架構建立自適應表單。
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 2c25a8b7-73f7-40fb-a303-9446a708c8eb
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 0%

---

# 建立自適應窗體 {#creating-an-adaptive-form}

## <strong>建立自適應窗體</strong> {#strong-create-an-adaptive-form-strong}

按照以下步驟建立自適應表單。

1. 訪問 [!DNL Experience Manager Forms] 作者實例位於 `https://'[server]:[port]'/<custom-context-if-any>.`

1. 在Experience Manager登錄頁上輸入憑據。

   登錄後，在左上角，點擊 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。

   >[!NOTE]
   >
   >對於預設安裝，登錄名為 `admin` 密碼是 `admin`。

1. 點擊 **[!UICONTROL 建立]** 選擇 **[!UICONTROL 自適應窗體]**。
1. 將顯示一個選擇模板的選項。 有關模板的詳細資訊，請參見 [自適應表單模板](creating-adaptive-form.md#p-adaptive-form-templates-p)。 點擊模板以選擇它，然後點擊「下一步」。
1. 出現「添加屬性」選項。 指定以下屬性欄位的值。 「標題」(Title)和「名稱」(Name)欄位是必填的：

   * **[!UICONTROL 標題：]** 指定窗體的顯示名稱。 標題可幫助您在 [!DNL Experience Manager Forms] 用戶介面。
   * **[!UICONTROL 名稱：]** 指定窗體的名稱。 在儲存庫中建立具有指定名稱的節點。 開始鍵入標題時，將自動生成名稱欄位的值。 您可以更改建議的值。 名稱欄位只能包含字母數字字元、連字元和下划線。 所有無效輸入都用連字元替換。
   * **[!UICONTROL 描述：]** 指定有關表單的詳細資訊。
   * **[!UICONTROL 標籤：]** 指定用於唯一標識自適應表單的標籤。 標籤在搜索窗體中的幫助。 要建立標籤，請在 **[!UICONTROL 標籤]** 框。

1. 可以基於以下表單模型之一建立自適應表單：

   * [窗體資料模型](#fdm)
   * [XFA表單模板](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [XML或JSON架構](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * 無或沒有任何窗體模型

   您可以從 **[!UICONTROL 窗體模型]** 的 **[!UICONTROL 添加屬性]** 的子菜單。 預設情況下，所選的表單模型為 **[!UICONTROL 無]**。

1. 點擊 **[!UICONTROL 建立]**。 建立一個自適應表單，並出現一個用於開啟表單以進行編輯的對話框。

   指定完所有屬性後，按一下 **[!UICONTROL 建立]**。 建立一個自適應表單，並出現一個用於開啟表單以進行編輯的對話框。

   指定完所有屬性後，按一下 **[!UICONTROL 建立]**。 建立一個自適應表單，並出現一個用於開啟表單以進行編輯的對話框。

1. 點擊 **[!UICONTROL 開啟]** 的子菜單。 此窗體開啟以進行編輯，並顯示模板中的可用內容。 它還顯示邊欄，以根據需要定制新建立的表單。

   根據自適應表單的類型，在關聯的XFA表單模板、XML架構或JSON架構中存在的表單元素將顯示在 **[!UICONTROL 資料模型對象]** 頁籤 **[!UICONTROL 內容瀏覽器]** 欄。 也可以拖放這些元素來構建自適應窗體。

   有關自適應表單創作介面和可用元件的資訊，請參見 [創作自適應表單簡介](introduction-forms-authoring.md)。

   >[!NOTE]
   >
   >允許瀏覽器中的彈出窗口在新頁籤中開啟新建立的窗體。

## 基於表單資料模型建立自適應表單 {#fdm}

[[!DNL Experience Manager Forms] 資料整合](data-integration.md) 允許您整合多個資料源，並將其實體和服務組合在一起以建立表單資料模型。 它是JSON架構的擴展。 可以使用表單資料模型建立自適應表單。 在表單資料模型中配置的實體或資料模型對象可用作表單創作的資料模型對象。 它們綁定到各自的資料源，用於預填表單並將提交的資料寫回各自的資料源。 您還可以使用自適應表單規則調用表單資料模型中配置的服務。

要使用表單資料模型建立自適應表單，請執行以下操作：

1. 在「添加屬性」螢幕的「表單模型」頁籤中，選擇 **[!UICONTROL 窗體資料模型]** 的 **[!UICONTROL 從中選擇]** 的子菜單。

   ![建立af-1-1](assets/create-af-1-1.png)

1. 點擊以展開 **[!UICONTROL 選擇表單資料模型]**。 列出所有可用表單資料模型。

   從資料模型中選擇。

   ![建立af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>也可以更改自適應表單的表單資料模型。 有關詳細步驟，請參見 [編輯自適應表單的表單模型屬性](#edit-form-model)。

## 基於XFA表單模板建立自適應表單 {#create-an-adaptive-form-based-on-an-xfa-form-template}

您可以重新調整XFA表單模板的用途以建立自適應表單。 要重新調整用途，請上載XFA表單模板並將其與自適應表單關聯。 表單模板（XFA表單）的元素在進行自適應表單創作時可用於內容查找器。 在Content Finder中，可以在表單上拖放表單模板元素。

<!-- >>[!NOTE]
>
>[Upload the XFA Form Template](get-xdp-pdf-documents-aem.md) to AEM Forms before you start creating an adaptive form based on the form template.

Do the following to use an XFA form template as form model for your adaptive form:

1. On the **[!UICONTROL Add Properties]** page, open the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, from the drop-down list, select **[!UICONTROL Form Templates]**. All the form templates that are uploaded to the repository via AEM Forms UI are listed for selection. Select a template from the list.

   ![Associate XFA Form Template with an Adaptive Form](assets/form_model_xfa_associate.png)
**Figure:** *Selecting a form template*

   >[!NOTE]
   >
   >You can also change the form template for an adaptive form. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model). -->

## 基於XML或JSON架構建立自適應表單 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML和JSON架構表示組織中後端系統生成或使用資料的結構。 可以將模式與自適應表單相關聯，並使用其元素將動態內容添加到自適應表單。 模式的元素可在內容瀏覽器的「資料模型對象」頁籤中用於創作自適應表單。 可以拖放架構元素以構建表單。

請參閱以下文檔，瞭解如何為創作自適應表單設計XML或JSON架構。

* [使用XML架構建立自適應表單](adaptive-form-xml-schema-form-model.md)
* [使用JSON架構建立自適應表單](adaptive-form-json-schema-form-model.md)

執行以下操作以將XML或JSON架構用作自適應表單的表單模型：

1. 在 **[!UICONTROL 添加屬性]** 「自適應表單建立」頁的步驟，點擊 **[!UICONTROL 窗體模型]** 頁籤。
1. 在「表單模型」(Form Model)頁籤中，選擇 **[!UICONTROL 架構]** 從 **[!UICONTROL 從中選擇]** 下拉欄位。

1. 點擊 **[!UICONTROL 選擇方案]** 並執行以下操作之一：

   * **[!UICONTROL 從磁碟上載]**  — 選擇此選項，然後點擊「上載架構定義」以瀏覽並從檔案系統上載XML架構或JSON架構。 上載的架構檔案駐留在窗體中，並且無法訪問其他自適應窗體。
   * **[!UICONTROL 在儲存庫中搜索]**  — 選擇此選項可從儲存庫中可用的架構定義檔案清單中選擇。 選擇XML或JSON架構檔案作為表單模型。 所選模式通過引用與表單相關聯，並且可以在其它自適應表單中使用。

   >[!CAUTION]
   >
   >確保JSON架構檔案名以結尾 **.schema.json**。 例如：mySchema.schema.json

   ![選擇XML或JSON架構](assets/upload-schema.png)
   **圖：** *選擇XML或JSON架構*

1. （僅適用於XML架構）在選擇或上載XML架構後，請指定選定XSD檔案的根元素，以使用自適應表單進行映射。

   ![選擇XSD根元素](assets/xsd-root-element.png)
   **圖：** *選擇XSD根元素*

>[!NOTE]
>
>也可以更改自適應表單的模式。 有關詳細步驟，請參見 [編輯自適應表單的表單模型屬性](#edit-form-model)。

## 自適應表單模板 {#adaptive-form-templates}

模板提供基本結構並定義自適應表單的外觀（佈局和樣式）。 它具有預格式化的元件，包含某些屬性和內容結構。 <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

此外，您還可以使用模板編輯器建立自己的模板。 有關使用模板的詳細資訊，請參閱 [自適應表單模板](template-editor.md)。

>[!NOTE]
>
>開啟使用高級模板建立的用於編輯的自適應表單時，將顯示一條錯誤消息。 高級模板具有「簽名步驟」元件，預設情況下為其啟用Adobe Sign。 建立並選擇 [Adobe Sign雲配置](adobe-sign-integration-adaptive-forms.md) 和 [配置簽名者](working-with-adobe-sign.md#addsignerstoanadaptiveform) 以解決錯誤。

## 編輯自適應表單的表單模型屬性 {#edit-form-model}

建立自適應表單時不使用表單模型（使用表單模型的「無」選項），也不使用表單模型，如表單模板、XML架構或JSON架構或表單資料模型。 可以將自適應表單的表單模型從「無」更改為其它表單模型。 對於基於表單模型的自適應表單，可以為同一表單模型選擇其他表單模板、XML架構、JSON架構或表單資料模型。 但是，不能將一個表單模型更改為另一個表單模型。

1. 選擇自適應窗體並點擊 **屬性** 表徵圖
1. 開啟 **[!UICONTROL 窗體模型]** ，然後執行以下操作之一。

   * 如果自適應表單沒有表單模型，則可以選擇另一個表單模型，並相應地選擇表單模板、XML或JSON架構或表單資料模型。
   * 如果自適應表單基於表單模型，則可以為同一表單模型選擇其他表單模板、XML或JSON架構或表單資料模型。

1. 點擊 **[!UICONTROL 保存]** 的子菜單。

## 自動保存自適應表單 {#auto-save-an-adaptive-form}

預設情況下，自適應表單的內容會保存在用戶操作上，如按「保存」按鈕。 您還可以配置一個自適應表單，以便根據事件或時間間隔自動開始保存內容。 自動保存選項在以下方面非常有用：

* 自動為匿名用戶和登錄用戶保存內容
* 保存表單的內容而無需或用戶干預最少
* 開始基於用戶事件保存表單的內容
* 在指定時間間隔後重複保存表單的內容

### 為自適應表單啟用自動保存 {#enable-auto-save-for-an-adaptive-form}

預設情況下，未啟用自動保存選項。 可以從自適應表單的「自動保存」頁籤中啟用自動保存選項。 「自動保存」頁籤還提供了幾個其他配置選項。 執行以下步驟以啟用和配置自適應表單的自動保存選項：

1. 要訪問屬性中的自動保存部分，請選擇一個元件，然後點擊 ![欄位級](assets/field-level.png) > **[!UICONTROL 自適應窗體容器]**，然後按一下 ![招商](assets/cmppr.png)。
1. 在 **[!UICONTROL 自動保存]** 的 **[!UICONTROL 啟用]** 自動保存。
1. 在 **[!UICONTROL 自適應窗體事件]** 框中，指定1或TRUE以在表單載入到瀏覽器中時自動開始保存表單。 您還可以為事件指定條件表達式，當觸發並返回true時，該表達式將開始保存表單的內容。
1. 指定觸發器。 根據您的配置觸發自動保存。 您的選項包括：

   * **[!UICONTROL 基於時間：]** 選擇選項以根據特定時間間隔開始保存內容。
   * **[!UICONTROL 基於事件：]** 選擇選項以在觸發事件時開始保存內容。

   選擇觸發器時，將啟用「策略配置」框。 「策略配置」框允許您：

   * 如果選擇，則指定時間間隔 **[!UICONTROL 基於時間]** 觸發器。
   * 如果選擇，請指定事件名稱 **[!UICONTROL 基於事件]** 觸發器。

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. （僅限基於時間的自動保存）執行以下步驟來配置基於時間的自動保存選項。

   1. 在 **[!UICONTROL 在此間隔自動保存]** 框中，以秒為單位指定時間間隔。 在間隔框中指定的秒數過後，會重複保存表單。

1. （僅基於事件的自動保存）執行以下步驟來配置基於事件的自動保存選項。

   1. 在 **[!UICONTROL 此事件後自動保存]** 框，指定 [導橋](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 的子菜單。 每次表達式計算為TRUE時，都會保存表單。

1. （可選）要自動為匿名用戶保存內容，請選擇 **[!UICONTROL 為匿名用戶啟用自動保存]** ，然後按一下 **[!UICONTROL 確定]**。

   >[!NOTE]
   >
   >要使匿名用戶使用自動保存選項，請確保將Forms通用配置服務配置為允許所有用戶預覽、驗證和簽名表單。
   >
   >要配置服務，請轉到Adobe Experience ManagerWeb控制台配置， `https://'[server]:[port]'system/console/configMgr` 編輯 **[!UICONTROL Forms通用配置服務]** 的子菜單。 **[!UICONTROL 所有用戶]** 的上界 **[!UICONTROL 允許]** ，並保存配置。
