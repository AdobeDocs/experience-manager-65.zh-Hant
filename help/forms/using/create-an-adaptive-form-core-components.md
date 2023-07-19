---
title: 如何建立最適化表單？
seo-title: Learn how to create a Core Components based Adaptive Form on AEM 6.5 Forms.
description: 瞭解如何使用建立最適化表單 [!DNL Experience Manager Forms]. 最適化Forms是回應式HTML5表單，可簡化資訊收集和處理。 深入瞭解如何根據表單資料模型和XML或JSON結構描述建立最適化表單。
seo-description: Learn how to create an Adaptive Form using [!DNL Experience Manager Forms]. Adaptive Forms are responsive HTML5 forms that streamline information gathering and processing. Dig deeper on how to create an Adaptive Form based on a Form Data Model and XML or JSON schema.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 1b97dc536550da8904bc7da09e983e0722c42a3d
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 2%

---


# 建立以核心元件為基礎的最適化Forms {#creating-an-adaptive-form-core-components}


<span class="preview"> Adobe建議使用核心元件 [將最適化Forms新增至AEM Sites頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 或 [建立獨立的最適化Forms](/help/forms/using/create-an-adaptive-form-core-components.md). </span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | 本文 |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html) |

**套用至：** ✅最適化表單核心元件❎ [最適化表單基礎元件](/help/forms/using/create-adaptive-form.md).


最適化表單可讓您建立吸引人、回應式、動態且最適化的表單。AEM Forms為商業使用者提供易於使用的UI，以便快速建立最適化Forms。 UI提供快速索引標籤導覽，以便輕鬆選取預先設定的範本、樣式、欄位和提交選項來建立調適型表單。

開始之前，請先瞭解您可用的Forms元件型別：

* [最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)：這些是標準化的資料擷取元件。 這些元件提供自訂功能、縮短開發時間，並降低數位註冊體驗的維護成本。 開發人員可以輕鬆自訂這些元件並設定其樣式。 Adobe建議運用這些現代且可擴充的元件來開發最適化Forms。

* [Adaptive Forms Foundation元件](creating-adaptive-form.md)：這些是傳統（舊）資料擷取元件。 您可以繼續使用這些專案來編輯現有的基礎元件型最適化表單。 如果您要建立表單，Adobe建議使用  [最適化Forms核心元件](/help/forms/using/create-adaptive-form.md) 以建立最適化Forms。

## 先決條件

您需要下列專案才能建立最適化表單：

* **為您的環境啟用最適化Forms核心元件**：需要AEM Archetype專案版本41或更新版本，才能 [為您的環境啟用核心元件](/help/forms/using/enable-adaptive-forms-core-components.md). 為您的環境啟用核心元件時， **最適化Forms （核心元件）** 範本和畫布主題會新增至您的環境。

* **自適應表單範本**：範本提供基本結構，並定義調適型表單的外觀（版面配置和樣式）。 它有預先格式化的元件，包含特定屬性和內容結構。 它還提供定義主題和提交動作的選項。 主題定義外觀，提交動作定義提交最適化表單時要採取的動作。

  >[!NOTE]
  >
  > 如果您沒有， **最適化Forms （核心元件）** 您環境上的範本， [為您的環境啟用最適化Forms核心元件](/help/forms/using/enable-adaptive-forms-core-components.md). 為您的環境啟用核心元件時， **最適化Forms （核心元件）** 範本已新增至您的環境。

* **最適化表單主題**：主題包含元件和面板的樣式詳細資訊。 樣式包含背景顏色、狀態顏色、透明度、對齊方式及大小等屬性。 套用主題時，指定的樣式會反映在相應的元件上。  此 `Canvas` 為您的環境啟用核心元件時，預設會新增主題。 您也可以 [下載和自訂標準主題](create-or-customize-themes-for-adaptive-forms-core-components.md).

* **許可權**：將使用者新增至 [!DNL forms-users] 群組。 的成員 [!DNL forms-users] 群組有權建立最適化表單。 如需表單特定使用者群組的詳細清單，請參閱 [群組與許可權](forms-groups-privileges-tasks.md).

## 建立最適化表單 {#create-an-adaptive-form}

1. 登入您的本機 [AEM作者執行個體](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#author-and-publish-installs).

1. 在Experience Manager登入頁面中輸入您的認證。 登入後，在左上角，點選 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.

1. 點選 **[!UICONTROL 建立]**  > **[!UICONTROL 建立最適化Forms]**.

1. 選取最適化Forms核心元件範本，然後按一下 **[!UICONTROL 下一個]**.

1. 此 **[!UICONTROL 新增屬性]** 出現。 指定下列屬性欄位的值。 「標題」和「名稱」欄位為必填欄位：

   * **[!UICONTROL 標題：]** 指定表單的顯示名稱。 標題可協助您識別 [!DNL Experience Manager Forms] 使用者介面。
   * **[!UICONTROL 名稱：]** 指定表單的名稱。 在存放庫中會建立具有指定名稱的節點。 當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議值。 名稱欄位只能包含英數字元、連字型大小和底線。
   * **[!UICONTROL 說明：]** 指定表單的詳細資訊。
   * **[!UICONTROL 主題使用者端資源庫]：** 指定最適化表單的主題。 根據預設， `adaptiveform.theme.canvas3` 已選取主題。 您也可以從以下選擇不同的主題： **[!UICONTROL 主題使用者端資源庫]** 下拉式功能表。
   * **[!UICONTROL 設定容器：]**  定義最適化Forms設定檔的儲存位置。 這些設定檔案包含與Adaptive Forms的行為和外觀相關的設定和屬性。
   * **[!UICONTROL 標籤：]** 指定可唯一識別最適化表單的標籤。 標籤有助於搜尋表單。 若要建立標籤，請在 **[!UICONTROL 標籤]** 方塊。
1. 點選 **[!UICONTROL 建立]**. 最適化表單隨即建立，並出現對話方塊以開啟表單進行編輯。


1. 點選 **[!UICONTROL 編輯]** 以在新標籤中開啟新建立的表單。 表單會開啟以進行編輯，並顯示範本中可用的內容。 它也會顯示側邊欄以自訂新建立的表單。


## 使用Adaptive Forms核心元件建立您的表單

開啟表單進行編輯後，您可以使用可用的最適化Forms核心元件將表單欄位新增至表單。 您可以拖放或使用+ [插入元件] 將這些元件新增至表單的選項。 請參閱AEM核心元件檔案，瞭解可用功能 [最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#components). 您也可以造訪 [https://aemcomponents.dev/](https://aemcomponents.dev/) 以檢視作用中的可用核心元件。

## 設定最適化表單的提交動作 {#configure-submit-action-for-form}

提交動作可讓您選擇透過最適化表單擷取的資料目的地。 當使用者按一下最適化表單上的提交按鈕時觸發。 調適型表單包含一些立即可用的提交動作。 您也可以擴充預設提交動作，以建立自己的自訂提交動作。 若要設定表單的提交動作：

1. 開啟「內容」瀏覽器，然後選取 **[!UICONTROL 參考線容器]** 最適化表單的元件。
1. 按一下指南容器屬性 ![指南屬性](/help/forms/using/assets/configure-icon.svg) 圖示。 「最適化表單容器」對話方塊開啟。

1. 按一下  **[!UICONTROL 提交]** 標籤。

   ![按一下扳手圖示以開啟最適化表單容器對話方塊，以設定提交動作](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. 選取並設定 **[!UICONTROL 提交動作]**，根據您的需求。 如需提交動作的詳細資訊，請參閱 [最適化表單提交動作](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## 將使用者重新導向至頁面或在提交表單時顯示感謝訊息

在提交表單時，您可以將使用者重新導向至其他網頁或訊息。 若要重新導向使用者或設定感謝訊息：

1. 開啟「內容」瀏覽器，然後選取 **[!UICONTROL 參考線容器]** 最適化表單的元件。
1. 按一下指南容器屬性 ![指南屬性](/help/forms/using/assets/configure-icon.svg) 圖示。 「最適化表單容器」對話方塊開啟。
1. 開啟 **[!UICONTROL 提交]** 標籤。

   ![按一下扳手圖示以開啟最適化表單容器對話方塊，以設定重新導向頁面或感謝訊息](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * 若要設定重新導向URL，請針對提交選項，選取 **[!UICONTROL 重新導向至URL]** 選項，然後瀏覽並選取AEM Sites頁面，或提供外部頁面的URL。

   * 若要設定自訂或感謝訊息，請在[提交]選項中選取 **[!UICONTROL 顯示訊息]** 選項，並在 **[!UICONTROL 訊息內容]** 方塊。 它是RTF文字方塊，您可以使用全熒幕選項來檢視所有可用的RTF專案。

## 為最適化表單設定結構描述或表單資料模型 {#configure-schema-or-data-model-for-form}

您可以使用表單資料模型將表單連線至資料來源，以根據使用者動作傳送及接收資料。 您也可以將表單連線至JSON結構描述，以預先定義的格式接收提交的資料。 根據需求，將您的表單連結至JSON結構描述或表單資料模型：

* [建立JSON結構描述並上傳至您的環境](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [建立表單資料模型](/help/forms/using/create-form-data-models.md)

### 為您的表單設定JSON結構描述或表單資料模型

若要為表單設定JSON結構描述或表單資料模型：

1. 開啟「內容」瀏覽器，然後選取 **[!UICONTROL 參考線容器]** 最適化表單的元件。
1. 按一下指南容器屬性 ![指南屬性](/help/forms/using/assets/configure-icon.svg) 圖示。 「最適化表單容器」對話方塊開啟。
1. 開啟 **[!UICONTROL 資料模型]** 標籤。

   ![按一下扳手圖示以開啟最適化表單容器對話方塊，以設定JSON結構描述或表單資料模型](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 根據您的要求，選取並設定JSON結構描述或表單資料模型：

   * 當您選取 **[!UICONTROL 表單模型]** 選項，使用 **[!UICONTROL 選取表單資料模型]** 選項以選取預先設定的表單資料模型。
   * 當您選取 **[!UICONTROL 結構描述]** 選項，使用 **[!UICONTROL 結構描述]** 選項來為您的表單選取JSON結構描述。

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!NOTE]
>
> 您可以使用指南容器屬性來編輯最適化表單的JSON結構描述或表單資料模型。

## 設定預填服務  {#configure-prefill-service-for-form}

您可以使用預填服務，以使用現有資料自動填入最適化表單的欄位。 當使用者開啟表單時，這些欄位的值會預先填充。 您可以：

* [建立自訂預填服務](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [使用表單資料模型預填服務](#fdm-prefill-service)

### 使用表單資料模型預填服務預先填入最適化表單的欄位 {#fdm-prefill-service}

您可以使用表單資料模型預填服務，透過表單資料模型或自訂預填服務預先填入最適化表單的欄位。 表單資料模型預填服務使用 [取得已設定表單資料模型的服務](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) 以擷取資料。 若要使用最適化表單的表單資料模型預填服務：

1. 開啟「內容」瀏覽器，然後選取 **[!UICONTROL 參考線容器]** 最適化表單的元件。
1. 按一下指南容器屬性 ![指南屬性](/help/forms/using/assets/configure-icon.svg) 圖示。 「最適化表單容器」對話方塊開啟。
1. 按一下最適化表單容器屬性 ![最適化表單容器屬性](/help/forms/using/assets/configure-icon.svg) 圖示。 設定資料模型的「最適化表單容器」對話方塊開啟。
   ![按一下扳手圖示以開啟最適化表單容器對話方塊，以設定重新導向頁面或感謝訊息](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. 選擇表單資料模型. 開啟 **[!UICONTROL 基本]** 標籤。 在預填服務中，選取 **[!UICONTROL 表單資料模型預填服務]**.
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。您的最適化表單現在已設定為使用表單資料模型預填。 您現在可以使用 [規則編輯器](rule-editor.md) 建立規則以預先填入表單的欄位。

<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and tap ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Tap **[!UICONTROL Save]** to save the properties.
-->

## 下一步

* [使用規則編輯器將動態行為新增至表單](rule-editor.md)
* [建立或自訂以核心元件為基礎的最適化Forms的主題](create-or-customize-themes-for-adaptive-forms-core-components.md)
* 建立以核心元件為基礎的最適化Forms範本

## 另請參閱

* [建立以Core Components為基礎的最適化表單](create-an-adaptive-form-core-components.md)
* [建立最適化表單或新增最適化表單至AEM Sites頁面或體驗片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)

