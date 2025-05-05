---
title: 如何建立最適化表單？
description: 瞭解如何使用 [!DNL Experience Manager Forms]建立最適化表單。 最適化Forms是回應式HTML5表單，可簡化資訊收集和處理。 深入瞭解如何根據表單資料模型和XML或JSON結構描述建立最適化表單。
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
solution: Experience Manager, Experience Manager Forms
exl-id: ee596672-b0b5-42e9-a139-72f90287bf3b
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1794'
ht-degree: 29%

---

# 建立以核心元件為基礎的最適化Forms {#creating-an-adaptive-form-core-components}


<span class="preview">Adobe 建議使用核心元件[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)或[建立獨立的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html) |
| AEM 6.5 | 本文 |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

最適化表單可讓您建立吸引人、回應式、動態且最適化的表單。AEM Forms提供方便企業使用者使用的UI，以便快速建立最適化Forms。 UI提供快速索引標籤導覽，以便輕鬆選取用於建立最適化表單的預先設定的範本、樣式、欄位和提交選項。

開始之前，請先了解您可以使用的表單元件類型：

* [最適化表單核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)：這些是標準化的資料擷取元件。這些元件會為您的數位註冊體驗提供自訂功能、縮短的開發時間，並降低維護成本。開發人員可以輕鬆地自訂這些元件和設計其樣式。Adobe建議使用這些現代且可擴展的元件來開發最適化Forms。

* [最適化表單基礎元件](creating-adaptive-form.md)：這些是經典 (舊) 的資料擷取元件。您可以繼續使用這些元件來編輯以現有基礎元件為主的最適化表單。如果您正在建立表單，Adobe建議使用[最適化Forms核心元件](/help/forms/using/create-adaptive-form.md)來建立最適化Forms。

## 必要條件

您必須符合以下條件才能建立最適化表單：

* **為您的環境啟用最適化Forms核心元件**：需要AEM Archetype專案版本41或更新版本，才能[為您的環境啟用核心元件](/help/forms/using/enable-adaptive-forms-core-components.md)。 為您的環境啟用核心元件時，**最適化Forms （核心元件）**&#x200B;範本和畫布主題會新增到您的環境中。

* **最適化表單範本**：此範本會提供基本結構並定義最適化表單的外觀 (版面和樣式)。其中具有包含特定屬性和內容結構的預先格式化元件。它也會提供定義主題和提交動作的選項。主題會定義外觀，而提交動作會定義提交最適化表單時要採取的動作。您也可以將[範例範本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)部署至您的環境。 這些功能可協助您快速建立表格。

  >[!NOTE]
  >
  > 如果您的環境中沒有&#x200B;**最適化表單 (核心元件)** 範本，請[為您的環境啟用最適化表單核心元件](/help/forms/using/enable-adaptive-forms-core-components.md)。為您的環境啟用核心元件後，**最適化表單 (核心元件)** 範本就會新增到您的環境中。

* **最適化表單主題**：主題包含元件和面板的樣式詳細資料。樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。套用主題時，指定的樣式會反映在對應的元件上。當您啟用環境的核心元件時，`Canvas`主題會預設新增。 您可以[下載及自訂標準佈景主題](create-or-customize-themes-for-adaptive-forms-core-components.md)。 針對&#x200B;**現成可用的佈景主題**，您可以將[範例佈景主題](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)部署至您的環境。 這些可幫助您開始設計表單的樣式，並提供基礎結構，以根據您的業務需求建立或自訂主題。

* **權限**：將您的使用者新增到 [!DNL forms-users] 群組。[!DNL forms-users] 群組的成員擁有建立最適化表單的權限。如需表單特定之使用者群組的詳細清單，請參閱[群組和權限](forms-groups-privileges-tasks.md)。

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## 建立最適化表單 {#create-an-adaptive-form}

1. 登入您的本機[AEM作者執行個體](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#author-and-publish-installs)。

1. 在 Experience Manager 登入頁面上輸入您的認證。登入後，在左上角選取&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。

1. 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 建立最適化Forms]**。

1. 選取最適化Forms核心元件範本，然後按一下「下一步&#x200B;**[!UICONTROL 」]**。

1. **[!UICONTROL 新增屬性]**&#x200B;出現。 指定下列屬性欄位的值。 「標題」和「名稱」欄位為必填欄位：

   * **[!UICONTROL 標題：]**&#x200B;指定表單的顯示名稱。 標題有助於在 [!DNL Experience Manager Forms] 使用者介面中識別表單。
   * **[!UICONTROL 名稱：]**&#x200B;指定表單的名稱。存放庫中會建立具有指定名稱的節點。您開始輸入標題時，就會自動產生名稱欄位的值。您可以變更建議的值。名稱欄位只能包含英數字元、連字型大小和底線。
   * **[!UICONTROL 描述：]**&#x200B;指定表單的詳細資訊。
   * **[!UICONTROL 主題使用者端資料庫]：**&#x200B;指定最適化表單的主題。 依預設，已選取`adaptiveform.theme.canvas3`主題。 您也可以從&#x200B;**[!UICONTROL 主題使用者端資料庫]**&#x200B;下拉式功能表中選擇不同的主題。
   * **[!UICONTROL 組態容器：]**&#x200B;定義最適化Forms組態檔的儲存位置。 這些組態檔包含與Adaptive Forms的行為和外觀相關的設定和屬性。
   * **[!UICONTROL 標籤：]**&#x200B;指定可唯一識別最適化表單的標籤。 標籤有助於搜尋表單。 若要建立標籤，請在&#x200B;**[!UICONTROL 標籤]**&#x200B;方塊中輸入新標簽名稱。
1. 選擇 **[!UICONTROL 建立]**。系統隨即建立最適化表單，並顯示對話方塊以開啟表單進行編輯。


1. 選取&#x200B;**[!UICONTROL 編輯]**&#x200B;以在新索引標籤中開啟新建立的表單。 表單會開啟以進行編輯，並顯示範本中可用的內容。 它也會顯示側邊欄以自訂新建立的表單。


## 使用最適化Forms核心元件來建立您的表單

開啟表單進行編輯後，您可以使用可用的Adaptive Forms核心元件來將表單欄位新增至表單。 您可以拖放或使用+ [插入元件]選項，將這些元件新增至表單。 請參閱AEM核心元件檔案，瞭解可用的[最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant#components)。 您也可以造訪[https://aemcomponents.dev/](https://aemcomponents.dev/)，檢視作用中的可用核心元件。

## 為最適化表單設定提交動作 {#configure-submit-action-for-form}

提交動作可讓您選擇透過最適化表單擷取的資料目的地。 當使用者按一下最適化表單上的提交按鈕時會觸發。 調適型表單包含一些立即可用的提交動作。 您也可以擴充預設提交動作，以建立自己的自訂提交動作。 若要設定表單的提交動作：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/using/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。

1. 按一下「**[!UICONTROL 提交]**」標籤。

   ![按一下扳手圖示可開啟「最適化表單容器」對話框，以設定提交動作](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. 根據您的要求選取和設定「**[!UICONTROL 提交動作]**」。如需提交動作的詳細資訊，請參閱[最適化表單提交動作](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## 將使用者重新導向至頁面，或在提交表單時顯示感謝訊息

在提交表單時，您可以將使用者重新導向至其他網頁或訊息。 若要重新導向使用者或設定感謝訊息：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/using/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 開啟&#x200B;**[!UICONTROL 提交]**&#x200B;標籤。

   ![按一下扳手圖示以開啟最適化表單容器對話方塊，以設定重新導向頁面或感謝您的訊息](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * 若要設定重新導向URL，請在[送出]選項中選取&#x200B;**[!UICONTROL 重新導向至URL]**&#x200B;選項，然後瀏覽並選取AEM Sites頁面，或提供外部頁面的URL。

   * 若要設定自訂或感謝訊息，請在[送出]選項中選取&#x200B;**[!UICONTROL 顯示訊息]**&#x200B;選項，並在&#x200B;**[!UICONTROL 訊息內容]**&#x200B;方塊中提供訊息。 它是RTF文字方塊，您可以使用全熒幕選項來檢視所有可用的RTF專案。

## 為最適化表單設定結構描述或表單資料模型 {#configure-schema-or-data-model-for-form}

您可以使用表單資料模型將表單連線至資料Source，以根據使用者動作傳送及接收資料。 您也可以將表單連線至JSON結構描述，以預先定義的格式接收提交的資料。 根據需求，將您的表單連結至JSON結構描述或表單資料模型：

* [建立JSON結構描述並上傳至您的環境](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [建立表單資料模型](/help/forms/using/create-form-data-models.md)

### 為您的表單設定JSON結構描述或表單資料模型

若要設定表單的JSON結構描述或表單資料模型：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/using/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 開啟&#x200B;**[!UICONTROL 資料模型]**&#x200B;標籤。

   ![按一下「扳手」圖示以開啟「最適化表單容器」對話方塊，設定JSON結構描述或表單資料模型](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 根據您的要求，選取並設定JSON結構描述或表單資料模型：

   * 當您選取&#x200B;**[!UICONTROL 表單模型]**&#x200B;選項時，請使用&#x200B;**[!UICONTROL 選取表單資料模型]**&#x200B;選項來選取預先設定的表單資料模型。
   * 當您選取&#x200B;**[!UICONTROL 結構描述]**&#x200B;選項時，請使用&#x200B;**[!UICONTROL 結構描述]**&#x200B;選項為您的表單選取JSON結構描述。

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!NOTE]
>
> 您可以使用指南容器屬性來編輯最適化表單的JSON結構描述或表單資料模型。

## 設定預填服務  {#configure-prefill-service-for-form}

您可以使用預填服務，使用現有資料自動填寫最適化表單的欄位。 當使用者開啟表單時，這些欄位的值將被預填。 您可以：

* [建立自訂預填服務](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [使用表單資料模型預填服務](#fdm-prefill-service)

### 使用表單資料模型預填服務預先填入最適化表單的欄位 {#fdm-prefill-service}

您可以使用表單資料模型預填服務，透過表單資料模型或自訂預填服務預先填入最適化表單的欄位。 表單資料模型預填服務使用已設定的表單資料模型[&#128279;](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services)的Get服務來擷取資料。 若要針對最適化表單使用表單資料模型預填服務：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/using/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下最適化表單容器屬性![最適化表單容器屬性](/help/forms/using/assets/configure-icon.svg)圖示。 用來設定資料模型的最適化表單容器對話方塊隨即開啟。
   ![按一下扳手圖示以開啟最適化表單容器對話方塊，以設定重新導向頁面或感謝您的訊息](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. 選取表單資料模型。 開啟&#x200B;**[!UICONTROL 基本]**&#x200B;標籤。 在預填服務中，選取&#x200B;**[!UICONTROL 表單資料模型預填服務]**。
1. 按一下&#x200B;**[!UICONTROL 完成]**。 您的最適化表單現在已設定為使用表單資料模型預填。 您現在可以使用[規則編輯器](rule-editor.md)來建立規則以預先填入表單的欄位。

## 如何重新命名AEM最適化表單？{#rename-an-AEM-Adaptive-Form}

若要重新命名最適化表單，請執行下列步驟：

1. 在您的AEM Forms使用者介面中選取最適化表單。
1. 按一下位於上方邊欄上的&#x200B;**屬性**。

   ![屬性](/help/forms/using/assets/rename-form-properties.png)

1. 變更&#x200B;**標題**&#x200B;標籤中的表單名稱，如下圖所示。
1. 按一下&#x200B;**儲存並關閉**。

   ![重新命名AEM最適化表單](/help/forms/using/assets/rename-form-title.png)


<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and select ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Select **[!UICONTROL Save]** to save the properties.
-->

## 下一步

* [使用規則編輯器將動態行為新增至表單](rule-editor.md)
* [建立或自訂核心元件型最適化Forms的主題](create-or-customize-themes-for-adaptive-forms-core-components.md)


## 另請參閱

* [建立以核心元件為基礎的最適化表單](create-an-adaptive-form-core-components.md)
* [建立最適化表單或新增最適化表單至AEM Sites頁面或體驗片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [範例主題範本和表單資料模型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
