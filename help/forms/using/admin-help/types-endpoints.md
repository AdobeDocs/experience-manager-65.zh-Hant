---
title: 端點類型
seo-title: Types of endpoints
description: 瞭解不同類型的端點。
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

在使用服務之前，必須配置並啟用終結點。 終結點指定如何調用服務。

>[!NOTE]
>
>在Workbench中，端點稱為起始點。

可以向服務添加以下類型的端點。 並非所有服務都支援所有終結點：

**電子郵件：** 允許用戶通過向指定的電子郵件帳戶發送包含一個或多個檔案附件的電子郵件來調用服務。 在配置電子郵件終結點之前，必須配置所需的電子郵件帳戶。 （請參閱配置電子郵件終結點。）

**監視資料夾：** 允許用戶通過將檔案放置在資料夾中來調用服務，該資料夾以定義的間隔被掃描。 （請參閱配置監視的資料夾終結點。）

**任務管理器：** 使Workspace用戶能夠調用服務。

**遠程處理：** 使用Flex構建的應用程式能夠使用（表單棄用）AEM表單遠AEM程調用服務。 為每個激活的服務自動建立遠程處理終結點。 建立與終結點同名的Flex目標，Flex客戶端可以建立指向此目標以調用相關服務上的操作的遠程對象。

**SOAP:** 使用表單寫程式API開AEM發的客戶端應用程式能夠使用SOAP模式調用服務。 為每個激活的服務自動建立SOAP終結點。

**附註**: *當在Adobe Acrobat或Adobe Reader查看文檔時使用SOAP端點時，可以從文檔安全文檔中刪除安全性。 有關如何在LCRM文檔上禁用SOAP引點的詳細資訊，請參見 [禁用文檔安全文檔的SOAP終結點](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** 使用Forms寫程式API開發的客AEM戶端應用程式能夠使用Enterprise JavaBeans(EJB)模式調用服務。 會為每個激活的服務自動建立EJB終結點。

**WSDL:** 使用表單寫程式API開AEM發的客戶端應用程式能夠使用Web服務定義語言(WSDL)調用服務。 「核心配置」頁包含一個選項，用於為屬於表單一部分的所有服務啟用WSDLAEM生成。 (請參閱配置一AEM般表單設定。)

**休息：** 可以配置在Workbench中建立的流程，以便您可以通過表示狀態轉移(REST)請求調用這些流程。 REST請求從HTML頁發送。 即，您可以使用REST請AEM求從網頁直接調用表單進程。

電子郵件、TaskManager、監視資料夾和遠程處理終結點只顯示服務的特定操作。 添加這些端點需要第二個配置步驟來選擇調用服務、設定配置參數以及指定輸入和輸出參數映射的方法。
