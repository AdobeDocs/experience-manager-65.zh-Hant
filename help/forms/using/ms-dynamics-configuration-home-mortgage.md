---
title: 設定Microsoft Dynamics 365，以用於We.Finance參考網站的住房抵押貸款工作流程
description: 瞭解如何透過最適化表單針對We.Finance參考網站的住房抵押貸款工作流程使用Microsoft&reg； Dynamics 365服務。
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Foundation Components
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 設定Microsoft Dynamics 365，以用於We.Finance參考網站的住房抵押貸款工作流程 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

瞭解如何透過最適化表單針對We.Finance參考網站的住房抵押貸款工作流程使用Microsoft® Dynamics 365服務

## 概觀 {#overview}

Microsoft® Dynamics 365是客戶關係管理(CRM)和企業資源規劃(ERP)軟體，提供企業解決方案來建立和管理客戶帳戶、聯絡人、銷售機會、商機和案例。

AEM Forms提供雲端服務，將Dynamics 365與整合 [Forms資料整合](/help/forms/using/data-integration.md) 模組。 您必須先設定Microsoft® Dynamics 365，以與We.Finance參考網站搭配使用，才能透過Microsoft® Dynamics案例使用Home Mortgage應用程式逐步說明。

## 先決條件 {#prerequisites}

開始設定和設定Dynamics 365之前，請確定您擁有：

* AEM 6.3 Forms Service Pack 1及更新版本
* Microsoft® Dynamics 365帳戶
* 已向Microsoft® Azure Active Directory註冊Dynamics 365服務的應用程式
* 已註冊應用程式的使用者端ID和使用者端密碼

## 將住房抵押貸款電腦與您的網站首頁連結 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 在編寫執行個體上，前往以下頁面：

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 向下捲動至「住房抵押貸款電腦」。
1. 反白右欄的（電腦）面板，並選取以顯示快顯功能表。 在躍現式選單中，選取「設定」。 便會顯示「編輯AEM Forms容器」對話方塊。

   ![calculatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. 在「編輯AEM Forms容器」對話方塊中，瀏覽資產路徑並在以下路徑選取home-mortgage-calculator並選取 **確認**：

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. 選取「**完成**」。
1. 在編輯的頁面上Publish。

   >[!NOTE]
   >
   >計算器欄位與FDM的繫結是透過We.Finance參考站台套件預先設定。 若要檢視繫結，您可以在撰寫模式中開啟表單，並檢視欄位繫結參考。

1. 若要建立自訂實體來儲存房屋抵押貸款申請者的申請記錄，請將AEMFormsFSIRefsite_1_0.zip解決方案套件匯入您的Microsoft® Dynamics執行個體：

   1. 從以下位置下載套件：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 將解決方案套件匯入至Microsoft® Dynamics執行個體。 在您的Microsoft® Dynamics執行個體中，前往 **設定** > **解決方案** 然後選取 **匯入**.

1. 若要設定重新網站中使用的使用者聯絡詳細資訊，請將Sarah Rose Contact.CSV套件匯入您的Microsoft® Dynamics執行個體：

   1. 從以下位置下載套件：

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 將套件匯入您的Microsoft® Dynamics執行個體。 在您的Microsoft® Dynamics執行個體中，前往 **銷售** > **連絡人** 然後選取 **匯入資料**.
