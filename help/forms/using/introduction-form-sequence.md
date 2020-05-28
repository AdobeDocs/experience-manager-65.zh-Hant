---
title: 多步驟表單序列簡介
seo-title: 多步驟表單序列簡介
description: 有了AEM Forms，您可以定義表單面板的順序，讓使用者在其中導覽並填寫最適化表單。
seo-description: 有了AEM Forms，您可以定義表單面板的順序，讓使用者在其中導覽並填寫最適化表單。
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
translation-type: tm+mt
source-git-commit: 68ea2335a8466c3c23b766efb1a04b6a38d7f670
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---


# 多步驟表單序列簡介{#introduction-to-multi-step-form-sequence}

最適化表單可讓表單作者輕鬆建立多步驟資料擷取體驗。 它提供內建支援，可建立多個面板，並將每個面板與不同的導覽模式建立關聯。 表單作者可將邏輯區段中的表單欄位分組，並將群組表示為面板。 使用面板版面控制面板之間的整體導覽。 作者可以選擇以不同版面排列面板，例如使用精靈版面依序排列面板，或使用標籤式版面以臨機方式排列面板。 如需面板版面的詳細資訊，請參 [閱最適化表單的版面功能](../../forms/using/layout-capabilities-adaptive-forms.md)。

在一般的表單填寫體驗中，除了擷取資料外，還需執行更多步驟。 完整的表單提交可包括其他步驟，例如數位簽署表單、驗證表單中填入的資訊、處理付款等。 它不同於個案。

如果您的使用案例要求資料擷取的一組步驟，或有需要遵循特定步驟的法規，AEM Forms會提供跨表單強制執行該共同結構的方法。 表單結構的預先實施定義了表單的步驟順序。 ![多步驟表單序列範例](assets/formpipeline.png)

多步驟表單序列範例

讓我們舉個例子，說明您需要為表單建立填寫、驗證、簽署和確認步驟的序列。 建立此序列的步驟如下：

1. 定義表單範本並新增必要面板。 請注意，序列中每個步驟都應有一個面板。 不過，您可以在面板內加入子面板。

   在此範例中，我們可新增下列面板：

   * **填滿**: 它包含用於擷取資料的表單欄位。 在這裡，您可以包含巢狀子面板，以針對不同類型的資訊建立區段，例如個人、家庭、財務等。

   * **驗證**: 它包含 **Verify** （驗證）元件，可用於XFA自適應表單。 它會以唯讀模式顯示在「填色」面板中擷取的資訊，以進行驗證。

   * **電子簽名**: 它包含 **Sign** 元件，可用於XFA自適應表單。 它提供下列簽署服務：

      * Adobe Document Cloud eSign Services
      * 塗鴉簽名
   * **確認**: 它包含 **Summary** （摘要）元件，在用戶簽署表單並進入序列中的Confirmation(Summary)步驟後，該元件將顯示確認表單提交的消息。 作者可以設定「摘要」元件的文字、顯示感謝訊息、顯示產生的PDF連結等。


1. 將根面板的佈局選為「 **[!UICONTROL 嚮導」]**。
1. 完成剩餘步驟以建立表單範本。 如需詳細資訊，請參 [閱建立自訂最適化表單範本](../../forms/using/custom-adaptive-forms-templates.md)。

在表單範本中定義表單序列後，您可以使用它建立表單，其基本結構將定義為序列，不過您隨時都可以自訂表單以符合您的需求。

