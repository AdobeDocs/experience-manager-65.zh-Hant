---
title: 使用表單資料模型
seo-title: 使用表單資料模型
description: 瞭解如何使用表單資料模型來建立並使用最適化表單和互動式通訊。
seo-description: 瞭解如何使用表單資料模型來建立並使用最適化表單和互動式通訊。
uuid: 9d8d8f43-9a50-4905-a6ef-a5ea3b9c11f7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 87f5f9f5-2d03-4565-830e-eacc3757e542
docset: aem65
feature: 表單資料模型
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---


# 使用表單資料模型{#use-form-data-model}

![](do-not-localize/data-integeration.png)

AEM Forms資料整合可讓您使用分散的後端資料來源來建立表單資料模型，以便在各種調適性表單和互動式通訊工作流程中當做架構使用。 它需要設定資料來源，並根據資料來源中可用的資料模型物件和服務來建立表單資料模型。 如需詳細資訊，請參閱下列：

* [AEM Forms資料整合](../../forms/using/data-integration.md)
* [設定資料來源](../../forms/using/configure-data-sources.md)
* [建立表單資料模型](../../forms/using/create-form-data-models.md)
* [使用表單資料模型](../../forms/using/work-with-form-data-model.md)

表單資料模型是JSON結構描述的擴充功能，您可用來：

* [建立最適化表單和片段](#create-af)
* [建立互動式通訊和建立區塊，例如文字、清單和條件片段](#create-ic)
* [使用範例資料預覽互動式通訊](#preview-ic)
* [預先填寫最適化表單和互動式通訊](#prefill)
* [將提交的自適應表單資料寫回資料來源](#write-af)
* [使用自適應表單規則叫用服務](#invoke-services)

## 建立最適化表單和片段{#create-af}

您可以根據表單資料模型建立[自適應表單](../../forms/using/creating-adaptive-form.md)和[自適應表單片段](../../forms/using/adaptive-form-fragments.md)。 在建立自適應表單或自適應表單片段時，請執行以下操作以使用表單資料模型：

1. 在「添加屬性」螢幕的「表單模型」頁籤中，從&#x200B;**[!UICONTROL 從]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL 表單資料模型]**。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 點選以展開&#x200B;**[!UICONTROL 選擇表單資料模型]**。 列出所有可用的表單資料模型。

   從資料模型中選擇。

   ![create-af-2-1](assets/create-af-2-1.png)

1. （**僅適應性表單片段**）您可以基於表單資料模型中的一個資料模型對象建立自適應性表單片段。 展開&#x200B;**[!UICONTROL 表單資料模型定義]**&#x200B;下拉式清單。 它列出指定表單資料模型中的所有資料模型對象。 從清單中選擇一個資料模型對象。

   ![create-af-3](assets/create-af-3.png)

一旦基於表單資料模型建立了自適應表單或自適應表單片段，表單資料模型對象將以自適應表單編輯器顯示在內容瀏覽器的&#x200B;**[!UICONTROL 資料模型對象]**&#x200B;頁籤中。

>[!NOTE]
>
>對於自適應表單片段，只有在編寫時選擇的資料模型對象及其關聯的資料模型對象才會顯示在「資料模型對象」頁籤中。

![data-model-objects-tab](assets/data-model-objects-tab.png)

您可以將資料模型物件拖放至最適化表單或片段上，以新增表單欄位。 新增的表格欄位會保留中繼資料屬性，並與資料模型物件屬性系結。 此系結可確保在表單提交時，欄位值會在對應的資料來源中更新，並在轉譯表單時預先填入。

## 建立互動式通訊{#create-ic}

您可以根據表單資料模型建立互動式通訊，您可使用已設定資料來源的資料來預先填寫互動式通訊。 此外，諸如文本、清單和條件文檔片段等互動式通信的構建塊可以基於表單資料模型。

在建立互動式通訊或檔案片段時，您可以選擇表單資料模型。 下圖顯示了「建立互動式通信」對話框的「常規」頁籤。

![create-ic](assets/create-ic.png)

「建立互動式通信」對話框的「常規」頁籤

如需詳細資訊，請參閱：

[建立互動式通訊](../../forms/using/create-interactive-communication.md)

[互動式通訊中的文字](/help/forms/using/texts-interactive-communications.md)

[互動式通訊的條件](/help/forms/using/conditions-interactive-communications.md)

[清單片段](/help/forms/using/lists.md)

## 使用範例資料{#preview-ic}預覽

表單資料模型編輯器允許您為表單資料模型中的資料模型對象生成和編輯示例資料。 您可以使用這些資料來預覽和測試互動式通訊和調適性表單。 在預覽之前，您必須先產生範例資料，如[使用表單資料模型](../../forms/using/work-with-form-data-model.md#sample)所述。

若要預覽具有範例表單資料模型資料的互動式通訊：

1. 在作AEM者例項中，導覽至&#x200B;**[!UICONTROL Forms>Forms與檔案]**。
1. 選擇互動式通訊，並點選工具列中的&#x200B;**[!UICONTROL 預覽]**&#x200B;以選擇&#x200B;**[!UICONTROL 網頁頻道]**、**[!UICONTROL 列印頻道]**&#x200B;或&#x200B;**[!UICONTROL 兩個頻道]**&#x200B;來預覽互動式通訊。
1. 在「預覽&#x200B;[*channel*]」對話方塊中，確定已選取「測試表單資料模型的資料」，並點選「預覽&#x200B;**[!UICONTROL 」。****]**

互動式通訊會開啟，並預先填入範例資料。

![網頁預覽](assets/web-preview.png)

同樣地，若要預覽具有範例資料的最適化表單，請在作者模式中開啟最適化表單，然後點選「預覽」****。

## 使用表單資料模型服務{#prefill}預填

AEM Forms提供現成可用的表單資料模型預填服務，讓您能夠根據表單資料模型，進行最適化表單和互動式通訊。 預填充服務以自適應形式和互動式通信查詢資料模型對象的資料源，並相應地在呈現表單或通信的同時預填充資料。

要為自適應表單啟用表單資料模型預填充服務，請開啟「自適應表單容器」屬性，並從「基本」accordion的「預填充服務」下拉式清單中選擇「**[!UICONTROL 表單資料模型預填充服務」。]******&#x200B;然後，儲存屬性。

![預填充服務](assets/prefill-service.png)

若要在互動式通訊中設定表單資料模型預填服務，您可以在建立表單資料模型預填服務時，在「預填服務」下拉式清單中選取「表單資料模型預填服務」(Form Data Model Prefill Service)，或在稍後修改屬性。

![edit-ic-props](assets/edit-ic-props.png)

編輯互動式通訊的屬性對話方塊

## 將提交的自適應表單資料寫入資料源{#write-af}

當使用者根據表單資料模型提交表單時，您可以設定表單，將資料模型物件的提交資料寫入其資料來源。 為了實現此使用案例，AEM Forms提供了「表單資料模型提交操作」（僅針對基於表單資料模型的自適應表單提供現成可用的操作）。 [](../../forms/using/configuring-submit-actions.md)它將資料模型對象的提交資料寫入其資料源。

要配置表單資料模型提交操作，請開啟「自適應表單容器」屬性，並從「提交accordion」下的「提交操作」下拉式清單中選擇「使用表單資料模型提交」。 ****&#x200B;然後，瀏覽並從要提交的資料模型對象的&#x200B;**[!UICONTROL 名稱下拉式清單中選擇資料模型對象。]**&#x200B;儲存屬性。

在表單提交時，將配置的資料模型對象的資料寫入到各個資料源。

![資料提交](assets/data-submission.png)

您也可以使用二進位資料模型物件屬性，將表單附件提交至資料來源。 執行以下操作以向JDBC資料源提交附件：

1. 將包含二進位屬性的資料模型物件新增至表單資料模型。
1. 在最適化表單中，將&#x200B;**[!UICONTROL File Attachment]**&#x200B;元件從元件瀏覽器拖放到最適化表單上。
1. 點選以選取新增的元件，並點選![settings_icon](assets/settings_icon.png)以開啟元件的「屬性」瀏覽器。
1. 在「系結參考」欄位中，點選![foldersearch_18](assets/foldersearch_18.png)並導覽以選取您在表單資料模型中新增的二進位屬性。 視需要設定其他屬性。

   點選![check-button](assets/check-button.png)以儲存屬性。 附件欄位現在綁定到表單資料模型的二進位屬性。

1. 在「最適化表單容器」屬性的「提交」區段中，啟用「提交表單附件」。 ****&#x200B;它會在表單提交時，將二進位屬性欄位中的附件提交給資料來源。

## 使用規則{#invoke-services}調用最適化表單中的服務

在基於表單資料模型的自適應表單中，可以[建立規則](../../forms/using/rule-editor.md)以調用在表單資料模型中配置的服務。 規則中的&#x200B;**[!UICONTROL 叫用服務]**&#x200B;操作列出了表單資料模型中的所有可用服務，並允許您為服務選擇輸入和輸出欄位。 您也可以使用&#x200B;**設定值**&#x200B;規則類型來叫用表單資料模型服務，並將欄位值設定為服務傳回的輸出。

例如，下列規則會叫用以員工ID為輸入的get服務，而傳回的值會填入表單中對應的「相依ID」、「姓」、「名字」和「性別」欄位。

![調用服務](assets/invoke-service.png)

此外，您還可以使用`guidelib.dataIntegrationUtils.executeOperation` API在規則編輯器的代碼編輯器中編寫JavaScript。 如需API詳細資訊，請參閱[API以叫用表單資料模型服務](/help/forms/using/invoke-form-data-model-services.md)。
