---
title: AEM Content and Commerce 快速入門
description: 瞭解如何部署AEM內容和Commerce專案。
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 3%

---

# AEM Content and Commerce 快速入門 {#start}

若要開始使用AEM內容和Commerce，您必須安裝適用於AEM 6.5的AEM內容和Commerce附加元件。

## 最低軟體需求

需要[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7或更新版本。

## 上線 {#onboarding}

AEM內容和Commerce的上線流程分為兩個步驟：

1. 安裝適用於AEM 6.5的AEM Content and Commerce附加元件

2. 將AEM與您的商務解決方案連線

### 安裝適用於AEM 6.5的AEM Content and Commerce附加元件 {#install-add-on}

從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)入口網站下載並安裝適用於AEM 6.5的AEM Commerce附加元件。

啟動並安裝必要的AEM 6.5 Service Pack。 建議您安裝最後一個可用的Service Pack。

>[!NOTE]
>
>CSE將針對AEM Managed Service客戶完成這項工作。

### 將AEM連線至您的Commerce系統 {#connect}

AEM可連線至任何具有AEM適用的GraphQL端點可存取的商務系統。 這些端點通常可以公開使用，也可以透過私人VPN或本機連線進行連線，具體取決於個別專案設定。

可選擇提供驗證標頭，以使用需要驗證的其他CIF功能。

由[AEM專案原型](https://github.com/adobe/aem-project-archetype)產生的專案，以及已包含在[預設設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)中的[AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)必須調整。

將`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中`url`的值取代為您的商務系統的GraphQL端點。 此設定可透過OSGI主控台完成，或透過專案部署OSGI設定來完成。 使用不同的AEM執行模式支援中繼和生產系統的不同設定。

AEM內容和Commerce附加元件及CIF核心元件同時使用AEM伺服器端和使用者端連線。 使用者端CIF核心元件和CIF附加撰寫工具預設會連線至`/api/graphql`。 如有需要，可透過CIFCloud Service設定調整此專案（請參閱下文）。

CIF附加元件提供位於`/api/graphql`的GraphQL Proxy Servlet，可選擇用於[本機開發](develop.md)。 在生產部署中，強烈建議透過AEM Dispatcher或其他網路層（如CDN）設定商務GraphQL端點的反向Proxy。

## 設定存放區和目錄 {#catalog}

附加元件和[CIF核心元件](https://github.com/adobe/aem-core-cif-components)可用於連線至不同商務商店（或商店檢視等）的多個AEM網站結構。 根據預設，CIF附加元件會以連線到Adobe Commerce預設存放區和目錄的預設設定進行部署。

您可以按照以下步驟，透過CIFCloud Service設定來針對專案調整此設定：

1. 在AEM中，前往「工具>Cloud Service> CIF設定」

2. 選取您要變更的商務設定

3. 透過動作列開啟設定屬性

![CIFCloud Service設定](/help/commerce/cif/assets/cif-cloud-service-config.png)

可以設定下列屬性：

- GraphQL使用者端 — 選取已設定的GraphQL使用者端以進行商務後端通訊。 這通常應該保持在預設值。
- 存放區檢視 — 存放區檢視識別碼。 如果空白，則使用預設存放區檢視。
- GraphQL Proxy路徑 — AEM中的GraphQL Proxy用來將請求代理至商務後端GraphQL端點的URL路徑。

  >[!NOTE]
  >
  >在大多數設定中，不可變更預設值`/api/graphql`。 只有未使用所提供GraphQL Proxy的進階設定，才應變更此設定。

- 啟用目錄UID支援 — 在商務後端GraphQL呼叫中啟用對UID而非ID的支援。

  >[!NOTE]
  >
  >Adobe Commerce 2.4.2引進了對UID的支援。只有在您的Commerce後端支援2.4.2版或更新版本的GraphQL結構描述時，才會啟用此功能。

- 目錄根類別識別碼 — 商店目錄根的識別碼（UID或ID）

  >[!CAUTION]
  >
  >從CIF核心元件2.0.0版開始，已移除對`id`的支援，並取代為`uid`。 如果您的專案使用CIF核心元件2.0.0版，您必須啟用目錄UID支援，並使用有效的類別UID作為「目錄根類別識別碼」。

以上所示的設定可供參考。 專案應提供自己的設定。

如需使用多個AEM網站結構並結合不同商務目錄的更複雜設定，請參閱[Commerce多商店設定](configuring/multi-store-setup.md)教學課程。

## 其他資源 {#additional-resources}

- [AEM專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
- [Commerce多商店設定](configuring/multi-store-setup.md)
