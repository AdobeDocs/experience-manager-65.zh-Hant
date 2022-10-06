---
title: 端點類型
seo-title: Types of endpoints
description: 了解不同類型的端點。
seo-description: Learn about the different types of endpoints.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 端點類型 {#types-of-endpoints}

您必須先設定並啟用端點，才能使用服務。 端點指定如何調用服務。

>[!NOTE]
>
>在Workbench中，端點稱為起點。

可以向服務添加以下類型的端點。 並非所有服務都支援所有端點：

**電子郵件：** 通過向指定的電子郵件帳戶發送包含一個或多個檔案附件的電子郵件消息，使用戶能夠調用服務。 設定電子郵件端點之前，您必須設定必要的電子郵件帳戶。 （請參閱設定電子郵件端點。）

**觀看的資料夾：** 將檔案放在資料夾中，以定義的間隔掃描，使用戶能夠調用服務。 （請參閱設定觀看的資料夾端點）。

**任務管理器：** 使工作區使用者能叫用服務。

**遠程：** 啟用以Flex建置的應用程式，以使用(AEM forms為過時)AEM forms Remoting叫用服務。 系統會自動為每個已激活的服務建立遠程端點。 建立與端點同名的Flex目的地，Flex用戶端可建立指向此目的地的遠端物件，以叫用相關服務上的作業。

**SOAP:** 使用AEM表單寫程式API開發的用戶端應用程式能夠使用SOAP模式調用服務。 系統會自動為每個已激活的服務建立SOAP端點。

**附註**: *在Adobe Acrobat或Adobe Reader中檢視檔案時使用SOAP端點時，可從檔案安全性檔案中移除安全性。 有關如何禁用LCRM文檔上的SOAP引數的詳細資訊，請參見 [禁用文檔安全文檔的SOAP端點](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** 使用AEM Forms寫程式API開發的客戶端應用程式能夠使用企業JavaBeans(EJB)模式調用服務。 系統會自動為每個激活的服務建立一個EJB端點。

**WSDL:** 允許使用AEM表單寫程式API開發的客戶端應用程式使用Web服務定義語言(WSDL)調用服務。 「核心配置」頁包含一個選項，用於為屬於AEM表單的所有服務啟用WSDL生成。 (請參閱設定一般AEM表單設定。)

**休息：** 可在Workbench中建立的程式可進行設定，以便您能透過「代表性狀態轉移(REST)」請求來叫用這些程式。 REST要求會從HTML頁面傳送。 也就是說，您可以使用REST要求直接從網頁叫用AEM表單程式。

電子郵件、TaskManager、Watched Folder和Remoteing端點僅顯示服務的特定操作。 添加這些端點需要第二個配置步驟來選擇調用服務的方法、設定配置參數以及指定輸入和輸出參數映射。
