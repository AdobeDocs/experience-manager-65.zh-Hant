---
title: 如何建立最適化表單
description: 瞭解如何使用建立最適化表單 [!DNL Experience Manager Forms]. 調適型表單是回應式HTML5表單，可簡化資訊收集和處理。 深入瞭解如何根據表單資料模型、XFA表單範本及XML或JSON結構描述建立最適化表單。
role: User, Developer
level: Beginner
feature: Adaptive Forms, Foundation Components
exl-id: 2c25a8b7-73f7-40fb-a303-9446a708c8eb
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1923'
ht-degree: 9%

---

# 建立最適化表單 {#creating-an-adaptive-form}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html) |
| AEM 6.5 | 本文章 |

## 建立最適化表單 {#strong-create-an-adaptive-form-strong}

請依照下列步驟建立最適化表單。

1. 存取 [!DNL Experience Manager Forms] 作者執行個體在 `https://'[server]:[port]'/<custom-context-if-any>.`

1. 在 Experience Manager 登入頁面上輸入您的認證。

   登入後，在左上角選取「 」 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.

   >[!NOTE]
   >
   >對於預設安裝，登入為 `admin` 密碼是 `admin`.

1. 選取 **[!UICONTROL 建立]** 並選取 **[!UICONTROL 最適化表單]**.
1. 隨即顯示選取範本的選項。 如需範本的詳細資訊，請參閱 [最適化表單範本](creating-adaptive-form.md#p-adaptive-form-templates-p). 選取要選取的範本，然後選取「下一步」。
1. 「新增屬性」的選項隨即顯示。 指定下列屬性欄位的值。 「標題」和「名稱」欄位為必填欄位：

   * **[!UICONTROL 標題：]** 指定表單的顯示名稱。 標題有助於在 [!DNL Experience Manager Forms] 使用者介面中識別表單。
   * **[!UICONTROL 名稱：]**&#x200B;指定表單的名稱。存放庫中會建立具有指定名稱的節點。您開始輸入標題時，就會自動產生名稱欄位的值。您可以變更建議的值。名稱欄位只能包含字母數字字元、連字號和底線。所有無效的輸入都會以連字號取代。
   * **[!UICONTROL 說明：]** 指定表單的詳細資訊。
   * **[!UICONTROL 標籤：]** 指定可唯一識別最適化表單的標籤。 標籤有助於搜尋表單。 若要建立標籤，請在 **[!UICONTROL 標籤]** 方塊。

1. 您可以根據下列其中一個表單模型建立最適化表單：

   * [表單資料模型](#fdm)
   * [XFA表單範本](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [xml或JSON結構描述](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * 無或不含任何表單模型

   您可從以下位置設定這些許可權： **[!UICONTROL 表單模型]** 標籤上的 **[!UICONTROL 新增屬性]** 頁面。 依預設，選取的表單模型為 **[!UICONTROL 無]**.

1. 選擇 **[!UICONTROL 建立]**。系統隨即建立最適化表單，並顯示對話方塊以開啟表單進行編輯。

   指定完所有屬性後，按一下 **[!UICONTROL 建立]**. 系統隨即建立最適化表單，並顯示對話方塊以開啟表單進行編輯。

   指定完所有屬性後，按一下 **[!UICONTROL 建立]**. 系統隨即建立最適化表單，並顯示對話方塊以開啟表單進行編輯。

1. 選取 **[!UICONTROL 開啟]** 以在新標籤中開啟新建立的表單。 表單會開啟以進行編輯，並顯示範本中可用的內容。 也會顯示側邊欄，以便您根據需求自訂新建立的表單。

   根據最適化表單的型別，相關XFA表單範本、XML結構描述或JSON結構描述中存在的表單元素會顯示在 **[!UICONTROL 資料模型物件]** 的標籤 **[!UICONTROL 內容瀏覽器]** 在側邊欄中。 您也可以拖放這些元素來建置最適化表單。

   如需關於最適化表單製作介面和可用元件的資訊，請參閱 [製作調適型表單簡介](introduction-forms-authoring.md).

   >[!NOTE]
   >
   >允許瀏覽器中的快顯視窗，以在新索引標籤中開啟新建立的表單。

## 根據表單資料模型建立最適化表單 {#fdm}

[[!DNL Experience Manager Forms] 資料整合](data-integration.md) 可讓您整合多個資料來源，並將其實體和服務整合在一起，以建立表單資料模型。 這是JSON結構描述的擴充功能。 您可以使用表單資料模型來建立最適化表單。 在表單資料模型中設定的實體或資料模型物件，可作為用於表單製作的資料模型物件。 它們會繫結至各自的資料來源，並用於預先填入表單及將提交的資料寫入回各自的資料來源。 您也可以使用最適化表單規則，呼叫在表單資料模型中設定的服務。

若要使用表單資料模型來建立最適化表單：

1. 在新增屬性畫面的表單模型索引標籤中，選取 **[!UICONTROL 表單資料模型]** 在 **[!UICONTROL 選取自]** 下拉式清單。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 選取以展開 **[!UICONTROL 選取表單資料模型]**. 列出所有可用的表單資料模型。

   從資料模型中選取。

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>您也可以變更最適化表單的表單資料模型。 如需詳細步驟，請參閱 [編輯最適化表單的表單模型屬性](#edit-form-model).

## 根據XFA表單範本建立最適化表單 {#create-an-adaptive-form-based-on-an-xfa-form-template}

您可以重新利用XFA表單範本來建立最適化表單。 若要重新調整用途，請上傳XFA表單範本並將其與調適型表單建立關聯。 表單範本（XFA表單）的元素可在最適化表單製作時用於內容尋找器。 從「內容尋找器」中，您可以將表單範本元素拖放至表單上。

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

## 根據XML或JSON結構描述建立調適型表單 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML和JSON結構描述代表組織中後端系統產生或使用資料的結構。 您可以將結構描述關聯至最適化表單，並使用其元素將動態內容新增至最適化表單。 結構描述的元素可在內容瀏覽器的「資料模型物件」標籤中使用，以編寫調適型表單。 您可以拖放結構元素來建置表單。

請參閱以下檔案以瞭解如何為製作調適型表單設計XML或JSON結構描述。

* [使用XML結構描述建立調適型表單](adaptive-form-xml-schema-form-model.md)
* [使用JSON結構描述建立調適型表單](adaptive-form-json-schema-form-model.md)

若要使用XML或JSON結構描述作為調適型表單的表單模型，請執行下列動作：

1. 在 **[!UICONTROL 新增屬性]** 最適化表單建立頁面的步驟，選擇在 **[!UICONTROL 表單模型]** 標籤。
1. 在「表單模型」標籤中，選取 **[!UICONTROL 結構描述]** 從 **[!UICONTROL 選取自]** 下拉式欄位。

1. 選取 **[!UICONTROL 選取結構描述]** 並執行下列任一項作業：

   * **[!UICONTROL 從磁碟上傳]**  — 選取此選項並選取「上傳結構描述定義」，從您的檔案系統瀏覽並上傳XML結構描述或JSON結構描述。 上傳的結構描述檔案位於表單中，其他最適化表單無法存取。
   * **[!UICONTROL 在存放庫中搜尋]**  — 選取此選項，從存放庫中可用的結構描述定義檔案清單中選取。 選取XML或JSON結構描述檔案作為表單模型。 選取的結構描述會參照表單與之關聯，且可供其他最適化表單使用。

   >[!CAUTION]
   >
   >請確定JSON結構描述檔案名稱結尾為 **.schema.json**. 例如： mySchema.schema.json

   ![選取XML或JSON結構描述](assets/upload-schema.png)
   **圖：** *選取XML或JSON結構描述*

1. （僅適用於XML綱要）選取或上傳XML綱要後，請指定所選XSD檔案的根元素，以對應至最適化表單。

   ![選取XSD根元素](assets/xsd-root-element.png)
   **圖：** *選取XSD根元素*

>[!NOTE]
>
>您也可以變更最適化表單的結構描述。 如需詳細步驟，請參閱 [編輯最適化表單的表單模型屬性](#edit-form-model).

## 最適化表單範本 {#adaptive-form-templates}

範本提供基本結構，並定義最適化表單的外觀（版面配置和樣式）。 它有預先格式化的元件，其中包含特定屬性和內容結構。 <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

此外，您可以使用範本編輯器建立自己的範本。 如需使用範本的詳細資訊，請參閱 [最適化表單範本](template-editor.md).

>[!NOTE]
>
>當您開啟使用進階範本建立的最適化表單進行編輯時，會出現一則錯誤訊息。 進階範本有「簽名步驟」元件，並且預設會為其啟用Adobe Sign。 建立並選取 [Adobe Sign雲端設定](adobe-sign-integration-adaptive-forms.md) 和 [設定簽署者](working-with-adobe-sign.md#addsignerstoanadaptiveform) 以解決錯誤。

## 編輯最適化表單的表單模型屬性 {#edit-form-model}

最適化表單的建立不需要表單模型（對表單模型使用「無」選項），或使用表單模型，例如表單範本、XML結構描述或JSON結構描述或表單資料模型。 您可以將最適化表單的表單模型從無變更為其他表單模型。 對於根據表單模型的最適化表單，您可以為相同表單模型選擇其他表單範本、XML結構描述、JSON結構描述或表單資料模型。 不過，您無法在不同表單模型之間變更。

1. 選取最適化表單並選取 **屬性** 圖示。
1. 開啟「**[!UICONTROL 表單模型]**」標籤，並執行以下其中一項操作。

   * 如果調適型表單沒有表單模型，您可以選擇另一個表單模型，並據此選擇表單範本、XML或JSON結構描述或表單資料模型。
   * 如果最適化表單是以表單模型為基礎，您可以為相同表單模型選擇其他表單範本、XML或JSON結構描述或表單資料模型。

1. 選取 **[!UICONTROL 儲存]** 以儲存屬性。

## 自動儲存最適化表單 {#auto-save-an-adaptive-form}

依預設，最適化表單的內容會在使用者動作時儲存，例如按下「儲存」按鈕時。 您也可以設定最適化表單，以根據事件或時間間隔自動開始儲存內容。 自動儲存選項非常實用：

* 自動為匿名和登入的使用者儲存內容
* 儲存表單內容而不需要使用者介入或使用者介入很小
* 開始根據使用者事件儲存表單內容
* 在指定的時間間隔後重複儲存表單內容

### 為最適化表單啟用自動儲存 {#enable-auto-save-for-an-adaptive-form}

預設不會啟用自動儲存選項。 您可以從最適化表單的「自動儲存」標籤啟用自動儲存選項。 「自動儲存」標籤也提供幾個其他組態選項。 執行以下步驟，為最適化表單啟用並設定自動儲存選項：

1. 若要存取屬性中的自動儲存區段，請選取元件，然後選取 ![欄位層級](assets/field-level.png) > **[!UICONTROL 最適化表單容器]**，然後選取 ![cmppr](assets/cmppr.png).
1. 在 **[!UICONTROL 自動儲存]** 部分， **[!UICONTROL 啟用]** 自動儲存選項。
1. 在 **[!UICONTROL 最適化表單事件]** 方塊中，指定1或TRUE會在表單載入瀏覽器時自動開始儲存表單。 您也可以為事件指定條件運算式，觸發並傳回true時，此運算式就會開始儲存表單的內容。
1. 指定觸發器。 系統會根據您的設定觸發自動儲存。 您的選項有：

   * **[!UICONTROL 基於時間：]** 選取選項，以根據特定時間間隔開始儲存內容。
   * **[!UICONTROL 以事件為基礎：]** 選取選項，以便在觸發事件時開始儲存內容。

   當您選取觸發器時，會啟用「策略組態」方塊。 策略設定方塊可讓您：

   * 如果選取，請指定時間間隔 **[!UICONTROL 基於時間]** 觸發器。
   * 如果您選取「 」，請指定事件名稱 **[!UICONTROL 基於事件]** 觸發器。

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. （僅限以時間為基礎的自動儲存）執行下列步驟，設定「以時間為基礎的自動儲存」選項。

   1. 在 **[!UICONTROL 在此間隔自動儲存]** 方塊，以秒為單位指定時間間隔。 表單會在間隔方塊中指定的秒數過後重複儲存。

1. （僅限事件式自動儲存）執行下列步驟，設定事件式自動儲存的選項。

   1. 在 **[!UICONTROL 在此事件後自動儲存]** 方塊，指定 [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 事件。 每次運算式評估為TRUE時，都會儲存表單。

1. （選用）若要自動為匿名使用者儲存內容，請選取 **[!UICONTROL 啟用匿名使用者的自動儲存]** 選項，然後按一下 **[!UICONTROL 確定]**.

   >[!NOTE]
   >
   >若要讓自動儲存選項適用於匿名使用者，請務必將Forms通用設定服務設定為允許所有使用者預覽、驗證及簽署表單。
   >
   >若要設定服務，請前往Adobe Experience Manager Web Console設定，位於 `https://'[server]:[port]'system/console/configMgr` 並編輯 **[!UICONTROL Forms通用設定服務]** 以選擇 **[!UICONTROL 所有使用者]** 中的選項 **[!UICONTROL 允許]** 欄位並儲存設定。
