---
title: AEM Forms資料整合
seo-title: AEM Forms Data Integration
description: 資料整合使您能夠將AEM Forms與不同的資料源整合，並建立表單資料模型以建立和使用自適應表單和互動式通信。
seo-description: Data Integration lets you integrate AEM Forms with disparate data sources and create form data model to create and work with adaptive forms and interactive communications.
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
feature: Form Data Model
exl-id: dd1146e4-952d-4dfa-8084-46c6096c4177
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# [!DNL AEM Forms] 資料整合 {#aem-forms-data-integration}

![](do-not-localize/data-integeration.png)

企業基礎架構包括不同的後端系統或資料源，如資料庫、 Web服務、 REST服務、 OData服務和CRM解決方案。 綜上所述，他們建立了一個為企業應用程式提供資料以執行日常業務的資訊系統。 另一方面，應用程式會捕獲資料並將其發送回更新資料源。

[!DNL AEM Forms] 諸如自適應表單和互動式通信之類的應用程式需要與資料源整合以在呈現表單和建立互動式通信的同時獲取客戶資料。 當根據自適應表單中的用戶輸入從資料源獲取資料時，存在使用情形。 此外，可以回寫所提交的自適應表單資料以更新各個資料源。

雖然分佈式模組化系統有其自身的優點，但挑戰在於跨資料源整合和建立資料關聯。 資料整合是功能強大、高效的企業基礎架構的關鍵，該基礎架構的不同資料源連接到用於交換業務資料的應用程式。

## 資料整合概述 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] 資料整合允許配置和連接不同的資料源 [!DNL AEM Forms]。 它提供了直觀的用戶介面，以建立跨連接資料源的業務實體和服務的統一資料表示模式。 統一表示稱為表單資料模型，是JSON架構的擴展。 表單資料模型中的實體稱為資料模型對象。 表單資料模型允許您：

* 從連接的資料源訪問資料模型對象、屬性和服務。
* 建立自定義資料模型對象和屬性
* 在資料源內和資料源之間建立資料模型對象之間的關聯。
* 調用資料模型對象服務以查詢資料源或將資料從資料源寫入資料。

建立表單資料模型後，可以在各種自適應表單和互動式通信工作流中使用它，例如：

* 基於表單資料模型建立自適應表單和互動式通信
* 預填充自適應表單和來自配置資料源的互動式通信
* 使用自適應表單規則調用資料源服務/操作
* 將提交的自適應表單資料寫入資料源

## 資料整合入門 {#get-started-with-data-integration}

實施資料整合的第一步是確定和配置資料源，這些資料源儲存您希望以自適應形式和互動式通信使用情形利用的資訊。 接下來，您將建立一個表單資料模型，該模型使用來自一個或多個資料源的資料模型對象、屬性和服務。 您可以基於表單資料模型建立自適應表單和互動式通信，其中互動式通信中的自適應表單域或佔位符綁定到相應的資料源屬性。

[!DNL AEM Forms] 還允許您建立與資料源無關的表單資料模型，並稍後將表單資料模型中的資料模型對象和屬性與資料源關聯或綁定。 它消除了在處理表單資料模型時對資料源的任何依賴。

查看以下內容以開始、瞭解和實施資料整合。

* [設定資料來源](../../forms/using/configure-data-sources.md)
* [建立表單資料模型](../../forms/using/create-form-data-models.md)
* [使用表單資料模型](../../forms/using/work-with-form-data-model.md)
* [使用表單資料模型](../../forms/using/using-form-data-model.md)
