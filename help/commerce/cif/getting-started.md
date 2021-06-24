---
title: AEM內容與商務快速入門
description: 了解如何部署AEM內容與商務專案。
topics: Commerce
feature: 商務整合架構
thumbnail: 37843.jpg
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
source-git-commit: 61b8d0bf960bd03a19d22061f3c897a56259dd24
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---

# AEM內容與商務快速入門 {#start}

若要開始使用AEM Content and Commerce，您需要安裝適用於AEM 6.5的AEM Content and Commerce附加元件。

## 最低軟體需求

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7或更新版本為必要。

## 入門 {#onboarding}

AEM內容與商務的上線程式為兩個步驟：

1. 安裝AEM 6.5的AEM Content and Commerce附加元件

2. 將AEM與您的商務解決方案連接

### 安裝AEM 6.5的AEM Content and Commerce附加元件 {#install-add-on}

從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)入口網站下載並安裝AEM Commerce Add-On for AEM 6.5。

啟動並安裝所需的AEM 6.5 Service Pack。 建議您安裝最後一個可用的Service Pack。

>[!NOTE]
>
>這將由AEM Managed Service客戶的CSE完成。

### 將AEM連線至您的Commerce System {#connect}

AEM可連線至任何具有AEM適用之GraphQL端點可存取的商務系統。 這些端點通常可公開使用，或可根據個別專案設定透過私有VPN或本機連線連線。

可選地，可提供驗證標頭以使用需要驗證的其他CIF功能。

必須調整[AEM專案原型](https://github.com/adobe/aem-project-archetype)和[AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)所產生的專案（已包含在[預設設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)中）。

將`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中的`url`值替換為商務系統的GraphQL端點。 此設定可透過OSGI主控台完成，或透過專案部署OSGI設定。 使用不同的AEM執行模式，支援預備和生產系統的不同設定。

AEM Content and Commerce附加元件和CIF核心元件會同時使用AEM伺服器端和用戶端連線。 用戶端CIF核心元件和CIF附加元件製作工具依預設會連線至`/api/graphql`。 如有需要，可透過CIFCloud Service設定來調整（請參閱下方）。

CIF附加元件提供位於`/api/graphql`的GraphQL代理Servlet，可選擇用於[本地開發](develop.md)。 對於生產部署，強烈建議透過AEM Dispatcher或其他網路層（例如CDN），設定反向Proxy至商務GraphQL端點。

## 配置儲存和目錄 {#catalog}

附加元件和[CIF核心元件](https://github.com/adobe/aem-core-cif-components)可用於連接至不同商務商店（或商店檢視等）的多個AEM網站結構。 依預設，CIF附加元件的部署會具有預設設定，連線至Adobe商務的預設存放區和目錄(Magento)。

依照下列步驟，透過CIFCloud Service設定，針對專案調整此設定：

1. 在AEM中前往「工具 — >Cloud Services-> CIF設定」

2. 選擇要更改的商務配置

3. 透過動作列開啟設定屬性

![CIFCloud Services設定](/help/commerce/cif/assets/cif-cloud-service-config.png)

可以配置以下屬性：

- GraphQL客戶端 — 選擇配置的GraphQL客戶端以進行商務後端通信。 這通常應保持預設值。
- 儲存檢視 — (Magento)儲存檢視識別碼。 如果為空，則使用預設的商店視圖。
- GraphQL代理路徑 — AEM中的URL路徑GraphQL代理，用於代理向商務後端GraphQL端點的請求。
   >[!NOTE]
   >
   > 在大多數設定中，預設值`/api/graphql`不得變更。 只有進階設定（不使用提供的GraphQL代理）才應變更此設定。
- 啟用目錄UID支援 — 在商務後端GraphQL呼叫中，啟用對UID的支援，而非ID。
   >[!NOTE]
   >
   > Adobe商務(Magento)2.4.2已推出UID支援。請僅在您的商務後端支援2.4.2版或更新版本的GraphQL架構時啟用。
- 目錄根類別標識符 — 儲存目錄根的標識符（UID或ID）
   >[!CAUTION]
   >
   > 從CIF核心元件2.0.0版開始，`id`的支援已移除，並改為`uid`。 如果您的專案使用CIF核心元件2.0.0版，則必須啟用目錄UID支援，並使用有效的類別UID作為「目錄根類別識別碼」。

上述組態供參考。 專案應提供自己的設定。

如需使用多個AEM網站結構並結合不同商務目錄的更複雜設定，請參閱[商務多商店設定](configuring/multi-store-setup.md)教學課程。

## 其他資源 {#additional-resources}

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [商務多商店設定](configuring/multi-store-setup.md)
