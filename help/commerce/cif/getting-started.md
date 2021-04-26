---
title: 內容與商AEM務快速入門
description: 瞭解如何部署內AEM容與商務專案。
topics: Commerce
feature: 商務整合框架
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: 8ead3d1b24177effa4d40141408c5676eaabcc30
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# 內容與商AEM務快速入門{#start}

若要開始使AEM用「內容與商務」，您必須安裝AEMContent and Commerce Add-On for AEM 6.5。

## 最低軟體需求

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7或更新版本為必填項目。

## 入門 {#onboarding}

「內容與AEM商務」的登入程式分為兩步：

1. 安裝AEMContent and Commerce Add-On for AEM 6.5

2. 與您的AEM商務解決方案連絡

### 安裝AEMContent and Commerce add-on for AEM 6.5

從[軟AEM體散發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)入口網站下載並安AEM裝適用於6.5的Commerce Add-On。

啟動並安裝所需AEM的6.5 Service Pack。 我們建議安裝最後一個可用的Service Pack。

    >[!NOTE]
    >
    >由CSE為受管理服務客戶AEM完成。

### 連AEM線至您的商務系統

可連AEM接到任何具有可訪問GraphQL端點的商務系AEM統。 這些端點通常可以公開使用，也可以通過專用VPN或本地連接來連接，具體取決於單個項目設定。

可選地，可以提供驗證頭以使用需要驗證的附加CIF功能。

必須調整[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)和[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)（已包含在[預設配置](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)中）生成的項目。

將`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中的`url`值替換為商務系統的GraphQL端點。 此設定可透過OSGI主控台完成，或透過專案部署OSGI設定。 使用不同的執行模式，支援不同的測試和生產系統AEM組態。

內AEM容與商務附加元件和CIF核心元件AEM都使用伺服器端和用戶端連線。 用戶端CIF核心元件和CIF附加元件製作工具預設會連線至`/api/graphql`。 如有需要，可透過CIFCloud Service設定來調整此設定（請參閱下文）。

CIF附加元件在`/api/graphql`處提供GraphQL代理Servlet，該GraphQL代理Servlet可選擇用於[本地開發](develop.md)。 對於生產部署，強烈建議透過Dispatcher或其他網路層（如CDN），設AEM定商務GraphQL端點的反向proxy。

## 配置儲存和目錄{#catalog}

附加元件和[CIF核心元件](https://github.com/adobe/aem-core-cif-components)可用於連接到不同商AEM務商店（或商店檢視等）的多個網站結構。 預設情況下，CIF附加模組的部署具有與Adobe商務的預設儲存和目錄(Magento)連接的預設配置。

此配置可通過CIFCloud Service配置根據以下步驟調整：

1. 轉AEM至「工具」->「Cloud Services」->「CIF配置」

2. 選擇要更改的商務配置

3. 通過操作欄開啟配置屬性

![CIFCloud Services配置](/help/commerce/cif/assets/cif-cloud-service-config.png)

可以配置以下屬性：

- GraphQL客戶端——選擇已配置的GraphQL客戶端，用於商務後端通信。 這通常應維持在預設值。
- 商店檢視-(Magento)商店檢視識別碼。 如果為空，則使用預設的儲存視圖。
- GraphQL代理路徑——用於代理向商務後端GraphQLAEM端點的請求的URL路徑GraphQL代理。
   >[!NOTE]
   >
   > 在大多數設定中，預設值`/api/graphql`不能更改。 只有不使用提供的GraphQL代理的高級設定才應更改此設定。
- 啟用目錄UID支援——在商務後端GraphQL呼叫中啟用UID支援，而非ID支援。
   >[!NOTE]
   >
   > 對Adobe商務(Magento)2.4.2引入的UID的支援。只有在您的商務後端支援2.4.2版或更新版本的GraphQL架構時，才能啟用此功能。
- 目錄根類別標識符——儲存目錄根的標識符（UID或ID）

上述配置供參考。 專案應提供其專屬的組態。

如需使用多個網站結構AEM並結合不同商務目錄的更複雜設定，請參閱[商務多商店設定](configuring/multi-store-setup.md)教學課程。

## 其他資源 {#additional-resources}

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [商務多商店設定](configuring/multi-store-setup.md)
