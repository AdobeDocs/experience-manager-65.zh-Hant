---
title: 端點類型
seo-title: 端點類型
description: 瞭解不同類型的端點。
seo-description: 瞭解不同類型的端點。
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# 端點類型{#types-of-endpoints}

必須先配置並啟用端點，才能使用服務。 端點指定如何調用服務。

>[!NOTE]
>
>在Workbench中，端點稱為起點。

可以將下列類型的端點添加到服務中。 並非所有服務都支援所有端點：

**電子郵件：** 透過傳送內含一或多個檔案附件的電子郵件至指定的電子郵件帳戶，讓使用者可叫用服務。在設定電子郵件端點之前，您必須設定所需的電子郵件帳戶。 （請參閱設定電子郵件端點。）

**監視資料夾：** 讓使用者將檔案置於資料夾中，以定義的間隔掃描，以叫用服務。（請參閱設定監看的資料夾端點。）

**TaskManager：使** 工作區用戶能夠調用服務。

**Remoting：啟** 用以Flex建立的應用程式，以使用（AEM表單已過時）AEM Forms Remoting叫用服務。系統會為每個激活的服務自動建立遠程端點。 建立的Flex目標與端點名稱相同，而Flex用戶端可建立指向此目標的遠端物件，以叫用相關服務的作業。

**SOAP：啟** 用使用AEM表單程式設計API開發的用戶端應用程式，以使用SOAP模式叫用服務。系統會為每個已激活的服務自動建立SOAP端點。

**注意**: *當在Adobe Acrobat或Adobe Reader中檢視檔案時，使用SOAP端點時，可從檔案安全性檔案中移除安全性。有關如何在LCRM文檔上禁用SOAP端點的詳細資訊，請參閱[為文檔安全文檔禁用SOAP端點](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB：啟** 用使用AEM Forms寫程式API開發的客戶端應用程式，以使用Enterprise JavaBeans(EJB)模式調用服務。系統會為每個激活的服務自動建立一個EJB端點。

**WSDL：啟** 用使用AEM表單程式設計API開發的用戶端應用程式，以使用網站服務定義語言(WSDL)來叫用服務。「核心設定」頁面包含一個選項，可針對屬於AEM表單一部分的所有服務啟用WSDL產生。 （請參閱「設定一般AEM表單設定」）。

**REST：在** Workbench中建立的流程可以進行配置，以便通過「代表性狀態轉移(REST)」請求調用它們。REST請求是從HTML頁面傳送。 也就是說，您可以使用REST請求，直接從網頁叫用AEM表單程式。

電子郵件、TaskManager、Watched資料夾和Remoting端點僅顯示服務的特定操作。 添加這些端點需要第二個配置步驟來選擇調用服務、設定配置參數以及指定輸入和輸出參數映射的方法。
