---
title: 為We.Finance參考網站的住房抵押工作流程配置Microsoft Dynamics 365
seo-title: 為We.Finance參考網站的住房抵押工作流程配置Microsoft Dynamics 365
description: 瞭解如何透過We.Finance參考網站的住房抵押工作流程調整表單，運用Microsoft® Dynamics 365服務
seo-description: 瞭解如何透過We.Finance參考網站的住房抵押工作流程調整表單，運用Microsoft® Dynamics 365服務
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# 為We.Finance參考網站的住房抵押工作流程配置Microsoft Dynamics 365 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

瞭解如何透過We.Finance參考網站的住房抵押工作流程調整表單，運用Microsoft® Dynamics 365服務

## 概覽 {#overview}

Microsoft® Dynamics 365是客戶關係管理(CRM)和企業資源規劃(ERP)軟體，提供企業解決方案，以建立和管理客戶帳戶、聯絡人、潛在客戶、商機和案例。

AEM Forms提供雲端服務，可將Dynamics 365與 [Forms Data Integration](/help/forms/using/data-integration.md) 模組整合。 Microsoft® Dynamics [(Microsoft® Dynamics](/help/forms/using/finance-reference-site-walkthrough.md#home-mortgage-application-walkthrough-with-microsoft-dynamics) )的「家庭抵押」應用程式範例將示範當客戶使用Microsoft® Dynamics forms Data Integration時，如何使用We.Finance參考網站申請貸款。 在Microsoft® Dynamics案例中使用「家庭抵押」應用程式逐步說明之前，您必須設定Microsoft® Dynamics 365，以便與We.Finance參考網站搭配使用。

## 必備條件 {#prerequisites}

在開始設定和設定Dynamics 365之前，請確定您已：

* [設定和設定AEM Forms參考網站](/help/forms/using/setup-reference-sites.md)。

* AEM 6.3 Forms Service Pack 1和更新版本
* Microsoft® Dynamics 365帳戶
* Microsoft® Azure Active Directory的Dynamics 365服務註冊應用程式
* 註冊應用程式的用戶端ID和用戶端密碼

## 將首頁抵押電腦與您的網站首頁連結 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 在作者例項上，請前往下列頁面：

   https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html

1. 向下捲動至「房屋抵押計算器」。
1. 選中右欄的（計算器）面板，點選以顯示快顯功能表。 在彈出式選單中，點選「設定」。 此時會顯示「編輯AEM Forms容器」對話方塊。

   ![計算器配置面板](assets/calculatorconfigurepanel.png)

1. 在「編輯AEM Forms容器」對話方塊中，瀏覽資產路徑，並在下列路徑選取家庭抵押計算器，然後點選「確 **認**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 點選「 **完成**」。
1. 發佈已編輯的頁面。

   >[!NOTE]
   >
   >計算器欄位與FDM的綁定是通過We.Finance參考站點包預配置的。 若要檢視系結，您可以在編寫模式中開啟表單，並查看欄位系結參考。

1. 若要建立自訂實體，以儲存房屋抵押申請的申請人記錄，請將AEMFormsFSIRefsite_1_0.zip解決方案套件匯入您的Microsoft® Dynamics例項：

   1. 從以下網址下載套件：

      `https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 將解決方案套件匯入Microsoft® Dynamics實例。 在您的Microsoft® Dynamics例項中，前往「設 **定** >解決 **方案** 」 **，然後點選「**&#x200B;匯入」。

1. 若要設定refsite中使用的使用者連絡資訊，請將Sarah Rose Contact.CSV套件匯入您的Microsoft® Dynamics例項：

   1. 從以下網址下載套件：

      `https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 將套件匯入至您的Microsoft® Dynamics例項。 在您的Microsoft® Dynamics例項中，前往「銷 **售** > **連絡人** 」 **，然後點選「匯**&#x200B;入資料」。

