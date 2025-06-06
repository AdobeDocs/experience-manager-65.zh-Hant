---
title: 使用表單資料模型
description: 瞭解如何使用表單資料模型來建立和使用最適化表單和互動式通訊。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
docset: aem65
feature: Form Data Model
exl-id: 9a73a643-7ad4-49aa-a971-08d52679158d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 1%

---

# 使用表單資料模型{#use-form-data-model}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |


![hero-image](do-not-localize/data-integration.png)

AEM Forms資料整合可讓您使用不同的後端資料來源建立表單資料模型，以用作各種最適化表單和互動式通訊工作流程中的結構描述。 它需要設定資料來源，並根據資料來源中可用的資料模型物件和服務來建立表單資料模型。 如需詳細資訊，請參閱下列內容：

* [AEM Forms資料整合](../../forms/using/data-integration.md)
* [設定資料來源](../../forms/using/configure-data-sources.md)
* [建立表單資料模型](../../forms/using/create-form-data-models.md)
* [使用表單資料模型](../../forms/using/work-with-form-data-model.md)

表單資料模型是JSON結構描述的擴充功能，可用來執行以下操作：

* [建立最適化表單和片段](#create-af)
* [建立互動式通訊和建置區塊，例如文字、清單和條件片段](#create-ic)
* [使用範例資料預覽互動式通訊](#preview-ic)
* [預填最適化表單和互動式通訊](#prefill)
* [將提交的最適化表單資料寫回資料來源](#write-af)
* [使用最適化表單規則叫用服務](#invoke-services)

## 建立最適化表單和片段 {#create-af}

您可以根據表單資料模型建立[最適化表單](../../forms/using/creating-adaptive-form.md)和[最適化表單片段](../../forms/using/adaptive-form-fragments.md)。 執行下列動作，在建立最適化表單或最適化表單片段時使用表單資料模型：

1. 在[新增屬性]畫面的[表單模型]索引標籤中，選取&#x200B;**[!UICONTROL 從]**&#x200B;選取下拉式清單中的&#x200B;**[!UICONTROL 表單資料模型]**。

   ![create-af-1-1](assets/create-af-1-1.png)

1. 選取以展開&#x200B;**[!UICONTROL 選取表單資料模型]**。 列出所有可用的表單資料模型。

   從資料模型中選取。

   ![create-af-2-1](assets/create-af-2-1.png)

1. （**僅限最適化表單片段**）您只能根據表單資料模型中的一個資料模型物件來建立最適化表單片段。 展開&#x200B;**[!UICONTROL 表單資料模型定義]**&#x200B;下拉式清單。 它會列出指定表單資料模型中的所有資料模型物件。 從清單中選取資料模型物件。

   ![create-af-3](assets/create-af-3.png)

根據表單資料模型建立最適化表單或最適化表單片段後，表單資料模型物件會出現在最適化表單編輯器中，內容瀏覽器的&#x200B;**[!UICONTROL 資料模型物件]**&#x200B;索引標籤中。

>[!NOTE]
>
>對於最適化表單片段，只有編寫時選取的資料模型物件及其關聯的資料模型物件會出現在資料模型物件索引標籤中。

![data-model-objects-tab](assets/data-model-objects-tab.png)

您可以將資料模型物件拖放至最適化表單或片段來新增表單欄位。 新增的表單欄位會保留中繼資料屬性，並與資料模型物件屬性繫結。 繫結可確保欄位值在表單提交時更新到對應的資料來源中，並在表單轉譯時預先填充。

## 建立互動式通訊 {#create-ic}

您可以根據表單資料模型來建立互動式通訊，您可以使用已設定資料來源的資料來預先填入互動式通訊。 此外，互動式通訊的建置區塊（例如文字、清單和條件檔案片段）可以表單資料模型為基礎。

建立互動式通訊或檔案片段時，您可以選擇表單資料模型。 下圖顯示「建立互動式通訊」對話方塊的「一般」標籤。

![建立ic](assets/create-ic.png)

建立互動式通訊對話方塊的一般標籤

如需詳細資訊，請參閱：

[建立互動式通訊](../../forms/using/create-interactive-communication.md)

[互動式通訊中的文字](/help/forms/using/texts-interactive-communications.md)

[互動式通訊的條件](/help/forms/using/conditions-interactive-communications.md)

[清單片段](/help/forms/using/lists.md)

## 使用範例資料預覽 {#preview-ic}

表單資料模型編輯器可讓您為表單資料模型中的資料模型物件產生和編輯範例資料。 您可以使用此資料來預覽和測試互動式通訊和調適型表單。 在預覽之前產生範例資料，如[使用表單資料模型](../../forms/using/work-with-form-data-model.md#sample)中所述。

若要預覽包含範例表單資料模型資料的互動式通訊：

1. 在AEM作者執行個體上，瀏覽至&#x200B;**[!UICONTROL Forms > Forms &amp; Documents]**。
1. 選取互動式通訊，並在工具列中選取&#x200B;**[!UICONTROL 預覽]**&#x200B;以選取&#x200B;**[!UICONTROL Web Channel]**、**[!UICONTROL Print Channel]**&#x200B;或&#x200B;**[!UICONTROL Both Channel]**&#x200B;以預覽互動式通訊。
1. 在預覽&#x200B;[*管道*]&#x200B;對話方塊中，確定已選取&#x200B;**[!UICONTROL 表單資料模型]**&#x200B;的測試資料，並選取&#x200B;**[!UICONTROL 預覽]**。

互動式通訊隨即開啟，並預填樣本資料。

![網頁預覽](assets/web-preview.png)

同樣地，若要預覽含有範例資料的最適化表單，請在作者模式中開啟最適化表單，然後選取&#x200B;**[!UICONTROL 預覽]**。

## 使用表單資料模型服務預填 {#prefill}

AEM Forms提供立即可用的表單資料模型預填服務，可讓您啟用最適化表單，以及根據表單資料模型的互動式通訊。 預填服務會在呈現表單或通訊時，查詢最適化表單和互動式通訊中資料模型物件的資料來源，並據以預填資料。

若要啟用最適化表單的表單資料模型預填服務，請開啟「最適化表單容器」屬性，然後從「基本」摺疊式功能表的&#x200B;**[!UICONTROL 預填服務]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 表單資料模型預填服務]**。 然後，儲存屬性。

![預填服務](assets/prefill-service.png)

若要在互動式通訊中設定表單資料模型預填服務，您可以在建立時選取「預填服務」下拉式清單中的「表單資料模型預填服務」，或之後藉由修改屬性來選取「表單資料模型預填服務」。

![編輯ic-props](assets/edit-ic-props.png)

互動式通訊的「編輯內容」對話方塊

## 將提交的最適化表單資料寫入資料來源 {#write-af}

當使用者根據表單資料模型提交表單時，您可以設定表單以將資料模型物件的提交資料寫入其資料來源。 為了達成此使用案例，AEM Forms提供[表單資料模型提交動作](../../forms/using/configuring-submit-actions.md)，僅可用於根據表單資料模型的最適化表單。 它將資料模型物件的已提交資料寫入其資料來源中。

若要設定表單資料模型提交動作，請開啟最適化表單容器屬性，然後從「提交」摺疊式功能表下的「提交動作」下拉式清單中選取&#x200B;**[!UICONTROL 使用表單資料模型提交]**。 然後，從要提交的資料模型物件的&#x200B;**[!UICONTROL 名稱]**&#x200B;下拉式清單中瀏覽並選取資料模型物件。 儲存屬性。

在提交表單時，會將已設定資料模型物件的資料寫入各自的資料來源。

![資料提交](assets/data-submission.png)

您也可以使用二進位資料模型物件屬性，將表單附件提交至資料來源。 執行下列動作，將附件提交至JDBC資料來源：

1. 將包含二進位屬性的資料模型物件新增至表單資料模型。
1. 在最適化表單中，將&#x200B;**[!UICONTROL 檔案附件]**&#x200B;元件從「元件」瀏覽器拖放到最適化表單上。
1. 選取「 」以選取新增的元件，並選取「![settings_icon](assets/settings_icon.png)」以開啟元件的「屬性」瀏覽器。
1. 在「繫結參考」欄位中，選取![foldersearch_18](assets/foldersearch_18.png)，並導覽以選取您在表單資料模型中新增的二進位屬性。 視需要設定其他屬性。

   選取![check-button](assets/check-button.png)以儲存屬性。 附件欄位現在已繫結至表單資料模型的二進位屬性。

1. 在最適化表單容器屬性的提交區段中，啟用&#x200B;**[!UICONTROL 提交表單附件]**。 它會在表單提交時，將二進位屬性欄位中的附件提交至資料來源。

## 使用規則在最適化表單中叫用服務 {#invoke-services}

在基於表單資料模型的最適化表單中，您可以[建立規則](../../forms/using/rule-editor.md)以叫用表單資料模型中設定的服務。 規則中的&#x200B;**[!UICONTROL Invoke Services]**&#x200B;作業會列出表單資料模型中的所有可用服務，並讓您選取服務的輸入和輸出欄位。 您也可以使用&#x200B;**設定值**&#x200B;規則型別來呼叫表單資料模型服務，並將欄位值設定為服務傳回的輸出。

例如，下列規則會叫用以Employee Id作為輸入的get服務，而傳回的值會填入表單中對應的Dependent Id、Last Name、First Name和Gender欄位。

![叫用服務](assets/invoke-service.png)

此外，您可以使用`guidelib.dataIntegrationUtils.executeOperation` API在規則編輯器的程式碼編輯器中撰寫JavaScript。 如需API詳細資料，請參閱[要叫用表單資料模型服務](/help/forms/using/invoke-form-data-model-services.md)的API。
