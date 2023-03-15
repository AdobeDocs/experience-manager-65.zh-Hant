---
title: 為We.Finance參考網站的住房抵押工作流程設定Microsoft Dynamics 365
seo-title: Configure Microsoft Dynamics 365 for the home mortgage workflow of the We.Finance reference site
description: 了解如何透過We.Finance Reference網站的適用性表單，運用Microsoft® Dynamics 365服務進行家庭抵押工作流程
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

# 為We.Finance參考網站的住房抵押工作流程設定Microsoft Dynamics 365 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

了解如何透過We.Finance Reference網站的適用性表單，運用Microsoft® Dynamics 365服務進行家庭抵押工作流程

## 概觀 {#overview}

Microsoft® Dynamics 365是一種客戶關係管理(CRM)和企業資源規劃(ERP)軟體，提供企業解決方案，用於建立和管理客戶帳戶、聯繫人、銷售機會、銷售機會和案例。

AEM Forms提供雲端服務，以整合Dynamics 365與 [Forms資料整合](/help/forms/using/data-integration.md) 模組。 在使用Microsoft® Dynamics案例的住房抵押貸款應用程式逐步說明之前，您需要將Microsoft® Dynamics 365設定為與We.Finance參考網站搭配使用。

## 必備條件 {#prerequisites}

開始設定和配置Dynamics 365之前，請確保您有：

* AEM 6.3 Forms Service Pack 1及更新版本
* Microsoft® Dynamics 365帳戶
* 使用Microsoft® Azure Active Directory註冊的Dynamics 365服務應用程式
* 註冊應用程式的用戶端ID和用戶端密碼

## 將首頁抵押計算器與您的網站首頁連結 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 在製作例項上，前往下列頁面：

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 向下捲動至「Home Mortage Calculator（住房抵押計算器）」。
1. 選中右列（計算器）面板，然後點選以顯示彈出菜單。 在快顯功能表中，點選「設定」。 「編輯AEM Forms容器」對話方塊隨即出現。

   ![calculatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. 在「編輯AEM Forms容器」對話方塊中，瀏覽資產路徑，然後在下列路徑選取住宅抵押計算器，然後點選 **確認**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 點選 **完成**.
1. 發佈已編輯的頁面。

   >[!NOTE]
   >
   >計算器欄位與FDM的綁定是通過We.Finance參考站點包預配置的。 要查看綁定，可以在創作模式下開啟表單，並查看欄位綁定引用。

1. 若要建立自訂實體以儲存申請住房抵押申請的申請者記錄，請將AEMFormsFSIRefsite_1_0.zip解決方案套件匯入您的Microsoft® Dynamics例項：

   1. 從以下網址下載套件：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 將解決方案套件匯入Microsoft® Dynamics執行個體。 在您的Microsoft® Dynamics例項中，前往 **設定** > **解決方案** 然後點選 **匯入**.

1. 若要設定重新整理中使用的使用者聯絡資訊，請將Sarah Rose Contact.CSV套件匯入至您的Microsoft® Dynamics例項：

   1. 從以下網址下載套件：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 將套件匯入您的Microsoft® Dynamics例項。 在您的Microsoft® Dynamics例項中，前往 **銷售** > **聯繫人** 然後點選 **匯入資料**.
