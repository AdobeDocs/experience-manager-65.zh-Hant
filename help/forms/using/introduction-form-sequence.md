---
title: 多步驟表單序列簡介
seo-title: Introduction to multi-step form sequence
description: 透過AEM Forms，您可以定義一系列表單面板，讓使用者在其中導覽及填寫最適化表單。
seo-description: With AEM Forms, you can define a sequence of form panel in which you want users to navigate and fill an adaptive form.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
feature: Adaptive Forms
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 3%

---

# 多步驟表單序列簡介{#introduction-to-multi-step-form-sequence}

<span class="preview"> Adobe建議使用現代化且可擴充的資料擷取 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 的 [建立新的Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [將最適化Forms新增至AEM Sites頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 這些元件代表最適化Forms建立工作取得重大進展，可確保提供令人驚歎的使用者體驗。 本文說明使用基礎元件製作最適化Forms的舊方法。 </span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html) |
| AEM 6.5 | 本文 |


最適化表單可讓表單作者輕鬆建立多步驟資料擷取體驗。 隨附內建支援，可建立多個面板，以及將每個面板與不同導覽模式建立關聯。 表單作者可將邏輯區段中的表單欄位分組，並將群組表示為面板。 面板之間的整體導覽會使用面板配置來控制。 作者可以選擇以不同的版面配置來排列面板，例如，使用「精靈」版面配置按順序放置，或使用「索引標籤」版面配置以臨機操作方式放置。 如需面板配置的相關資訊，請參閱 [調適型表單的版面配置功能](../../forms/using/layout-capabilities-adaptive-forms.md).

在典型的表單填寫體驗中，除了擷取資料以外，還有更多步驟需要處理。 完整的表單提交可包括其他步驟，例如以數位方式簽署表單、驗證表單中填寫的資訊、處理付款等。 每個案例都不同。

如果您的使用案例需要一組資料擷取步驟，或有一些法規需要遵循某些步驟，AEM Forms會提供在表單中強制執行該通用結構的方法。 表單結構的預先實施會定義表單的步驟順序。 ![多步驟表單序列的範例](assets/formpipeline.png)

多步驟表單序列的範例

以您需要建立表單填寫、驗證、簽署和確認步驟的序列的使用案例為例。 建立此類序列的步驟如下：

1. 定義表單範本並在其中新增必要面板。 請注意，序列中的每個步驟都應該有一個面板。 不過，您可以在面板中包含子面板。

   在此範例中，我們可以新增下列面板：

   * **填滿**：其中包含用於擷取資料的表單欄位。 在這裡，您可以包含巢狀子面板，以針對不同型別的資訊（例如個人、家庭、財務等）建立區段。

   * **驗證**：此變數包含 **驗證** 可用於XFA型最適化表單的元件。 它以唯讀模式顯示「填滿」面板中擷取的資訊以進行驗證。

   * **電子簽章**：此變數包含 **簽署** 可用於XFA型最適化表單的元件。 它提供下列簽署服務：

      * Adobe Document Cloud eSign服務
      * 草寫簽名

   * **確認**：此變數包含 **摘要** 在使用者簽署表單並到達序列中的確認（摘要）步驟後，顯示確認表單提交的訊息的元件。 作者可以設定「摘要」元件的文字、顯示感謝訊息、顯示產生PDF的連結等。

1. 選取根面板的版面配置為 **[!UICONTROL 精靈]**.
1. 完成其餘步驟以建立表單範本。 如需詳細資訊，請參閱 [建立自訂最適化表單範本](../../forms/using/custom-adaptive-forms-templates.md).

在表單範本中定義表單順序後，您可以使用它來建立具有定義為現有順序的基本結構的表單，不過您可以隨時自訂表單以符合您的需求。
