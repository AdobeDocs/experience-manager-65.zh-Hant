---
title: 建立或新增調適型表單至 AEM Sites 頁面
description: 探索如何輕鬆建立或無縫新增調適型表單至您的 AEM Sites 頁面。 了解整合動態和可自訂表單至網站中的步驟式技術和最佳實務，最佳化您的數位體驗以達到最大影響。
Keywords: AEM Forms in sites, AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
feature: Adaptive Forms, Foundation Components
exl-id: dcf023a1-8735-48cb-b3ea-d17357eeedaf
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2884'
ht-degree: 23%

---

# 建立或新增調適型表單至 AEM Sites 頁面 {#create-or-add-an-adaptive-form-to-aem-sites-page}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | 本文章 |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html) |

透過 AEM Forms，您可以將調適型表單無縫整合到您的網頁中。 這可讓您的訪客方便填寫和提交表單，而無需離開他們所在的頁面。 這麼，他們便可毫不費力地使用網站的其他元素，同時積極與表單進行互動。

您可以使用AEM頁面編輯器快速建立多個表單並新增到您的AEM Sites頁面。 使用AEM頁面編輯器，內容作者就能利用調適型表單元件的功能（包括動態行為、驗證、資料整合、產生記錄檔案和業務流程自動化），在Sites頁面內建立順暢的資料擷取體驗。 它也可讓您使用AEM Sites頁面的各種功能，例如，版本設定、目標定位、翻譯和多網站管理員。

AEM Forms 會提供調適型表單內容和調適型表單 – 內嵌元件。 您可以使用調適型表單容器在體驗片段或AEM Sites頁面中建立表單，而調適型Forms — 內嵌元件可讓您新增現有的調適型表單或使用調適型Forms編輯器建立表單。

![網站頁面中的最適化表單](/help/forms/using/assets/adaptive-form-in-sites-page.png)

## 在AEM頁面編輯器或體驗片段中使用最適化表單容器元件的好處

在AEM頁面編輯器中使用調適型表單容器，可讓您使用調適型Forms元件的功能（包括動態行為、驗證、資料整合、產生記錄檔案和業務流程自動化），在Sites頁面中建立順暢的資料擷取體驗。 它也可讓您使用AEM Sites頁面的各種功能，例如、版本設定、目標定位、翻譯和多網站管理員，加強整體表單建立和管理體驗。 讓我們來探索其中的部分功能：

* **版本設定：** AEM Sites頁面選件 [強大的版本設定功能](/help/sites-authoring/working-with-page-versions.md)，可讓您追蹤及管理不同版本的表單。 這可讓您變更和增強表單，同時維持必要時回覆至先前版本的能力。 版本設定可確保採用受控且有條理的方式來形成開發和演化。
* **鎖定目標(與Adobe Target整合)：** 透過AEM Sites頁面鎖定目標功能，您也可以 [為不同受眾個人化表單體驗](/help/sites-administering/target.md). 透過使用使用者區段和目標定位條件，您可以針對特定使用者群組量身打造表單的內容、設計或行為。 這可讓您提供個人化和相關的表單體驗，提高參與度和轉換率。
* **翻譯：** AEM Sites [與翻譯服務緊密整合](/help/sites-administering/translation.md)，讓您輕鬆地將表單翻譯成多種語言。 此功能可簡化本地化程式，確保全球受眾可存取您的表單。 您可以在AEM翻譯專案中有效率地管理翻譯，減少支援多語言表單所需的時間與精力。 如需翻譯的詳細資訊，請參閱考量事項一節。
* **多網站管理和即時副本：** AEM Sites提供強大的 [多網站管理和即時複製功能](/help/sites-administering/msm.md)，讓您在單一環境中建立和管理多個網站。 此功能現在可讓您跨不同網站重複使用表單，確保一致性並減少重複工作。 透過集中化控制及管理，您可以有效維護及更新多個網站的表單。
* **主題：** AEM Sites頁面提供跨多個網頁設計和維護一致視覺樣式的架構。 這些會定義顏色、字型、樣式表及其他視覺元素，這些元素有助於網站的整體外觀和風格。 [您可以將為AEM Sites頁面設計的主題用於最適化表單，以節省時間和精力](/help/sites-authoring/style-system.md).
* **標籤：** AEM Sites頁面可讓您 [將標籤或標籤指派給頁面、資產或其他內容](/help/sites-authoring/tags.md). 標籤是關鍵字或中繼資料標籤，提供根據特定條件分類及組織內容的方式。 您可以指派一或多個標籤給AEM內的頁面、資產或任何其他內容專案，以改善搜尋並將資產分類。
* **鎖定和解鎖內容：** AEM Sites允許使用者 [控制對頁面的存取與修改](/help/sites-authoring/editing-content.md#locking-a-page-locking-a-page) 在AEM Sites環境中。 頁面鎖定時，即表示頁面可免受其他使用者未經授權的變更或編輯作業。 只有已鎖定內容的使用者或指定的管理員可以解除鎖定內容以允許修改。


## 在AEM頁面編輯器中新增最適化表單的各種選項

您可以通過使用以下選項來充分利用此功能：

* **[新增自訂最適化表單至AEM Sites頁面：](#create-an-adaptive-form-in-sites-editor)** 從頭開始建立全新的表單，根據您的需求和設計偏好進行量身打造。

* **[新增自訂最適化表單至體驗片段：](#create-an-adaptive-form-in-experience-fragment)** 將表單新增至AEM體驗片段，讓您的表單能夠延伸範圍，進而允許多個頁面或網站順暢地重複使用。

* **[將最適化表單轉換為體驗片段：](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)** 將新增至AEM Sites頁面的最適化表單轉換為體驗片段，以便在多個AEM Sites頁面中重複使用表單。

* **根據核准的範本建立並新增表單至AEM Sites頁面：** 運用預先核准的範本，快速建立符合貴組織品牌指導方針與設計標準的表單。 此選項僅適用於以最適化Forms編輯器或Adaptive Forms — 內嵌元件建立的最適化Forms 。

* **將現有表單新增至AEM Sites頁面：** 將您已建立的表單輕鬆整合至網站，讓訪客可直接與他們互動。 此選項僅適用於以最適化Forms編輯器或Adaptive Forms — 內嵌元件建立的最適化Forms 。

* **新增多個表單至AEM Sites頁面或體驗片段：**  新增多個表單至一個頁面，以根據使用者的偏好和需求為其提供多個選擇。 這些可以是從頭開始的全新形式和現有形式的組合。

## 考量事項 {#consideration}

* 當您使用調適型表單容器建立或新增表單時，表單會透過 AEM Sites 翻譯流程進行翻譯和本地化。 對於每種語言，系統會產生網站頁面和相應表單的個別副本 (語言副本)，當內容作者在父頁面表單中修訂規則時，表單的所有語言副本必須進行相同的變更。 最適化表單容器也可讓您使用AEM Sites頁面的各種功能，例如，版本設定、目標定位、翻譯和多網站管理員。

* 當您使用調適型表單 - 內嵌元件建立或新增表單時，表單會使用 AEM Forms 翻譯流程進行翻譯和本地化。 在這種情況下，Sites 頁面的所有語言副本中會維持和引用單一表單。 調適型表單-內嵌元件不會讓您存取 AEM Sites 頁面的各種功能，例如版本設定、目標定位、翻譯和多個網站管理員。


## 開始之前 {#before-you-start}

+++  為您的環境啟用調適型表單核心元件

確保 [為您的環境啟用最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/quick-setup/enable-headless-adaptive-forms-and-core-components.html?lang=en).

+++

+++  新增Adaptive Forms使用者端資料庫至您的AEM Sites頁面和體驗片段頁面元件

若要啟用調適型表單容器元件的完整功能，請使用部署管道將 Customheaderlibs 和 Customfooterlibs 客戶端資料庫新增至您的 AEM Sites 頁面。 若要新增資料庫：

1. 登入您的AEM Author執行個體並開啟CRX DE。 在本機執行的作者執行個體的預設URL為 `http://localhost:4502/crx/de`.

1. 開啟 `/apps/[your-sites-project]/components/page/customheaderlibs.html` 將下列程式碼新增至檔案中：

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. 開啟 `/apps/[your-sites-project]/components/page/customfooterlibs.html` 將下列程式碼新增至檔案中：

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. 開啟 `/apps/[your-sites-project]/components/xfpage/customheaderlibs.html` 將下列程式碼新增至檔案中：

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. 開啟 `/apps/[your-sites-project]/components/customfooterlibs.html` 將下列程式碼新增至檔案中：

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. 在您的環境中重複上述所有製作和發佈執行個體的步驟。

+++

+++ 啟用最適化Forms容器

若要啟用範本原則中的[!UICONTROL 調適型表單容器]元件，需執行以下步驟：

1. 開啟AEM Sites頁面或體驗片段進行編輯。 若要開啟頁面進行編輯，請選擇該頁面，然後按一下「編輯」。
1. 開啟網站或體驗片段頁面的範本。 若要開啟範本，前往[!UICONTROL 頁面資訊] ![頁面資訊](/help/forms/using/assets/Smock_Properties_18_N.svg)>[!UICONTROL 編輯範本]。 它會在範本編輯器中開啟對應的範本。
1. 在「結構」視圖中，在選單列中按一下&#x200B;**[!UICONTROL 「原則」]**![「原則」](/help/forms/using/assets/Smock_FeedManagement_18_N.svg)圖示。 在「**[!UICONTROL 允許的元件]**」清單中，選取「**[!UICONTROL 調適型表單容器]**」的勾選方格 (在 **[AEM 原型專案名稱] - 調適型表單**&#x200B;下方)。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## 建立最適化表單 {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

您可以直接在AEM Sites頁面或體驗片段中，從頭開始建立全新的表單，根據您的需求和設計偏好設定進行量身打造。 對於單次使用的表單，建議直接編寫到AEM Sites頁面，而體驗片段則適用於需要在您網站上的多個頁面中重複使用的表單。

* [在 AEM Sites 頁面建立表單](#create-an-adaptive-form-in-sites-editor)
* [在體驗片段中建立表單](#create-an-adaptive-form-in-experience-fragment)
* [將AEM Sites頁面中的自適應表單轉換為體驗片段](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### 在 AEM Sites 頁面建立表單 {#create-an-adaptive-form-in-sites-editor}

您可以使用AEM頁面編輯器中的調適型表單容器元件來建立自訂表單。 元件可讓您拖放表單元件來建立表單。 表單元件是以核心元件為主。 您可以根據組織的要求輕鬆自訂這一些。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

若要在 Sites 頁面建立調適型表單：

1. 在編輯模式中開啟 AEM Sites 頁面。
1. 將&#x200B;**[!UICONTROL 調適型表單容器]**&#x200B;元件從元件瀏覽器拖放至 Sites 頁面。 這樣可在頁面上為表單建立一個空間。 您可以使用版面模式來變更容器空間的大小。
1. 將調適型表單核心拖放至容器空間，以便建立表單。
1. 新增「提交」按鈕。

接下來，您 [設定提交動作](#configure-submit-action-for-form) 和進階屬性。

### 在體驗片段中建立表單 {#create-an-adaptive-form-in-experience-fragment}

您可以新增表單至 AEM 體驗片段來擴展表單的範圍，如此可跨多個頁面或多個網站進行無縫的重複使用。 例如，您可以在體驗片段中包含時事通訊註冊表單。這可讓您方便地在網站的多個頁面中重複使用片段，而無需重複重新建立表單。 在體驗片段內對電子報登錄檔單所做的任何更新或修改都會自動傳播到所有使用它的頁面。 這簡化了流程並確保無縫的用戶體驗，同時簡化了網站表單的管理。

若要在體驗片段中建立調適型表單：

1. 開啟體驗片段。
1. 拖放 **[!UICONTROL 最適化Forms容器]** 元件從元件瀏覽器移至體驗片段。
1. 將最適化表單核心元件拖放至體驗片段中的容器空間來建立表單。
1. 新增「提交」按鈕。

接下來，您 [設定提交動作](#configure-submit-action-for-form) 和進階屬性。

### 將AEM Sites頁面中的自適應表單轉換為體驗片段 {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

您可以將網站頁面編輯器中的現有最適化表單轉換為體驗片段，以跨多個頁面或網站重複使用表單。

若要將AEM Sites頁面中的最適化表單轉換為體驗片段：

1. 在編輯模式中開啟包含調適型表單的AEM Sites頁面(在調適型Forms容器元件中)。
1. 開啟「內容樹」，然後選取 **[!UICONTROL 最適化Forms容器]** 託管您的最適化表單。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。
1. 在功能表列上，選取 ![「轉換為體驗片段變數」圖示](/help/forms/using/assets/Smock_FilingCabinet_18_N.svg) 「轉換為體驗片段變數」圖示。
   ![將網站頁面中的表單轉換為體驗片段](/help/forms/using/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   會出現對話方塊，將最適化表單容器轉換為新的體驗片段或新增到現有的體驗片段
1. 在轉換為體驗片段變數對話方塊中，設定以下選項的值：

   * **動作：** 選取以建立體驗片段或新增到現有的體驗片段。
   * **父路徑：** 指定要託管體驗片段的資料夾路徑。 選項僅適用於建立體驗片段。
   * **範本：** 指定體驗片段範本的路徑。 如果您沒有體驗片段範本， [建立它](/help/sites-developing/experience-fragments.md). 該選項僅可用於將最適化表單新增到現有的體驗片段。
   * **片段標題：** 指定體驗片段的標題。 標題可唯一識別體驗片段


## 設定表單的提交動作 {#configure-submit-action-for-form}

提交動作可讓您選擇透過最適化表單擷取的資料目的地。 當使用者按一下最適化表單上的提交按鈕時會觸發。 調適型表單包含一些立即可用的提交動作。 您也可以擴充預設提交動作，以建立自己的自訂提交動作。 若要設定表單的提交動作：

1. 開啟包含最適化表單的AEM頁面編輯器或體驗片段。
1. 開啟「內容樹」，然後選取 **[!UICONTROL 最適化Forms容器]** 託管您的最適化表單。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。
1. 按一下最適化表單容器屬性 ![最適化表單容器屬性](/help/forms/using/assets/configure-icon.svg) 圖示。 可設定提交動作的調適型表單容器對話方塊隨即開啟。
   ![調適型表單容器](/help/forms/using/assets/adaptive-forms-container.png)
1. 根據您的要求，選取並設定提交動作。 如需「提交動作」的詳細資訊，請參閱 [最適化表單提交動作](configuring-submit-actions.md)


## 設定表單的結構描述或表單資料模型 {#configure-schema-or-data-model-for-form}

您可以使用表單資料模型將表單連線至資料來源，以根據使用者動作傳送及接收資料。 您也可以將表單連線至JSON結構描述，以預先定義的格式接收提交的資料。

將表單連線至結構描述或表單資料模型之前

* [建立JSON結構描述並上傳至您的環境](adaptive-form-json-schema-form-model.md)
* [建立表單資料模型](create-form-data-models.md)

若要設定表單的JSON結構描述或表單資料模型：

1. 開啟包含最適化表單的AEM頁面編輯器或體驗片段。
1. 開啟「內容樹」，然後選取 **[!UICONTROL 最適化Forms容器]** 託管您的最適化表單。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。
1. 按一下最適化表單容器屬性 ![最適化表單容器屬性](/help/forms/using/assets/configure-icon.svg) 圖示。 用來設定資料模型的最適化表單容器對話方塊隨即開啟。
   ![表單資料模型最適化表單容器](/help/forms/using/assets/form-data-model-adaptive-forms-container.png)
1. 根據您的要求，選取並設定JSON結構描述或表單資料模型。 如需「提交動作」的詳細資訊，請參閱 [最適化表單提交動作](configuring-submit-actions.md).

   * 當您選取 **[!UICONTROL 表單模型]** 選項，使用 **[!UICONTROL 選取表單資料模型]** 選項以選取預先設定的表單資料模型。
   * 當您選取 **[!UICONTROL 結構描述]** 選項，使用 **[!UICONTROL 結構描述]** 選項來為您的表單選取JSON結構描述。

1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

## 設定表單的預填服務 {#configure-prefill-service-for-form}

您可以使用預填服務，使用現有資料自動填寫最適化表單的欄位。 當使用者開啟表單時，這些欄位的值將被預填。 您可以：

* [建立自訂預填服務](prepopulate-adaptive-form-fields.md)
* [使用表單資料模型預填服務](#fdm-prefill-service)

### 使用表單資料模型預填服務 {#fdm-prefill-service}

您可以使用表單資料模型預填服務，使用已設定的表單資料模型預填表單的欄位。 表單資料模型預填服務使用 [取得已設定表單資料模型的服務](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) 以擷取資料。 若要針對最適化表單使用表單資料模型預填服務：

1. 開啟包含最適化表單的AEM頁面編輯器或體驗片段。
1. 開啟「內容樹」，然後選取 **[!UICONTROL 最適化Forms容器]** 託管您的最適化表單。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。
1. 按一下最適化表單容器屬性 ![最適化表單容器屬性](/help/forms/using/assets/configure-icon.svg) 圖示。 用來設定資料模型的最適化表單容器對話方塊隨即開啟。
   ![預填服務fdm aem sites頁面編輯器](/help/forms/using/assets/prefill-service-fdm-aem-sites-page-editor.png)
1. 選取表單資料模型。 開啟 **[!UICONTROL 基本]** 標籤。 在預填服務中，選取 **[!UICONTROL Forms入口網站草稿預填服務]**.
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

## 在表單提交時將使用者重新導向至新使用者，或顯示感謝訊息

在提交表單時，您可以將使用者重新導向至其他網頁或訊息。 若要重新導向使用者或設定感謝訊息：

1. 開啟包含最適化表單的AEM頁面編輯器或體驗片段。
1. 開啟「內容樹」，然後選取 **[!UICONTROL 最適化Forms容器]** 託管您的最適化表單。 一個AEM Sites頁面可以託管多個最適化Forms。 因此，請仔細選取正確的最適化Forms容器。
1. 按一下最適化表單容器屬性 ![最適化表單容器屬性](/help/forms/using/assets/configure-icon.svg) 圖示。 用來設定資料模型的最適化表單容器對話方塊隨即開啟。
1. 開啟 **[!UICONTROL 提交]** 標籤。

   * 若要設定重新導向URL，請針對送出選項，選取重新導向至URL選項，並提供絕對位址、重新導向URL或AEM Sites頁面的相對路徑。

   * 若要設定自訂或感謝訊息，請在[送出]選項中選取[顯示訊息]選項，然後在[訊息內容]方塊中提供訊息。 它是RTF文字方塊，您可以使用全熒幕選項來檢視所有可用的RTF專案。

## 另請參閱 {#see-also}

* [建立獨立的以核心元件為主的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)
* [為您的表單建立樣式或主題](/help/forms/using/create-or-customize-themes-for-adaptive-forms-core-components.md)
