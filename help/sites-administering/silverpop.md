---
title: 與Silverpop Engage整合
description: 瞭解如何將Adobe Experience Manager與Silverpop Engage整合。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# 與Silverpop Engage整合{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. Download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

將AEM與Silverpop Engage整合可讓您透過Silverpop管理及傳送在AEM中建立的電子郵件。 它也可讓您透過AEM頁面上的AEM Forms使用Silverpop的潛在客戶管理功能。

整合提供您下列功能：

* 能夠在AEM中建立電子郵件，並將其發佈至Silverpop進行發佈。
* 可設定AEM表單的動作以建立Silverpop訂閱者。

設定Silverpop Engage後，您可以將電子報或電子郵件發佈至Silverpop Engage。

## 建立Silverpop設定 {#creating-a-silverpop-configuration}

可透過&#x200B;**Cloud Service**、**工具**&#x200B;或&#x200B;**API端點**&#x200B;新增Silverpop設定。 本節將說明所有方法。

### 透過Cloud Service設定Silverpop {#configuring-silverpop-via-cloudservices}

若要在Cloud Service中建立Silverpop設定：

1. 在AEM中，按一下&#x200B;**工具** > **部署** > **Cloud Service**。 （或直接在`https://<hostname>:<port>/etc/cloudservices.html`存取。）
1. 在協力廠商服務底下，按一下&#x200B;**Silverop Engage**，然後按&#x200B;**設定**。 Silverpop設定視窗隨即開啟。

   >[!NOTE]
   >
   >除非您從Package Share下載套件，否則Silverpop Engage不提供協力廠商服務選項。

1. 輸入標題，並選擇性地輸入名稱，然後按一下&#x200B;**建立**。 隨即開啟** Silverpop設定**設定視窗。
1. 輸入使用者名稱和密碼，然後從下拉式清單中選取API端點。
1. 按一下&#x200B;**連線到Silverpop。**&#x200B;當您成功連線時，您會看到成功對話方塊。 按一下&#x200B;**確定**&#x200B;以結束視窗。 您可以按一下&#x200B;**移至Silverpop Engage**，移至Silverpop。
1. Silverpop已設定。 您可以按一下&#x200B;**編輯**&#x200B;來編輯組態。
1. 此外，Silverpop Engage架構可提供標題和名稱（選用），以設定個人化動作。 按一下「建立」，成功為已設定的Silverpop連線建立架構。

   匯入的資料延伸欄稍後可透過AEM元件 — **文字和Personalization**&#x200B;使用。

### 透過工具設定Silverpop {#configuring-silverpop-via-tools}

若要在工具中建立Silverpop設定：

1. 在AEM中，按一下&#x200B;**工具** > **部署** > **Cloud Service**。 或前往`https://<hostname>:<port>/misadmin#/etc`直接導覽至該處。
1. 選取&#x200B;**Tools**，然後選取&#x200B;**Cloud Service組態，**，再選取&#x200B;**Silverpop Engage**。
1. 按一下&#x200B;**新增**。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. 在&#x200B;**建立頁面**&#x200B;視窗中，輸入&#x200B;**標題**，並選擇性地輸入&#x200B;**名稱**，然後按一下&#x200B;**建立**。
1. 依照前一個程式中的步驟4輸入組態資訊。 請依照該程式進行，以便完成Silverpop的設定。

### 新增多個組態 {#adding-multiple-configurations}

若要新增多個組態：

1. 在歡迎頁面上，按一下&#x200B;**Cloud Service**&#x200B;並按一下&#x200B;**Silverpop Engage**。 按一下&#x200B;**顯示設定**&#x200B;按鈕，如果有一或多個Silverpop設定可用，就會顯示這個按鈕。 列出所有可用的設定。
1. 按一下「可用組態」旁的&#x200B;**+**&#x200B;符號。 它會開啟&#x200B;**建立組態**&#x200B;視窗。 請遵循之前的組態程式，以便建立組態。

### 設定API端點以連線至Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

目前，AEM有六個不安全的端點（參與1 - 6）。 Silverpop現在為現有端點提供兩個新端點及已變更的連線端點。

若要設定API端點：

1. 移至`https://<hostname>:<port>/crxde.`上的`/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node`
1. 按一下滑鼠右鍵並選取&#x200B;**建立**，然後選取&#x200B;**建立節點**。
1. 輸入&#x200B;**名稱**&#x200B;作為`sp-e0`，並選擇&#x200B;**型別**&#x200B;作為`cq:Widget`。
1. 將兩個屬性新增至新新增的節點：

   1. **名稱**： `text`，**型別**： `String`，**值**： `Engage 0`
   1. **名稱**： `value`，**型別**： `String`，**值**： `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   按一下「儲存全部」。

1. 以&#x200B;**Name**&#x200B;為`sp-e7`，**Type**&#x200B;為`cq:Widget`再建立一個節點。

   將兩個屬性新增至新新增的節點：

   1. **名稱**： `text`，**型別**： `String`，**值**： `Pilot`
   1. **名稱**： `value`，**型別**： `String`，**值**： `https://apipilot.silverpop.com/XMLAPI`

1. 若要變更現有的API端點（參與1 - 6），請逐一按一下每個端點，然後以下列方式取代值：

   | **節點名稱** | **現有的端點值** | **新端點值** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. 按一下&#x200B;**全部儲存**。 AEM現在已準備好透過安全的端點連線至Silverpop。

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
