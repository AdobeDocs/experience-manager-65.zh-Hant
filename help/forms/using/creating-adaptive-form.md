---
title: 如何建立最適化表單
description: '瞭解如何使用 [!DNL Experience Manager Forms]建立最適化表單。 最適化表單是互動式HTML5表單，可簡化資訊收集和處理。 深入瞭解如何根據表單資料模型、XFA表單範本和XML或JSON結構描述建立最適化表單。 '
feature: 適用性表單
role: Business Practitioner, Developer
level: Beginner
exl-id: 2c25a8b7-73f7-40fb-a303-9446a708c8eb
translation-type: tm+mt
source-git-commit: ad67634278088f8f953fde61a3543acdd70537dd
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# 建立最適化表單{#creating-an-adaptive-form}

## <strong>建立最適化表單</strong> {#strong-create-an-adaptive-form-strong}

請依照下列步驟建立最適化表單。

1. 在`https://'[server]:[port]'/<custom-context-if-any>.`存取[!DNL Experience Manager Forms]作者實例

1. 在Experience Manager登錄頁上輸入您的憑據。

   登入後，在左上角點選&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。

   >[!NOTE]
   >
   >對於預設安裝，登錄名為`admin` ，口令為`admin`。

1. 點選「**[!UICONTROL 建立]**」並選取「最適化表單」。****
1. 此時會出現選擇範本的選項。 如需範本的詳細資訊，請參閱[最適化表單範本](creating-adaptive-form.md#p-adaptive-form-templates-p)。 點選範本以選取範本，然後點選「下一步」。
1. 出現「Add Properties（添加屬性）」選項。 指定下列屬性欄位的值。 「標題」和「名稱」欄位是必填欄位：

   * **[!UICONTROL 標題：]** 指定表單的顯示名稱。標題可協助您識別[!DNL Experience Manager Forms]使用者介面中的表單。
   * **[!UICONTROL 名稱：]** 指定表單的名稱。在儲存庫中建立具有指定名稱的節點。 當您開始輸入標題時，系統會自動產生名稱欄位的值。 您可以變更建議的值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。
   * **[!UICONTROL 說明：]** 指定表單的詳細資訊。
   * **[!UICONTROL 標籤：指]** 定標籤以唯一識別最適化表單。標籤可協助搜尋表單。 若要建立標籤，請在&#x200B;**[!UICONTROL Tags]**&#x200B;方塊中輸入新標籤名稱。

1. 您可以根據下列其中一個表單模型建立最適化表單：

   * [表單資料模型](#fdm)
   * [XFA表單範本](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [XML或JSON結構描述](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * 無或沒有任何表單模型

   您可以從&#x200B;**[!UICONTROL 添加屬性]**&#x200B;頁面的&#x200B;**[!UICONTROL 表單模型]**&#x200B;標籤配置這些屬性。 預設情況下，選擇的表單模型為&#x200B;**[!UICONTROL 無]**。

1. 點選&#x200B;**[!UICONTROL Create]**。 會建立最適化表單，並出現對話方塊以開啟表單以供編輯。

   指定完所有屬性後，按一下&#x200B;**[!UICONTROL 建立]**。 會建立最適化表單，並出現對話方塊以開啟表單以供編輯。

   指定完所有屬性後，按一下&#x200B;**[!UICONTROL 建立]**。 會建立最適化表單，並出現對話方塊以開啟表單以供編輯。

1. 點選「**[!UICONTROL 開啟]**」，在新標籤中開啟新建立的表格。 表格隨即開啟以供編輯，並顯示範本中可用的內容。 它還顯示邊欄，以根據需求自訂新建立的表格。

   根據最適化表單的類型，關聯的XFA表單範本、XML表單或JSON表單中的表單元素會顯示在側欄中&#x200B;**[!UICONTROL 內容瀏覽器]**&#x200B;的&#x200B;**[!UICONTROL 資料模型物件]**&#x200B;標籤中。 您也可以拖放這些元素來建立最適化表單。

   有關最適化表單製作介面和可用元件的資訊，請參閱[製作最適化表單簡介](introduction-forms-authoring.md)。

   >[!NOTE]
   >
   >允許瀏覽器中的彈出式視窗在新標籤中開啟新建立的表格。

## 根據表單資料模型{#fdm}建立最適化表單

[[!DNL Experience Manager Forms] 資料](data-integration.md) 整合可讓您整合多個資料來源，並將其實體和服務整合在一起，以建立表單資料模型。它是JSON結構描述的擴充功能。 您可以使用表單資料模型來建立最適化表單。 在表單資料模型中配置的實體或資料模型對象可用作表單創作的資料模型對象。 這些資料系結至個別的資料來源，用來預先填寫表單，並將提交的資料寫回個別的資料來源。 您也可以使用最適化表單規則呼叫在表單資料模型中設定的服務。

要使用表單資料模型建立自適應表單：

1. 在「添加屬性」螢幕的「表單模型」頁籤中，從&#x200B;**[!UICONTROL 從]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL 表單資料模型]**。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 點選以展開&#x200B;**[!UICONTROL 選擇表單資料模型]**。 列出所有可用的表單資料模型。

   從資料模型中選擇。

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>您也可以變更最適化表單的表單資料模型。 有關詳細步驟，請參見[編輯最適化表單的表單模型屬性](#edit-form-model)。

## 基於XFA表單模板{#create-an-adaptive-form-based-on-an-xfa-form-template}建立自適應表單

您可以重新運用XFA表單範本來建立最適化表單。 若要重新使用，請上傳XFA表單範本並將其與最適化表單建立關聯。 表單範本（XFA表單）的元素可在製作最適化表單時用於內容搜尋器。 從「內容搜尋器」中，您可以拖放表單上的表單範本元素。

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

## 建立以XML或JSON結構描述{#create-an-adaptive-form-based-on-xml-or-json-schema}為基礎的最適化表單

XML和JSON結構描述資料由組織中的後端系統產生或使用的結構。 您可以將架構與最適化表單建立關聯，並使用其元素將動態內容新增至最適化表單。 架構的元素可在內容瀏覽器的「資料模型物件」索引標籤中使用，以製作最適化表單。 您可以拖放架構元素來建立表單。

請參閱下列檔案，以瞭解如何設計XML或JSON架構以製作最適化表單。

* [使用XML架構建立最適化表單](adaptive-form-xml-schema-form-model.md)
* [使用JSON結構描述建立最適化表單](adaptive-form-json-schema-form-model.md)

請執行下列動作，將XML或JSON結構描述用作最適化表單的表單模型：

1. 在最適化表單建立頁面的「新增屬性」步驟中，點選「表單模型」標籤。********
1. 在「表單模型」頁籤中，從&#x200B;**[!UICONTROL 從]**&#x200B;下拉欄位中選擇&#x200B;**[!UICONTROL 方案]**。

1. 點選「**[!UICONTROL 選擇架構]**」並執行下列任一操作：

   * **[!UICONTROL 從磁碟上傳]** -選取此選項，並點選「上傳結構描述定義」，從您的檔案系統瀏覽及上傳XML結構描述或JSON結構描述。已上載的架構檔案駐留在表單中，而且無法訪問其他自適應表單。
   * **[!UICONTROL 在儲存庫中搜索]** -選擇此選項可從儲存庫中可用的方案定義檔案清單中進行選擇。選取XML或JSON結構描述檔做為表單模型。 所選擇的模式通過引用與表單相關聯，並且可訪問以用於其它自適應表單。

   >[!CAUTION]
   >
   >請確定JSON結構描述檔名結尾為&#x200B;**.schema.json**。 例如：mySchema.schema.json

   ![選取XML或JSON結構描述](assets/upload-schema.png)
   **圖：選** *擇XML或JSON結構描述*

1. （僅適用於XML架構）選擇或上傳XML架構後，請指定所選XSD檔案的根元素，以與最適化表單對應。

   ![選擇XSD根元素](assets/xsd-root-element.png)
   **圖：選** *擇XSD根元素*

>[!NOTE]
>
>您也可以變更最適化表單的架構。 有關詳細步驟，請參見[編輯最適化表單的表單模型屬性](#edit-form-model)。

## 最適化表單範本{#adaptive-form-templates}

範本提供基本結構並定義最適化表單的外觀（版面和樣式）。 它具有預先格式化的元件，其中包含某些屬性和內容結構。<!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

此外，您也可以使用範本編輯器來建立自己的範本。 有關使用模板的詳細資訊，請參閱[最適化表單模板](template-editor.md)。

>[!NOTE]
>
>當您開啟使用進階範本建立的最適化表單進行編輯時，會出現錯誤訊息。 進階範本有「簽名步驟」元件，預設會啟用Adobe Sign。 建立並選取[Adobe Sign雲端組態](adobe-sign-integration-adaptive-forms.md)和[組態簽署者](working-with-adobe-sign.md#addsignerstoanadaptiveform)以解決錯誤。

## 編輯最適化表單{#edit-form-model}的表單模型屬性

最適化表單的建立不需使用表單模型（使用表單模型的「無」選項），或使用表單模型，例如表單範本、XML結構描述或JSON結構描述，或表單資料模型。 可將自適應表單的表單模型從「無」(None)更改為其它表單模型。 對於基於表單模型的最適化表單，您可以針對相同的表單模型選擇其他表單範本、XML結構描述、JSON結構描述或表單資料模型。 但是，不能將一個表單模型更改為另一個表單模型。

1. 選擇最適化表單，然後點選&#x200B;**屬性**&#x200B;圖示。
1. 開啟「**[!UICONTROL 表單模型]**」頁籤並執行下列操作之一。

   * 如果最適化表單沒有表單模型，您可以選擇其他表單模型，並據以選擇表單範本、XML或JSON結構描述或表單資料模型。
   * 如果最適化表單是以表單模型為基礎，您可以針對相同的表單模型選擇其他表單範本、XML或JSON結構描述，或表單資料模型。

1. 點選&#x200B;**[!UICONTROL Save]**&#x200B;以儲存屬性。

## 自動保存最適化表單{#auto-save-an-adaptive-form}

預設情況下，最適化表單的內容會保存在用戶操作上，例如按保存按鈕時。 您也可以設定自適應表單，以根據事件或時間間隔自動開始儲存內容。 自動儲存選項在下列項目中很實用：

* 自動儲存匿名和登入使用者的內容
* 儲存表單內容，毋需或最少的使用者干預
* 根據使用者事件開始儲存表格內容
* 在指定時間間隔後重複儲存表單內容

### 為最適化表單{#enable-auto-save-for-an-adaptive-form}啟用自動儲存

依預設，自動儲存選項不會啟用。 您可以從最適化表單的「自動儲存」索引標籤啟用自動儲存選項。 「自動保存」頁籤還提供了幾個其它配置選項。 執行以下步驟以啟用和配置最適化表單的自動保存選項：

1. 若要存取屬性中的自動儲存區段，請選取元件，然後點選![field-level](assets/field-level.png) > **[!UICONTROL 最適化表單容器]**，然後點選![cmppr](assets/cmppr.png)。
1. 在&#x200B;**[!UICONTROL 自動儲存]**&#x200B;區段中，**[!UICONTROL 啟用自動儲存選項。]**
1. 在&#x200B;**[!UICONTROL 最適化表單事件]**&#x200B;方塊中，指定1或TRUE，以在表單載入瀏覽器時自動開始儲存表單。 您也可以指定事件的條件運算式，當觸發並傳回true時，會開始儲存表單的內容。
1. 指定觸發器。 會根據您的設定觸發自動儲存。 您的選項包括：

   * **[!UICONTROL 基於時間：]** 選擇根據特定時間間隔開始保存內容的選項。
   * **[!UICONTROL 事件型：選]** 取在觸發事件時開始儲存內容的選項。

   選擇觸發器時，將啟用「策略配置」框。 「策略配置」框可讓您：

   * 如果選擇&#x200B;**[!UICONTROL 基於時間的]**&#x200B;觸發器，請指定時間間隔。
   * 如果您選擇&#x200B;**[!UICONTROL Event based]**&#x200B;觸發器，請指定事件名稱。

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. （僅限基於時間的自動保存）執行以下步驟以配置基於時間的自動保存選項。

   1. 在&#x200B;**[!UICONTROL 自動儲存此間隔]**&#x200B;方塊中，指定以秒為單位的時間間隔。 在間隔框中指定的秒數過後，會重複保存表單。

1. （僅限事件型自動儲存）執行下列步驟以設定事件型自動儲存的選項。

   1. 在&#x200B;**[!UICONTROL Auto save after this event]**&#x200B;方塊中，指定[GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)事件。 每次運算式評估為TRUE時，都會儲存表格。

1. （可選）要自動為匿名用戶保存內容，請選擇&#x200B;**[!UICONTROL 啟用匿名用戶自動保存選項，然後按一下**[!UICONTROL &#x200B;確定&#x200B;]**。]**

   >[!NOTE]
   >
   >若要自動儲存選項以供匿名使用者使用，請確定您已設定「Forms通用組態服務」，讓所有使用者都能預覽、驗證和簽署表格。
   >
   >要配置服務，請轉至`https://'[server]:[port]'system/console/configMgr`的Adobe Experience ManagerWeb控制台配置並編輯&#x200B;**[!UICONTROL Forms公共配置服務]**&#x200B;以在&#x200B;**[!UICONTROL 允許]**&#x200B;欄位中選擇&#x200B;**[!UICONTROL 所有用戶]**&#x200B;選項，並保存配置。
