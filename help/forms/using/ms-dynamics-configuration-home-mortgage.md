---
title: 為We.Finance參考網站的住房抵押工作流程配置Microsoft Dynamics 365
seo-title: 為We.Finance參考網站的住房抵押工作流程配置Microsoft Dynamics 365
description: Learn how to leverage the Microsoft® Dynamics 365 services through adaptive forms for the home mortgage workflow of the We.Finance Reference site
seo-description: Learn how to leverage the Microsoft® Dynamics 365 services through adaptive forms for the home mortgage workflow of the We.Finance Reference site
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
translation-type: tm+mt
source-git-commit: f323b490c37effc3cbb36c793b62fa788eca9545

---


# Configure Microsoft Dynamics 365 for the home mortgage workflow of the We.Finance reference site {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

Learn how to leverage the Microsoft® Dynamics 365 services through adaptive forms for the home mortgage workflow of the We.Finance Reference site

## 概覽 {#overview}

Microsoft® Dynamics 365 is a Customer Relationship Management (CRM) and Enterprise Resource Planning (ERP) software that provides enterprise solutions for creating and managing customer accounts, contacts, leads, opportunities, and cases.

AEM Forms provides a cloud service to integrate Dynamics 365 with [Forms Data Integration](/help/forms/using/data-integration.md) module. The scenario [Home Mortgage application walkthrough with Microsoft® Dynamics](/help/forms/using/finance-reference-site-walkthrough.md#home-mortgage-application-walkthrough-with-microsoft-dynamics) showcases how a customer uses the We.Finance reference site to apply for a loan when the site is using Microsoft® Dynamics for Forms Data Integration. Before you can use the Home Mortgage application walkthrough with Microsoft® Dynamics scenario, you need to configure Microsoft® Dynamics 365 to be used with the We.Finance reference site.

## 必備條件 {#prerequisites}

Before you begin to set up and configure Dynamics 365, ensure that you have:

* [Set up and configure AEM Forms reference sites](/help/forms/using/setup-reference-sites.md).

* AEM 6.3 Forms Service Pack 1 and later
* Microsoft® Dynamics 365 account
* Registered application for Dynamics 365 service with Microsoft® Azure Active Directory
* Client ID and client secret for the registered application

## 將首頁抵押電腦與您的網站首頁連結 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. On the author instance, go to the following page:

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. Scroll down to the Home Mortgage Calculator.
1. Highlight the right column&#39;s (calculator&#39;s) panel and tap to display the pop-up menu. In the pop-up menu, tap Configure. The Edit AEM Forms Container dialog appears.

   ![計算器配置面板](assets/calculatorconfigurepanel.png)

1. In the Edit AEM Forms Container dialog, browse the asset path and select home-mortgage-calculator at the following path and tap **Confirm**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 點選「 **完成**」。
1. Publish the edited page.

   >[!NOTE]
   >
   >The binding of the calculator fields with the FDM is preconfigured through the We.Finance reference site package. To view the binding, you can open the form in the authoring mode and see the field bind references.

1. To create a custom entity for storing applicant record for home mortgage application, import the AEMFormsFSIRefsite_1_0.zip solution package to your Microsoft® Dynamics instance:

   1. 從以下網址下載套件：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 將解決方案套件匯入Microsoft® Dynamics實例。 在您的Microsoft® Dynamics例項中，前往「設 **定** >解決 **方案** 」 **，然後點選「**&#x200B;匯入」。

1. 若要設定refsite中使用的使用者連絡資訊，請將Sarah Rose Contact.CSV套件匯入您的Microsoft® Dynamics例項：

   1. 從以下網址下載套件：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 將套件匯入至您的Microsoft® Dynamics例項。 在您的Microsoft® Dynamics例項中，前往「銷 **售** > **連絡人** 」 **，然後點選「匯**&#x200B;入資料」。

