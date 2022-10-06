---
title: 使用表單資料模型
seo-title: Use form data model
description: 了解如何使用表單資料模型來建立及使用最適化表單和互動式通訊。
seo-description: Learn how to use form data model to create and work with adaptive forms and interactive communications.
uuid: 9d8d8f43-9a50-4905-a6ef-a5ea3b9c11f7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 87f5f9f5-2d03-4565-830e-eacc3757e542
docset: aem65
feature: Form Data Model
exl-id: 9a73a643-7ad4-49aa-a971-08d52679158d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 0%

---

# 使用表單資料模型{#use-form-data-model}

![](do-not-localize/data-integeration.png)

AEM Forms資料整合可讓您使用不同的後端資料來源來建立表單資料模型，以便在各種最適化表單和互動式通訊工作流程中當作結構描述。 它需要配置資料源，並根據資料源中可用的資料模型對象和服務建立表單資料模型。 如需詳細資訊，請參閱下列內容：

* [AEM Forms資料整合](../../forms/using/data-integration.md)
* [設定資料來源](../../forms/using/configure-data-sources.md)
* [建立表單資料模型](../../forms/using/create-form-data-models.md)
* [使用表單資料模型](../../forms/using/work-with-form-data-model.md)

表單資料模型是JSON結構描述的擴充功能，可用於：

* [建立最適化表單和片段](#create-af)
* [建立互動式通訊和建置區塊，例如文字、清單和條件片段](#create-ic)
* [使用範例資料預覽互動式通訊](#preview-ic)
* [預填最適化表單和互動式通訊](#prefill)
* [將提交的最適化表單資料寫入資料來源](#write-af)
* [使用最適化表單規則叫用服務](#invoke-services)

## 建立最適化表單和片段 {#create-af}

您可以建立 [適用性表單](../../forms/using/creating-adaptive-form.md) 和 [適用性表單片段](../../forms/using/adaptive-form-fragments.md) 根據表單資料模型。 建立最適化表單或最適化表單片段時，請執行下列動作以使用表單資料模型：

1. 在「添加屬性」螢幕上的「表單模型」頁簽中，選擇 **[!UICONTROL 表單資料模型]** 在 **[!UICONTROL 從]** 下拉式清單。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 點選以展開 **[!UICONTROL 選擇表單資料模型]**. 會列出所有可用的表單資料模型。

   從資料模型中選取。

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**僅適用性表單片段**)您可以僅根據表單資料模型中的一個資料模型物件，建立最適化表單片段。 展開 **[!UICONTROL 表單資料模型定義]** 下拉式清單。 它列出指定表單資料模型中的所有資料模型對象。 從清單中選取資料模型物件。

   ![create-af-3](assets/create-af-3.png)

建立以表單資料模型為基礎的最適化表單或最適化表單片段後，表單資料模型物件會出現在 **[!UICONTROL 資料模型物件]** 內容瀏覽器的索引標籤。

>[!NOTE]
>
>對於最適化表單片段，只有在創作時選取的資料模型物件及其相關的資料模型物件會顯示在「資料模型物件」索引標籤中。

![data-model-objects-tab](assets/data-model-objects-tab.png)

您可以將資料模型物件拖放至最適化表單或片段，以新增表單欄位。 新增的表單欄位會保留中繼資料屬性，並與資料模型物件屬性系結。 系結可確保表單提交時欄位值會在對應的資料來源中更新，並在表單轉譯時預填。

## 建立互動式通訊 {#create-ic}

您可以根據表單資料模型建立互動式通訊，以便使用來自已設定資料來源的資料預先填入互動式通訊。 此外，互動式通信的構建模組（如文本、清單和條件文檔片段）可以基於表單資料模型。

建立互動式通訊或檔案片段時，您可以選擇表單資料模型。 下圖顯示了「建立交互通信」對話框的「常規」頁簽。

![create-ic](assets/create-ic.png)

「建立互動式通信」對話框的「常規」頁簽

如需詳細資訊，請參閱：

[建立互動式通訊](../../forms/using/create-interactive-communication.md)

[互動式通訊中的文字](/help/forms/using/texts-interactive-communications.md)

[互動式通訊中的條件](/help/forms/using/conditions-interactive-communications.md)

[清單片段](/help/forms/using/lists.md)

## 使用範例資料預覽 {#preview-ic}

表單資料模型編輯器可讓您為表單資料模型中的資料模型物件產生和編輯範例資料。 您可以使用此資料來預覽和測試互動式通訊和最適化表單。 您必須先產生範例資料，才能依照 [使用表單資料模型](../../forms/using/work-with-form-data-model.md#sample).

若要預覽與範例表單資料模型資料的互動式通訊：

1. 在AEM製作例項上，導覽至 **[!UICONTROL Forms > Forms與檔案]**.
1. 選取互動式通訊並點選 **[!UICONTROL 預覽]** ，以選取 **[!UICONTROL Web頻道]**, **[!UICONTROL 列印管道]**，或 **[!UICONTROL 兩個管道]** 預覽互動式通訊。
1. 在預覽中 [*頻道*] 對話，確保 **[!UICONTROL 表單資料模型的測試資料]** 已選取並點選 **[!UICONTROL 預覽]**.

互動式通訊隨即開啟，其中包含預填的範例資料。

![網頁預覽](assets/web-preview.png)

同樣地，若要預覽包含範例資料的最適化表單，請在製作模式中開啟最適化表單，然後點選 **[!UICONTROL 預覽]**.

## 使用表單資料模型服務預填 {#prefill}

AEM Forms提供現成可用的表單資料模型預填服務，讓您能夠根據表單資料模型啟用最適化表單和互動式通訊。 預填充服務以自適應形式和交互通信查詢資料模型對象的資料源，並相應地在呈現表單或通信時預填充資料。

若要為最適化表單啟用「表單資料模型預填服務」，請開啟「最適化表單容器」屬性並選取 **[!UICONTROL 表單資料模型預填服務]** 從 **[!UICONTROL 預填服務]** 「基本」設定追蹤器中的下拉式清單。 然後，儲存屬性。

![預填服務](assets/prefill-service.png)

若要在互動式通訊中設定表單資料模型預填服務，您可以在建立預填服務下拉式清單中選取「表單資料模型預填服務」，或之後透過修改屬性來建立預填服務。

![edit-ic-props](assets/edit-ic-props.png)

編輯互動式通信的屬性對話框

## 將提交的最適化表單資料寫入資料來源 {#write-af}

當使用者根據表單資料模型提交表單時，您可以設定表單以將資料模型物件的已提交資料寫入其資料來源。 為達成此使用案例，AEM Forms提供 [表單資料模型提交動作](../../forms/using/configuring-submit-actions.md)，現成可供根據表單資料模型適用的最適化表單使用。 它會將資料模型物件的已提交資料寫入其資料來源中。

若要設定「表單資料模型提交」動作，請開啟「最適化表單容器」屬性並選取 **[!UICONTROL 使用表單資料模型提交]** 從「提交」設定追蹤器下的「提交動作」下拉式清單。 然後，瀏覽並選取資料模型物件， **[!UICONTROL 要提交的資料模型對象的名稱]** 下拉式清單。 儲存屬性。

在表單提交時，將配置的資料模型對象的資料寫入相應的資料源。

![資料提交](assets/data-submission.png)

您也可以使用二進位資料模型物件屬性，將表單附件提交至資料來源。 執行以下操作將附件提交到JDBC資料源：

1. 將包含二進位屬性的資料模型物件新增至表單資料模型。
1. 在最適化表單中，拖放 **[!UICONTROL 檔案附件]** 元件（從「元件」瀏覽器）上的元件移至最適化表單。
1. 點選以選取新增的元件，然後點選 ![settings_icon](assets/settings_icon.png) 開啟元件的「屬性」瀏覽器。
1. 在「系結參考」欄位中，點選 ![foldersearch_18](assets/foldersearch_18.png) 並導覽至選取您在表單資料模型中新增的二進位屬性。 視需要設定其他屬性。

   點選 ![check-button](assets/check-button.png) 以儲存屬性。 附件欄位現在已綁定到表單資料模型的二進位屬性。

1. 在適用性表單容器屬性的「提交」區段中，啟用 **[!UICONTROL 提交表單附件]**. 它會在提交表單時將二進位屬性欄位中的附件提交給資料來源。

## 使用規則叫用適用性表單中的服務 {#invoke-services}

在以表單資料模型為基礎的最適化表單中，您可以 [建立規則](../../forms/using/rule-editor.md) 調用在表單資料模型中配置的服務。 此 **[!UICONTROL 調用服務]** 規則中的操作列出表單資料模型中的所有可用服務，並允許您為服務選擇輸入和輸出欄位。 您也可以使用 **設定值** 規則類型，以叫用表單資料模型服務，並將欄位的值設為服務傳回的輸出。

例如，以下規則調用以員工ID作為輸入的獲取服務，並且返回的值將填充到窗體中相應的「從屬ID」、「姓氏」、「名字」和「性別」欄位中。

![調用服務](assets/invoke-service.png)

此外，您也可以使用 `guidelib.dataIntegrationUtils.executeOperation` 在規則編輯器的程式碼編輯器中撰寫JavaScript的API。 如需API詳細資訊，請參閱 [調用表單資料模型服務的API](/help/forms/using/invoke-form-data-model-services.md).
