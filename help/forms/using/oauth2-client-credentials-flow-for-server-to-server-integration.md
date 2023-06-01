---
title: 使用OAuth 2.0使用者端憑證流程與AEM Forms整合Salesforce
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: 使用OAuth 2.0使用者端憑證流程整合Salesforce與AEM Forms的步驟
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
source-git-commit: f03513c98455e00beef37819a5a47ba56dfa5028
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 使用OAuth 2.0使用者端憑證流程整合Salesforce  {#configure-salesforce-with-ouath-2.0-client-credential}

若要將AEM Forms與Salesforce應用程式整合，則會使用OAuth 2.0使用者端憑證流程。 這是一種標準化和安全的直接通訊方法，使用者無需參與。 在此流程中，使用者端應用程式(AEM Form)會交換Salesforce連線應用程式中定義的使用者端憑證，以取得存取權杖。 必要的使用者端憑證包括使用者金鑰和使用者密碼。

## 使用OAuth 2.0使用者端憑證流程整合Salesforce與AEM Forms的優點 {#advantages-of-integrating-saleforce-aemforms}

除了OAuth 2.0使用者端憑證流程外，AEM Forms還支援Salesforce與授權代碼流程的整合。 在OAuth 2.0授權代碼流程中，使用者端應用程式(AEM Forms)會代表Salesforce使用者取得資源存取權，但有一些限制：

* 每個使用者最多允許五個連線。 進一步的連線會自動撤銷較舊的連線。
* 如果使用者停用、失去存取權或更新密碼，AEM資料來源設定會停止運作。

## 必備條件 {#prerequisites}

若要在Salesforce和AEM環境之間擷取和擷取資料，請先符合某些先決條件，才能繼續進行：

+++ **使用使用者端憑證流程和僅限API的使用者設定Saleforce連線的應用程式**

您必須使用OAuth 2.0使用者端憑證流程為貴組織建立具有API專用使用者的Salesforce連線應用程式。 如需詳細步驟，請參閱文章 [用於伺服器對伺服器整合的OAuth 2.0使用者端憑證流程](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5). 這些步驟可協助您取得使用者金鑰和使用者密碼。

>[!NOTE]
>
> 建立AEM資料來源設定時，請務必記下必要的使用者金鑰和使用者機密。

+++

+++ **建立Swagger檔案**

Swagger是一組開放原始碼的規則、規格和工具，用於開發和描述RESTful API。 [建立Swagger檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) 將Salesforce與AEM Forms整合之前。

    >[！NOTE]
    >
    > AEM 6.5僅支援Swagger 2.0檔案規格。

+++

## 使用使用者端憑證設定Salesforce的步驟 {#steps-to-create-aem-datasource-configuration}

1. 登入您的Author執行個體。
1. 前往 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 資料來源]**.
1. 選取設定資料夾。
1. 按一下 **[!UICONTROL 建立]** 和 **[!UICONTROL 建立資料來源組態]** 出現。
1. 指定 **[!UICONTROL 標題]** 並選取 **[!UICONTROL 服務型別]** 作為 **[!UICONTROL RESTful服務]**.
1. 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 選取 **[!UICONTROL Swagger來源]** 作為 **[!UICONTROL 檔案].**
   >[!NOTE]
   >
   > 選取swagger檔案之後，就會自動填入「配置」、「主機名稱」和「基底」路徑。

1. 按一下「 」，從本機電腦上傳已建立的Swagger檔案 **[!UICONTROL 瀏覽]**.
1. 選取 **[!UICONTROL 驗證型別]** 作為 **[!UICONTROL OAuth 2.0]** 和 **[!UICONTROL 驗證設定]** 面板隨即顯示。
1. 選取 **[!UICONTROL 授權型別]** 作為 **[!UICONTROL 使用者端認證]**.
1. 指定 **[!UICONTROL 使用者端ID]** 和 **[!UICONTROL 使用者端密碼]** 從Salesforce連線應用程式取得。
1. 指定 **[!UICONTROL 存取權杖URL]** 格式
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 每個組織都有其專屬的網域名稱。

1. 按一下 **[!UICONTROL 測試連線]**.
1. 如果連線成功，請按一下 **[!UICONTROL 建立]** 按鈕。

現在，您可以 [建立表單資料模型](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) 將設定的資料來源與您的調適型表單整合。


