---
title: 發展商AEM業
description: 瞭解如何使用項目原型AEM生成啟AEM用商業的項目。 瞭解如何構建項目並將其部署到本地開發環境。
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 48479725-8b52-4ff2-a599-d20958b26ee6
source-git-commit: 78359fb8ecbcc0227ab5a3910175aed73d823902
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 10%

---

# 發展商AEM業 {#develop}

基於AEM商業整合框架(CIF)為其開發商業項AEM目遵循與其他項目相同的規則和最AEM佳做法。 請先查看以下內容：

- [AEM 6.5 Developing 使用指南](/help/sites-developing/home.md)
- [核AEM心概念](/help/sites-developing/the-basics.md)
- [開AEM發 — 指南和最佳做法](/help/sites-developing/dev-guidelines-bestpractices.md)
- [如何使用Apache AEM Maven生成項目](/help/sites-developing/ht-projects-maven.md)

## 地方商務發AEM展 {#local}

建議採用當地發展環境與CIF項目合作。

>[!NOTE]
>
>以下說明可幫助您使用CIFAEM為AEMCommerce設定本地開發環境，其重AEM點為6.5)。 如果您使用AEMas a Cloud Service，請參閱 [商AEM務as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html) 文檔。

6.AEM5(也稱AEM)的Commerce Add-on。 CIF Add-On也可供當地開發，並作為包AEM裝提供。 可以從 [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 功能包。

### 所需軟體

應在本地安裝以下內容：

- 本地AEM6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7或更高版本
- [爪哇11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 或更新版本)
- [節點LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 訪問CIF載入項

CIF載入項可以從 [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)，搜索「AEMCommerce載入項」。

>[!TIP]
>
>確保始終使用最新的CIF附加版本。

### 本地設定

使用以下步驟和CIF附AEM加程式開發本地CIF項目：

1. 獲取AEM6.5版並安AEM裝6.5 Service Pack。 需AEM要6.5 Service Pack 7，但建議安裝最後一個可用的Service Pack。

1. 解壓縮AEM.jar以建立 `crx-quickstart` 資料夾，運行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立 `crx-quickstart/install` 資料夾

1. 將從軟體分發門戶下載的CIF附加包複製到 `crx-quickstart/install` 的子菜單。

>[!TIP]
>
>或者， CIF附加軟體包也可以通過軟體包管理器安裝。

1. 啟動快AEM速啟動

通過OSGI控制台驗證安裝： `http://localhost:4502/system/console/osgi-installer`。 該清單應包括CIF附加相關的捆綁包、內容包和OSGI配置。 確保已啟動所有捆綁包。

## 專案設定 {#project}

使用CIF啟動您的AEMCommerce項目有兩種方法。

### 使用項AEM目原型

的 [項AEM目原型](https://github.com/adobe/aem-project-archetype) 是引導預配置項目以開始使用CIF的主要工具。 CIF核心元件和所有所需配置都可以包含在生成的項目中，並附帶一個額外選項。

>[!TIP]
>
>使用 [原型AEM25或更高版本](https://github.com/adobe/aem-project-archetype/releases) 生成項目。

請參閱AEM項目原型 [用法說明](https://github.com/adobe/aem-project-archetype#usage) 如何生成項AEM目。 要將CIF包括到項目中，請使用 `includeCommerce` 的雙曲餘切值。

例如：

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF核心元件可用於任何項目，包括提供的 `all` 或使用CIF內容包和相關OSGI包的個人。 要手動將CIF核心元件添加到項目，請使用以下相關項：

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### 使用AEMVenia引用儲存

啟動CIF項目的第二個選項是克隆和使用 [韋尼AEM亞引用儲存](https://github.com/adobe/aem-cif-guides-venia)。 Venia參AEM考儲存是示例參考儲存應用程式，演示了CIF核心元件的使AEM用。 它旨在作為一組最佳實踐示例和開發您自己的功能的潛在起點。

要開始使用Venia引用儲存，只需克隆 [Git儲存庫](https://github.com/adobe/aem-cif-guides-venia) 然後根據需要自定義項目。

>[!NOTE]
>
>Venia Reference Store項目包含兩個用於AEMas a Cloud Service和AEM6.5的生成配置檔案。檢查 [項目readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) 看看它們的用途。 AEM6.5使用 `classic` 檔案。

### 連AEM接到Commerce System

要將項目連接到商務系統，AEM必須使用商務系統的GraphQL終結點進行配置。

兩者，由 [項AEM目原型](https://github.com/adobe/aem-project-archetype) 或 [韋尼AEM亞引用儲存](https://github.com/adobe/aem-cif-guides-venia)，已包括 [預設配置](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) 必須調整。

替換 `url` 在 `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` 與項目使用的商務系統的GraphQL端點。

Commerce AEM Add-On和CIF核心元件通過伺服器直接通過瀏覽器連AEM接到Commerce Deppoint。 客戶端CIF核心元件和CIF附加創作工具（預設）連接到 `/api/graphql`。 如果需要，可通過CIFCloud Service配置來調整此值（見下文）。

CIF載入項提供位於 `/api/graphql`。 如果您不計畫使用本地AEM調度程式，建議也配置GraphQL代理Servlet。

導航到http://localhost:4502/system/console/configMgr並為 `Adobe CIF GraphQL Proxy Configuration` 服務。 使用與上面的GraphQL客戶端使用的商業系統的GraphQL端點。

## 其他資源

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [韋尼AEM亞引用儲存](https://github.com/adobe/aem-cif-guides-venia)
