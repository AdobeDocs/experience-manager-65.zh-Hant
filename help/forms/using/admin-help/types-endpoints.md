---
title: 端點型別
description: 瞭解不同型別的端點。 可以將不同型別的端點（例如電子郵件、Watched資料夾等）新增到服務中。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 端點型別 {#types-of-endpoints}

您必須先設定並啟用端點，才能使用服務。 端點會指定如何叫用服務。

>[!NOTE]
>
>在Workbench中，端點稱為起點。

下列型別的端點可新增至服務。 並非所有服務都支援所有端點：

**電子郵件：**&#x200B;透過傳送包含一或多個檔案附件的電子郵件訊息至指定的電子郵件帳戶，讓使用者能夠叫用服務。 在設定電子郵件端點之前，您必須設定必要的電子郵件帳戶。 （請參閱設定電子郵件端點）。

**Watched資料夾：**&#x200B;將檔案放在資料夾中，讓使用者可以叫用服務，該資料夾會以定義的間隔掃描。 （請參閱設定watched資料夾端點。）

**TaskManager：**&#x200B;讓Workspace使用者可以叫用服務。

**遠端處理：**&#x200B;啟用以Flex建置的應用程式，以使用(不適用於AEM表單)AEM表單遠端處理來叫用服務。 系統會自動為每個啟用的服務建立遠端端點。 會建立與端點同名的Flex目的地，而Flex使用者端可建立指向此目的地的遠端物件，以叫用相關服務的作業。

**SOAP：**&#x200B;啟用使用AEM表單程式設計API開發的使用者端應用程式，以使用SOAP模式叫用服務。 系統會自動為每個已啟用的服務建立SOAP端點。

**附註**： *在Adobe Acrobat或Adobe Reader中檢視檔案時使用SOAP端點時，可以從Document Security檔案移除安全性。 如需有關如何停用LCRM檔案上的SOAP端點的詳細資訊，請參閱[停用Document Security檔案的SOAP端點](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB：**&#x200B;讓使用AEM Forms程式設計API開發的使用者端應用程式，能夠使用Enterprise JavaBeans (EJB)模式呼叫服務。 系統會自動為每個已啟動的服務建立EJB端點。

**WSDL：**&#x200B;讓使用AEM Forms程式設計API開發的使用者端應用程式，能夠使用Web服務定義語言(WSDL)來呼叫服務。 「核心組態」頁面包含一個選項，可為AEM表單中的所有服務啟用WSDL產生。 (請參閱設定一般AEM表單設定)。

可以設定在Workbench中建立的&#x200B;**REST：**&#x200B;處理序，以便您可以透過代表性狀態轉移(REST)要求叫用它們。 從HTML頁面傳送REST要求。 也就是說，您可以使用REST要求，直接從網頁叫用AEM表單程式。

電子郵件、TaskManager、Watched資料夾及遠端端點只會公開服務的特定作業。 新增這些端點需要第二個設定步驟來選取呼叫服務的方法、設定設定引數，以及指定輸入和輸出引數對應。
