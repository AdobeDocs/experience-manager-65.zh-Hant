---
title: AEM Forms資料整合
seo-title: AEM Forms資料整合
description: 「資料整合」可讓您將AEM Forms與不同的資料來源整合，並建立表單資料模型，以建立並使用最適化表單和互動式通訊。
seo-description: 「資料整合」可讓您將AEM Forms與不同的資料來源整合，並建立表單資料模型，以建立並使用最適化表單和互動式通訊。
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# AEM Forms資料整合{#aem-forms-data-integration}

![](do-not-localize/data-integeration.png)

企業基礎架構包括分散的後端系統或資料來源，例如資料庫、web services、REST services、OData services和CRM解決方案。 總之，他們可建立一個資訊系統，為企業應用程式提供資料，以執行日常業務。 另一方面，應用程式會擷取資料並傳回以更新資料來源。

AEM Forms應用程式（例如可調式表單和互動式通訊）需要與資料來源整合，以擷取客戶資料，同時轉譯表單和建立互動式通訊。 在使用案例中，根據自適應表單中的用戶輸入從資料源提取資料。 此外，可以將提交的自適應表單資料寫回以更新各個資料源。

雖然分散式模組化系統有其自身的優點，但挑戰在於整合和建立跨資料來源的資料關聯。 資料整合是功能強大且有效率的企業基礎架構的關鍵，其中不同資料來源會連接至應用程式，以交換商業資料。

## 資料整合概觀 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

AEM Forms Data Integration可讓您設定不同的資料來源並與AEM Forms連接。 它提供直覺式使用者介面，以建立跨連線資料來源之商業實體與服務的統一資料表示架構。 統一表示法稱為表單資料模型，JSON結構描述的擴充功能。 表單資料模型中的實體稱為資料模型對象。 表單資料模型可讓您：

* 從連接的資料來源存取資料模型物件、屬性和服務。
* 建立自訂資料模型物件和屬性
* 在資料來源內部和跨資料來源建立資料模型物件之間的關聯。
* 叫用資料模型物件服務，以查詢資料來源或從資料來源寫入資料。

在建立表單資料模型後，您就可以在各種調適性表單和互動式通訊工作流程中使用它，例如：

* 建立以表單資料模型為基礎的自適應表單和互動式通訊
* 預先填寫來自已設定資料來源的最適化表單和互動式通訊
* 使用自適應表單規則調用資料源服務／操作
* 將提交的自適應表單資料寫入資料來源

## 開始使用資料整合 {#get-started-with-data-integration}

實作資料整合的第一步是識別並設定資料來源，以儲存您要在最適化表單和互動式通訊使用案例中運用的資訊。 接著，您會建立表單資料模型，其使用來自一或多個資料來源的資料模型物件、屬性和服務。 您可以根據表單資料模型建立最適化表單和互動式通訊，其中互動式通訊中的最適化表單欄位或預留位置會系結至個別資料來源屬性。

AEM Forms也可讓您建立與資料來源無關的表單資料模型，並稍後在表單資料模型中與資料來源建立關聯或系結資料模型物件和屬性。 它可消除您在處理表單資料模型時對資料來源的任何依賴。

請檢視下列內容，以開始、瞭解並實作資料整合。

* [設定資料來源](../../forms/using/configure-data-sources.md)
* [建立表單資料模型](../../forms/using/create-form-data-models.md)
* [使用表單資料模型](../../forms/using/work-with-form-data-model.md)
* [使用表單資料模型](../../forms/using/using-form-data-model.md)

