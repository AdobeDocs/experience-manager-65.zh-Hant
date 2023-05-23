---
title: 多步形式序列簡介
seo-title: Introduction to multi-step form sequence
description: 使用AEM Forms，您可以定義表單面板序列，您希望用戶在其中導航並填寫自適應表單。
seo-description: With AEM Forms, you can define a sequence of form panel in which you want users to navigate and fill an adaptive form.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
feature: Adaptive Forms
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 多步形式序列簡介{#introduction-to-multi-step-form-sequence}

自適應表單使表單作者能夠輕鬆建立多步資料捕獲體驗。 它提供了內置支援，用於建立多個面板並將每個面板與不同的導航模式相關聯。 表單作者可以在邏輯部分中對表單域進行分組，並將組表示為面板。 使用面板佈局控制面板之間的整體導航。 作者可以選擇以不同佈局排列面板，例如，使用「嚮導」佈局按順序放置面板，或使用「頁籤式佈局」按臨時方式放置面板。 有關面板佈局的資訊，請參見 [自適應表單的佈局功能](../../forms/using/layout-capabilities-adaptive-forms.md)。

在典型的表單填充體驗中，涉及的步驟比僅捕獲資料還要多。 完整的表單提交可以包括其他步驟，如數字簽名表單、驗證表單中填充的資訊、處理付款等。 不同的案例。

如果您的使用案例要求執行一組資料捕獲步驟，或有一些管理法規需要遵循某些步驟，AEM Forms將提供一種方法，可跨表單強制實施此通用結構。 表單結構的預先實現定義了表單的步驟順序。 ![多步表單序列示例](assets/formpipeline.png)

多步表單序列示例

讓我們採用一個使用案例，您需要為表單建立填充、驗證、簽名和確認步驟的序列。 建立此序列的步驟如下：

1. 定義表單模板並向其添加所需的面板。 請注意，序列中的每個步驟都應有一個面板。 但是，可以在面板內包括子面板。

   在本示例中，我們可以添加以下面板：

   * **填充**:它包含用於捕獲資料的表單域。 在此，您可以包括嵌套的子面板，以為不同類型的資訊建立節，如個人資訊、家庭資訊、財務資訊等。

   * **驗證**:它包含 **驗證** 可在基於XFA的自適應形式中使用的元件。 它以只讀模式顯示在「填充」面板中捕獲的資訊以進行驗證。

   * **電子簽名**:它包含 **簽名** 可在基於XFA的自適應形式中使用的元件。 它提供以下簽名服務：

      * Adobe Document Cloud電子簽名服務
      * Scribble簽名
   * **確認**:它包含 **摘要** 元件，它顯示一條消息，確認用戶在簽署表單後提交表單，並進入序列中的「確認（摘要）」步驟。 作者可以配置摘要元件的文本、顯示感謝消息、顯示到生成的PDF的連結等。


1. 選擇根面板的佈局作為 **[!UICONTROL 嚮導]**。
1. 完成其餘步驟以建立表單模板。 有關詳細資訊，請參見 [建立自定義自適應表單模板](../../forms/using/custom-adaptive-forms-templates.md)。

在表單模板中定義表單序列後，您可以使用它建立具有將基本結構定義為已就位序列的表單，不過您始終可以自定義表單以滿足您的要求。
