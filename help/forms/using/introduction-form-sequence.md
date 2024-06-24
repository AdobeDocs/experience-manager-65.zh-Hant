---
title: 多步驟表單序列簡介
description: 透過AEM Forms，您可以定義一系列表單面板，讓使用者在其中導覽及填寫最適化表單。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 32%

---

# 多步驟表單序列簡介{#introduction-to-multi-step-form-sequence}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文介紹使用基礎元件製作最適化Forms的舊方法。 </span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html) |
| AEM 6.5 | 本文章 |


最適化表單可讓表單作者輕鬆建立多步驟資料擷取體驗。 它隨附內建支援，可建立多個面板並將每個面板與不同的導覽模式建立關聯。表單作者可以在邏輯區段將表單欄位分組，並以面板來代表群組。面板之間的整體導覽是使用面板版面來控制。作者可以選擇以不同的版面配置來排列面板，例如，使用「精靈」版面配置以循序方式放置，或使用「索引標籤」版面配置以臨機操作方式放置。 如需面板配置的相關資訊，請參閱 [調適型表單的版面配置功能](../../forms/using/layout-capabilities-adaptive-forms.md).

在典型的表單填寫體驗中，除了擷取資料以外，還有更多步驟需要完成。 完整的表單提交可能包括其他步驟，例如以數位方式簽署表單、驗證表單中填寫的資訊，以及處理付款。 具體情況因案例而異。

如果您的使用案例需要執行一組資料擷取步驟，或有一些法規需要遵循某些步驟，AEM Forms提供了跨表單強制執行該通用結構的方法。 表單結構的預先實施會定義表單的步驟順序。 ![多步驟表單序列範例](assets/formpipeline.png)

多步驟表單序列範例

以使用案例為例，您需要建立表單的填寫、驗證、簽署和確認步驟順序。 若要建立這類序列，步驟如下：

1. 定義表單範本並將所需面板新增至其中。 序列中的每個步驟都應該有一個面板。不過，您可以在面板中包含子面板。

   在此範例中，可以新增下列面板：

   * **填寫**：包含用來擷取資料的表單欄位。您可以在此加入巢狀子面板，為不同型別的資訊（例如個人、家庭和財務）建立區段。

   * **驗證**：此變數包含 **驗證** 可用於XFA型最適化表單的元件。 它以唯讀模式顯示「填充」面板中擷取的資訊以進行驗證。

   * **電子簽章**：此變數包含 **簽署** 可用於XFA型最適化表單的元件。 它提供下列簽署服務：

      * Adobe Document Cloud 電子簽署服務
      * 手寫簽名

   * **確認**：包含「**摘要**」元件，會在使用者簽署表單並到達序列中的「確認 (摘要)」步驟後，顯示確認表單提交的訊息。作者可以設定「摘要」元件的文字、顯示感謝訊息、顯示產生PDF的連結等。

1. 選取根面板的版面做為「**[!UICONTROL 精靈]**」。
1. 完成其餘步驟，以便建立表單範本。 另請參閱 [建立自訂最適化表單範本](../../forms/using/custom-adaptive-forms-templates.md).

在表單範本中定義表單序列後，您可以使用它來建立具有定義為現有序列的基本結構的表單。 您可以隨時根據需求自訂表格。
