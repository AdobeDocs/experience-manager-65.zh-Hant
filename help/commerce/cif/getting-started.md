---
title: 內容和商AEM務入門
description: 瞭解如何部AEM署內容和商務項目。
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 3%

---

# 內容和商AEM務入門 {#start}

要開始使AEM用Content and Commerce，您需要安AEM裝6.5版的Content and Commerce附加AEM程式。

## 最低軟體要求

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 需要7或更高版本。

## 入門 {#onboarding}

內容和商AEM務的登錄過程分為兩步：

1. 安AEM裝6.5版的Content and Commerce附AEM加程式

2. 連AEM接您的商業解決方案

### 安AEM裝6.5版的Content and Commerce附AEM加程式 {#install-add-on}

從下載AEM並安裝Commerce Add-On for AEM6.5 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 門戶。

啟動並安裝AEM所需的6.5 Service Pack。 我們建議安裝上一個可用的Service Pack。

>[!NOTE]
>
>這將由CSE為托管服務客戶AEM完成。

### 連AEM接到您的Commerce System {#connect}

可AEM以連接到任何具有可訪問GraphQL終結點的商業系AEM統。 這些端點通常是公開可用的，或可通過專用VPN或本地連接進行連接，具體取決於各個項目設定。

可選地，可以提供驗證報頭以使用需要驗證的附加CIF功能。

由 [項AEM目原型](https://github.com/adobe/aem-project-archetype)的 [韋尼AEM亞引用儲存](https://github.com/adobe/aem-cif-guides-venia) 已包含在 [預設配置](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) 必須調整。

替換 `url` 在 `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` GraphQL終結點。 此配置可以通過OSGI控制台或通過項目部署OSGI配置來完成。 使用不同的運行模式支援用於暫存和生產系統的AEM不同配置。

內AEM容和商務附加元件和CIF核心元件AEM使用伺服器端和客戶端連接。 客戶端CIF核心元件和CIF附加創作工具預設連接到 `/api/graphql`。 如果需要，可通過CIFCloud Service配置來調整此值（見下文）。

CIF載入項在以下位置提供GraphQL代理Servlet `/api/graphql` 可選地用於 [地方發展](develop.md)。 對於生產部署，強烈建議通過Dispatcher或其他網路層（如CDN）AEM設定到商業GraphQL終結點的反向代理。

## 配置儲存和目錄 {#catalog}

載入項和 [CIF核心元件](https://github.com/adobe/aem-core-cif-components) 可用於連接到AEM不同商業商店（或商店視圖等）的多個站點結構。 預設情況下， CIF Add-On部署時使用連接到Adobe Commerce預設儲存和目錄的預設配置。

通過CIFCloud Service配置，可以根據項目調整此配置，步驟如下：

1. 轉AEM至工具 — >Cloud Services-> CIF配置

2. 選擇要更改的商業配置

3. 通過操作欄開啟配置屬性

![CIFCloud Services配置](/help/commerce/cif/assets/cif-cloud-service-config.png)

可以配置以下屬性：

- GraphQL客戶端 — 選擇已配置的GraphQL客戶端以進行商務後端通信。 通常應保持預設狀態。
- 儲存視圖 — 儲存視表徵圖識符。 如果為空，則使用預設儲存視圖。
- GraphQL代理路徑 — 用於代理向商業後端GraphQL終結點AEM的請求的URL路徑GraphQL代理。
   >[!NOTE]
   >
   > 在大多數設定中，預設值 `/api/graphql` 不能更改。 只有不使用提供的GraphQL代理的高級設定才應更改此設定。
- 啟用目錄UID支援 — 在商務後端GraphQL調用中啟用對UID的支援，而不是ID的支援。
   >[!NOTE]
   >
   > UID支援在Adobe Commerce2.4.2推出。僅當您的商業後端支援2.4.2版或更高版本的GraphQL架構時才啟用此功能。
- 目錄根類別標識符 — 儲存目錄根的標識符（UID或ID）
   >[!CAUTION]
   >
   > 從CIF核心元件2.0.0版開始，支援 `id` 已移除並替換為 `uid`。 如果項目使用CIF核心元件2.0.0版，則必須啟用目錄UID支援並使用有效的類別UID作為「目錄根類別標識符」。

上面所示的配置可供參考。 項目應提供自己的配置。

有關使用多個站點結構並AEM結合不同商業目錄的更複雜的設定，請參閱 [Commerce多商店設定](configuring/multi-store-setup.md) 教程。

## 其他資源 {#additional-resources}

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [韋尼AEM亞引用儲存](https://github.com/adobe/aem-cif-guides-venia)
- [Commerce多商店設定](configuring/multi-store-setup.md)
