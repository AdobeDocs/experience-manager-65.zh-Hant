---
title: 與Silverpop Engage整合
seo-title: 與Silverpop Engage整合
description: 瞭解如何將AEM與Silverpop Engage整合
seo-description: 瞭解如何將AEM與Silverpop Engage整合
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 1%

---


# 與Silverpop Engage整合{#integrating-with-silverpop-engage}

>[!NOTE]
>
>Silverpop整合是&#x200B;**not**&#x200B;的現成可用。 您必須從Package Share下載[Silverpop整合套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content)，並將它安裝在您的例項上。 安裝軟體包後，可以按照本文檔中的說明進行配置。

將AEM與Silverpop Engage整合後，您就可以透過Silverpop管理並傳送在AEM中建立的電子郵件。 它也可讓您透過AEM頁面上的AEM表單，使用Silverpop的銷售機會管理功能。

整合提供下列功能：

* 在AEM中建立電子郵件並發佈至Silverpop以進行散發的功能。
* 設定AEM表單動作以建立Silverpop訂閱者的能力。

在設定Silverpop Engage後，您可以將電子報或電子郵件發佈至Silverpop Engage。

## 建立Silverpop配置{#creating-a-silverpop-configuration}

Silverpop組態可透過&#x200B;**Cloudservices**、**Tools**&#x200B;或&#x200B;**API端點**&#x200B;新增。 本節將介紹所有方法。

### 透過Cloudservices {#configuring-silverpop-via-cloudservices}設定Silverpop

若要在Cloud Services中建立Silverpop設定：

1. 在AEM中，點選或按一下「工具&#x200B;**** > **部署** > **雲端服務**」。 （或直接存取`https://<hostname>:<port>/etc/cloudservices.html`。）
1. 在協力廠商服務下方，按一下「Silverop Engage」(**Silverop Engage)，然後按一下「Configure」（設定）。******「Silverpop」（銀色快顯）配置窗口隨即開啟。

   >[!NOTE]
   >
   >除非您從Package Share下載套件，否則Silverpop Engage不提供協力廠商服務下的選項。

1. 輸入標題和名稱（可選），然後按一下&#x200B;**建立**。 將開啟** Silverpop Settings**配置窗口。
1. 輸入用戶名、密碼，然後從下拉清單中選擇API端點。
1. 按一下&#x200B;**連接到Silverpop。** 成功連線後，您會看到成功對話方塊。按一下&#x200B;**OK**&#x200B;退出窗口。 您可以按一下&#x200B;**前往Silverpop Engage**，前往Silverpop。
1. 已設定Silverpop。 按一下&#x200B;**編輯**&#x200B;可編輯配置。
1. 此外，Silverpop Engage架構可透過提供標題和名稱（選用）來設定為個人化動作。 按一下「建立」將成功建立已設定之Silverpop連線的架構。

   匯入的資料擴充功能欄稍後可透過AEM元件- **文字與個人化**&#x200B;使用。

### 透過工具{#configuring-silverpop-via-tools}設定Silverpop

要在「工具」中建立Silverpop配置：

1. 在AEM中，點選或按一下「工具&#x200B;**** > **部署** > **雲端服務**」。 或者，直接前往`https://<hostname>:<port>/misadmin#/etc`導覽。
1. 選擇&#x200B;**工具**，然後選擇&#x200B;**雲端服務組態，**，然後選擇&#x200B;**Silverpop Engage**。
1. 按一下&#x200B;**新建**&#x200B;以開啟&#x200B;**建立頁面**&#x200B;窗口。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. 輸入&#x200B;**Title**&#x200B;和&#x200B;**Name**，然後按一下&#x200B;**Create**。
1. 按照上一步步驟4中的說明輸入配置資訊。 請依照該程式完成Silverpop的設定。

### 添加多個配置{#adding-multiple-configurations}

要添加多個配置：

1. 在歡迎頁面上，按一下「**雲端服務**」，然後按一下「Silverpop Engage **」。**&#x200B;按一下&#x200B;**顯示配置**&#x200B;按鈕，如果有一個或多個Silverpop配置可用，則該按鈕將顯示。 列出所有可用的配置。
1. 按一下「Available configurations（可用配置）」旁邊的&#x200B;**+**&#x200B;符號。 這將開啟&#x200B;**建立配置**&#x200B;窗口。 請依照先前的設定程式來建立新的設定。

### 設定API端點以連線至Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

目前，AEM有6個不安全的端點（Engage 1到6）。 Silverpop現在提供兩個新端點，並變更現有端點的連接端點。

若要設定API端點：

1. 前往`https://<hostname>:<port>/crxde.`上的`/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node`
1. 按一下右鍵並選擇&#x200B;**建立**，然後選擇&#x200B;**建立節點**。
1. 輸入&#x200B;**名稱**&#x200B;為`sp-e0`，然後選擇&#x200B;**類型**&#x200B;為`cq:Widget`。
1. 向新添加的節點添加兩個屬性：

   1. **名稱**: `text`，類 **型**: `String`, **值**:  `Engage 0`
   1. **名稱**: `value`，類 **型**: `String`, **值**:  `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   按一下「全部儲存」按鈕。

1. 再建立一個節點，其中&#x200B;**Name**&#x200B;為`sp-e7`,**Type**&#x200B;為`cq:Widget`。

   向新添加的節點添加兩個屬性：

   1. **名稱**: `text`，類 **型**: `String`, **值**:  `Pilot`
   1. **名稱**: `value`，類 **型**: `String`, **值**:  `https://apipilot.silverpop.com/XMLAPI`

1. 若要變更現有的API端點（參與1到6），請按一下每個端點並取代下列值：

   | **節點名稱** | **現有端點值** | **新端點值** |
   |---|---|---|
   | sp-e1 | https://api.engage1.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. 按一下&#x200B;**保存全部**。 AEM現在已準備好透過安全端點連線至Silverpop。

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)

