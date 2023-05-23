---
title: 為We.Finance參考站點的住房抵押工作流配置MicrosoftDynamics 365
seo-title: Configure Microsoft Dynamics 365 for the home mortgage workflow of the We.Finance reference site
description: 瞭解如何通過We.Finance參考網站的住房抵押工作流程的自適應表單來利用Microsoft® Dynamics 365服務
seo-description: Learn how to leverage the Microsoft® Dynamics 365 services through adaptive forms for the home mortgage workflow of the We.Finance Reference site
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# 為We.Finance參考站點的住房抵押工作流配置MicrosoftDynamics 365 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

瞭解如何通過We.Finance參考網站的住房抵押工作流程的自適應表單來利用Microsoft® Dynamics 365服務

## 概觀 {#overview}

Microsoft® Dynamics 365是一種客戶關係管理(CRM)和企業資源規劃(ERP)軟體，它為建立和管理客戶帳戶、聯繫人、銷售線索、機會和案例提供企業解決方案。

AEM Forms提供雲服務，將Dynamics 365與 [Forms資料整合](/help/forms/using/data-integration.md) 中。 在Microsoft® Dynamics方案中使用住房抵押應用程式演示之前，您需要配置Microsoft® Dynamics 365以與We.Finance參考站點一起使用。

## 必備條件 {#prerequisites}

在開始設定和配置Dynamics 365之前，請確保：

* AEM 6.3FormsService Pack 1及更高版本
* Microsoft® Dynamics 365帳戶
* 在Microsoft® Azure Active Directory中註冊Dynamics 365服務的應用程式
* 已註冊應用程式的客戶端ID和客戶端密鑰

## 將家庭抵押計算器與您的網站首頁連結 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 在作者實例上，轉到以下頁：

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 向下滾動到住房抵押計算器。
1. 選中右列（計算器）面板，然後點擊以顯示彈出菜單。 在彈出式菜單中，按一下「配置」。 將出現「編輯AEM Forms容器」對話框。

   ![計算器配置面板](assets/calculatorconfigurepanel.png)

1. 在「編輯AEM Forms集裝箱」對話框中，瀏覽資產路徑並選擇以下路徑中的家庭抵押計算器，然後點擊 **確認**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![選擇程式集路徑](assets/selectassetpath.png)

1. 點擊 **完成**。
1. 發佈已編輯的頁面。

   >[!NOTE]
   >
   >計算器欄位與FDM的綁定是通過We.Finance參考站點包預配置的。 要查看綁定，可以在創作模式下開啟表單並查看欄位綁定引用。

1. 要建立用於儲存住房抵押申請申請人記錄的自定義實體，請將AEMFormsFSIRefsite_1_0.zip解決方案包導入您的Microsoft® Dynamics實例：

   1. 從以下位置下載包：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 將解決方案包導入Microsoft® Dynamics實例。 在您的Microsoft® Dynamics實例中，轉到 **設定** > **解決方案** 然後點擊 **導入**。

1. 要設定refsite中使用的用戶聯繫人詳細資訊，請將Sarah Rose Contact.CSV包導入到您的Microsoft® Dynamics實例：

   1. 從以下位置下載包：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 將包導入您的Microsoft® Dynamics實例。 在您的Microsoft® Dynamics實例中，轉到 **銷售** > **聯繫人** 然後點擊 **導入資料**。
