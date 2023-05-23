---
title: 與Silverpop Engage整合
seo-title: Integrating with Silverpop Engage
description: 瞭解如何與Silverpop AEM Engage整合
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# 與Silverpop Engage整合{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. You must download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

與Silverpop AEM Engage整合後，您可以管理和發送通過Silverpop建立的AEM電子郵件。 它還允許您通過頁面上的表單使用Silverpop的AEM線索管AEM理功能。

該整合提供了以下功能：

* 在中建立電子郵件並AEM將其發佈到Silverpop以供分發。
* 設定表單操作以創AEM建Silverpop訂戶的能力。

配置Silverpop Engage後，您可以將新聞稿或電子郵件發佈到Silverpop Engage。

## 建立Silverpop配置 {#creating-a-silverpop-configuration}

Silverpop配置可通過 **Cloud Services**。 **工具**&#x200B;或 **API端點**。 本節介紹了所有方法。

### 通過Cloud Services配置Silverpop {#configuring-silverpop-via-cloudservices}

要在Cloud Services中建立Silverpop配置：

1. 在AEM中，點擊或按一下 **工具** > **部署** > **Cloud Services**。 (或直接訪問 `https://<hostname>:<port>/etc/cloudservices.html`。)
1. 在第三方服務下，按一下 **《銀翼戰士》** 然後 **配置**。 將開啟Silverpop配置窗口。

   >[!NOTE]
   >
   >除非您從包共用下載包，否則第三方服務下的Silverpop Engage不可用。

1. 輸入標題，或者輸入名稱，然後按一下 **建立**。 ** Silverpop Settings**配置窗口開啟。
1. 輸入用戶名、密碼，然後從下拉清單中選擇API終結點。
1. 按一下 **連接到Silverpop。** 成功連接後，將看到「成功」對話框。 按一下 **確定** 所以你就離開窗戶。 通過按一下 **轉到Silverpop Engage**。
1. 已配置Silverpop。 可通過按一下 **編輯**。
1. 此外，還可通過提供標題和名稱（可選）為個性化操作配置Silverpop Engage框架。 按一下建立成功為已配置的Silverpop連接建立框架。

   導入的資料擴展列稍後可通過元件AEM使用 —  **文本和個性化**。

### 通過工具配置Silverpop {#configuring-silverpop-via-tools}

要在工具中建立Silverpop配置：

1. 在AEM中，點擊或按一下 **工具** > **部署** > **Cloud Services**。 或者直接通過 `https://<hostname>:<port>/misadmin#/etc`。
1. 選擇 **工具**，則 **Cloud Services配置，** 然後 **《銀色遊戲》**。
1. 按一下 **新建**。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. 在 **建立頁** ，輸入 **標題** （可選） **名稱**，然後按一下 **建立**。
1. 輸入上一步驟4中概述的配置資訊。 按照此過程完成Silverpop的配置。

### 添加多個配置 {#adding-multiple-configurations}

要添加多個配置：

1. 在歡迎頁面上，按一下 **Cloud Services** 按一下 **《銀色遊戲》**。 按一下 **顯示配置** 按鈕。 列出所有可用配置。
1. 按一下 **+** 在「Available configurations（可用配置）」旁邊登錄。 開啟 **建立配置** 的子菜單。 按照上一配置過程建立配置。

### 配置API端點以連接到Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

目前，AEM有6個無擔保的端點(1 - 6)。 Silverpop現在提供兩個新端點，並為現有端點更改了連接端點。

配置API端點：

1. 轉到 `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` 上 `https://<hostname>:<port>/crxde.`
1. 按一下右鍵並選擇 **建立**，則 **建立節點**。
1. 輸入 **名稱** 如 `sp-e0` 選擇 **類型** 如 `cq:Widget`。
1. 向新添加的節點添加兩個屬性：

   1. **名稱**: `text`。 **類型**: `String`。 **值**: `Engage 0`
   1. **名稱**: `value`。 **類型**: `String`。 **值**: `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   按一下「全部保存」。

1. 使用 **名稱** 如 `sp-e7` 和 **類型** 如 `cq:Widget`。

   向新添加的節點添加兩個屬性：

   1. **名稱**: `text`。 **類型**: `String`。 **值**: `Pilot`
   1. **名稱**: `value`。 **類型**: `String`。 **值**: `https://apipilot.silverpop.com/XMLAPI`

1. 要更改現有API端點(Engage 1 - 6)，請逐個按一下每個端點並按如下方式替換這些值：

   | **節點名稱** | **現有端點值** | **新端點值** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. 按一下 **全部保存**。 現在AEM已準備好通過安全端點連接到Silverpop。

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
