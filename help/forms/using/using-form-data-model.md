---
title: 使用表單資料模型
seo-title: Use form data model
description: 瞭解如何使用表單資料模型來建立和使用自適應表單和互動式通信。
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

AEM Forms資料整合允許您使用全異的後端資料源來建立表單資料模型，您可以在各種自適應表單和互動式通信工作流中將其用作模式。 它需要配置資料源並基於資料源中可用的資料模型對象和服務建立表單資料模型。 有關詳細資訊，請參閱以下內容：

* [AEM Forms資料整合](../../forms/using/data-integration.md)
* [設定資料來源](../../forms/using/configure-data-sources.md)
* [建立表單資料模型](../../forms/using/create-form-data-models.md)
* [使用表單資料模型](../../forms/using/work-with-form-data-model.md)

表單資料模型是JSON架構的擴展，您可以使用它：

* [建立自適應窗體和片段](#create-af)
* [建立互動式通信和構建塊，如文本、清單和條件片段](#create-ic)
* [預覽與示例資料的交互通信](#preview-ic)
* [預填充自適應表單和互動式通信](#prefill)
* [將提交的自適應表單資料寫回資料源](#write-af)
* [使用自適應表單規則調用服務](#invoke-services)

## 建立自適應窗體和片段 {#create-af}

您可以建立 [自適應格式](../../forms/using/creating-adaptive-form.md) 和 [自適應形式片段](../../forms/using/adaptive-form-fragments.md) 基於表單資料模型。 在建立自適應表單或自適應表單片段時，請執行以下操作以使用表單資料模型：

1. 在「添加屬性」螢幕的「表單模型」頁籤中，選擇 **[!UICONTROL 窗體資料模型]** 的 **[!UICONTROL 從中選擇]** 的子菜單。

   ![建立af-1-1](assets/create-af-1-1.png)

1. 點擊以展開 **[!UICONTROL 選擇表單資料模型]**。 列出所有可用表單資料模型。

   從資料模型中選擇。

   ![建立af-2-1](assets/create-af-2-1.png)

1. (**僅自適應表單片段**)可以在表單資料模型中僅基於一個資料模型對象建立自適應表單片段。 展開 **[!UICONTROL 表單資料模型定義]** 下拉。 它列出指定表單資料模型中的所有資料模型對象。 從清單中選擇資料模型對象。

   ![建立af-3](assets/create-af-3.png)

一旦建立基於表單資料模型的自適應表單或自適應表單片段，表單資料模型對象就出現在 **[!UICONTROL 資料模型對象]** 的子菜單。

>[!NOTE]
>
>對於自適應表單片段，只有在創作時選擇的資料模型對象及其關聯的資料模型對象才會顯示在「資料模型對象」頁籤中。

![資料模型對象頁籤](assets/data-model-objects-tab.png)

可以將資料模型對象拖放到自適應表單或片段上以添加表單域。 添加的表單域保留元資料屬性並與資料模型對象屬性綁定。 該綁定確保在提交表單時在相應資料源中更新欄位值，並在呈現表單時預填。

## 建立互動式通信 {#create-ic}

您可以基於表單資料模型建立互動式通信，您可以使用該模型預先填充來自已配置資料源的資料的互動式通信。 此外，諸如文本、清單和條件文檔片段的互動式通信的構造塊可以基於表單資料模型。

在建立互動式通信或文檔片段時，可以選擇表單資料模型。 下圖顯示了「建立互動式通信」對話框的「常規」頁籤。

![建立ic](assets/create-ic.png)

「建立互動式通信」對話框的「常規」頁籤

有關詳細資訊，請參閱：

[建立互動式通信](../../forms/using/create-interactive-communication.md)

[互動式通信中的文本](/help/forms/using/texts-interactive-communications.md)

[交互通信中的條件](/help/forms/using/conditions-interactive-communications.md)

[清單片段](/help/forms/using/lists.md)

## 使用示例資料預覽 {#preview-ic}

表單資料模型編輯器允許您為表單資料模型中的資料模型對象生成和編輯示例資料。 您可以使用此資料來預覽和test互動式通信和自適應表單。 在預覽之前必須生成示例資料，如中所述 [使用表單資料模型](../../forms/using/work-with-form-data-model.md#sample)。

要預覽與示例表單資料模型資料的互動式通信，請執行以下操作：

1. 在作AEM者實例上，導航至 **[!UICONTROL Forms>Forms和文檔]**。
1. 選擇互動式通信並點擊 **[!UICONTROL 預覽]** 的 **[!UICONTROL Web通道]**。 **[!UICONTROL 打印通道]**&#x200B;或 **[!UICONTROL 兩個頻道]** 預覽互動式通信。
1. 在預覽中 [*通道*] 對話，確保 **[!UICONTROL Test表單資料模型]** 選中並點擊 **[!UICONTROL 預覽]**。

互動式通信以預填樣本資料開啟。

![Web預覽](assets/web-preview.png)

同樣，要預覽帶有示例資料的自適應表單，請在作者模式下開啟自適應表單並點擊 **[!UICONTROL 預覽]**。

## 使用表單資料模型服務的預填充 {#prefill}

AEM Forms公司提供現成的表單資料模型預填充服務，您可以基於表單資料模型啟用自適應表單和互動式通信。 所述預填充服務在自適應表單和互動式通信中查詢資料模型對象的資料源，並相應地在呈現表單或通信的同時預填充資料。

要為自適應表單啟用表單資料模型預填充服務，請開啟「自適應表單容器」屬性並選擇 **[!UICONTROL 表單資料模型預填充服務]** 從 **[!UICONTROL 預填充服務]** 按鈕。 然後，保存屬性。

![預填充服務](assets/prefill-service.png)

要在互動式通信中配置表單資料模型預填充服務，可以在「預填充服務」下拉清單中選擇「表單資料模型預填充服務」，同時通過修改屬性來建立該服務。

![編輯 — 道具](assets/edit-ic-props.png)

編輯互動式通信的屬性對話框

## 將提交的自適應表單資料寫入資料源 {#write-af}

當用戶基於表單資料模型提交表單時，可以配置表單以將資料模型對象的提交資料寫入其資料源。 為了實現此使用情形，AEM Forms提供 [表單資料模型提交操作](../../forms/using/configuring-submit-actions.md)，僅適用於基於表單資料模型的自適應表單的出廠設定。 它將資料模型對象的提交資料寫入其資料源。

要配置表單資料模型提交操作，請開啟自適應表單容器屬性並選擇 **[!UICONTROL 使用表單資料模型提交]** 從「提交」面板下的「提交操作」下拉清單中。 然後，瀏覽並從 **[!UICONTROL 要提交的資料模型對象的名稱]** 下拉。 保存屬性。

在表單提交時，將配置的資料模型對象的資料寫入相應的資料源。

![資料提交](assets/data-submission.png)

您還可以使用二進位資料模型對象屬性將表單附件提交到資料源。 執行以下操作將附件提交到JDBC資料源：

1. 將包含二進位屬性的資料模型對象添加到表單資料模型。
1. 在自適應窗體中，拖放 **[!UICONTROL 檔案附件]** 從「元件」瀏覽器到自適應窗體的元件。
1. 點擊以選擇添加的元件，然後點擊 ![設定表徵圖](assets/settings_icon.png) 開啟元件的屬性瀏覽器。
1. 在「綁定引用」欄位中，按一下 ![foldersearch_18](assets/foldersearch_18.png) 並導航以選擇在表單資料模型中添加的二進位屬性。 根據需要配置其他屬性。

   點擊 ![按鈕](assets/check-button.png) 的子菜單。 附件欄位現在綁定到窗體資料模型的二進位屬性。

1. 在「自適應表單容器」屬性的「提交」部分，啟用 **[!UICONTROL 提交表單附件]**。 它在提交表單時將二進位屬性欄位中的附件提交到資料源。

## 使用規則在自適應表單中調用服務 {#invoke-services}

在基於表單資料模型的自適應表單中， [建立規則](../../forms/using/rule-editor.md) 調用窗體資料模型中配置的服務。 的 **[!UICONTROL 調用服務]** 規則中的操作將列出表單資料模型中的所有可用服務，並允許您為服務選擇輸入和輸出欄位。 您還可以使用 **設定值** 規則類型，用於調用表單資料模型服務並將欄位的值設定為服務返回的輸出。

例如，以下規則調用以員工ID為輸入的獲取服務，返回的值將填充到表單中相應的「從屬ID」、「姓氏」、「名字」和「性別」欄位中。

![調用服務](assets/invoke-service.png)

此外，您還可以 `guidelib.dataIntegrationUtils.executeOperation` 在規則編輯器的代碼編輯器中編寫JavaScript的API。 有關API詳細資訊，請參見 [調用表單資料模型服務的API](/help/forms/using/invoke-form-data-model-services.md)。
