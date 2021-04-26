---
title: 發展商AEM務
description: 瞭解如何使用專案原型產生AEM具商務功能AEM的專案。 瞭解如何建立專案並將其部署至本機開發環境。
topics: Commerce, Development
feature: 商務整合框架
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: 8ead3d1b24177effa4d40141408c5676eaabcc30
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 4%

---


# 開AEM發商務{#develop}

根據商AEM務整合框架(CIF)開發商務專案，其AEM規則與最佳實務與其他專案相AEM同。 請先閱讀以下內容：

- [AEM 6.5 Developing 使用指南](/help/sites-developing/home.md)
- [AEM核心概念](/help/sites-developing/the-basics.md)
- [開AEM發——准則和最佳做法](/help/sites-developing/dev-guidelines-bestpractices.md)
- [如何使用Apache AEM Maven建立專案](/help/sites-developing/ht-projects-maven.md)

## Local Development for AEM Commerce {#local}

建議在當地開發環境下與CIF項目合作。

>[!NOTE]
>
>下列指示可協助您使用CIFAEM為AEMCommerce設定本機開發環境，其焦點為AEM6.5)。 如果您使AEM用Cloud Service，請參閱[AEM Commerce as aCloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/home.html)檔案。

6.AEM5(亦稱AEMCommerce Add-On)。 CIF附加元件也可供當地開發，並提供一AEM套。 它可從[軟體散發入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下載為功能套件。

### 所需軟體

本機應安裝下列程式碼：

- 本地AEM6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7或更新版本
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 或更新版本)
- [節點LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 訪問CIF附加模組

CIF附加元件可從[軟體散發入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下載，搜尋「AEM商務附加元件」。

>[!TIP]
>
>請務必使用最新的CIF附加元件版本。

### 本機設定

對於本地CIF項目開發，使用AEMCIF附加元件和以下步驟：

1. 取得AEM6.5版本並安裝AEM6.5 Service Pack。 需AEM要6.5 Service Pack 7，但建議安裝最後一個可用的Service Pack。

1. 解壓縮AEM.jar以建立`crx-quickstart`資料夾，請運行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立`crx-quickstart/install`資料夾

1. 將從軟體分發門戶下載的CIF附加軟體包複製到`crx-quickstart/install`資料夾中。

>[!TIP]
>
>或者，CIF附加軟體包也可以通過軟體包管理器安裝。

1. 開始快速AEM入門

通過OSGI控制台驗證設定： `http://localhost:4502/system/console/osgi-installer`。 清單中應包含CIF附加元件相關的組合、內容封裝和OSGI組態。 請確定已啟動所有搭售。

## 項目設定{#project}

使用CIF啟動您的商AEM務專案有兩種方式。

### 使用AEM專案原型

[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)是引導預配置項目以開始使用CIF的主要工具。 CIF核心元件和所有必需的配置都可以包含在一個生成的項目中，並附加一個選項。

>[!TIP]
>
>使用[AEM Project Archetype 25或更新版本](https://github.com/adobe/aem-project-archetype/releases)產生專案。

請參AEM閱項目原型[使用說明](https://github.com/adobe/aem-project-archetype#usage)，瞭解如何生成項AEM目。 要將CIF包括在項目中，請使用`includeCommerce`選項。

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

CIF核心元件可以通過包括提供的`all`包或使用CIF內容包和相關OSGI包的個人，在任何項目中使用。 要手動將CIF核心元件添加到項目，請使用以下相關性：

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

### 使用AEMVenia Reference Store

啟動CIF項目的第二個選擇是克隆並使用[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)。 Venia Reference StoreAEM是範例參考店面應用程式，示範CIF核心元件的使用AEM方式。 它是一組最佳實務範例，是開發您自己功能的潛在起點。

要開始使用Venia Reference Store，只需克隆[Git儲存庫](https://github.com/adobe/aem-cif-guides-venia)，然後根據您的需要開始自定義項目。

>[!NOTE]
>
>Venia Reference Store專案包含兩個建置設定檔，AEM做為Cloud Service和AEM6.5。請查看[專案readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)以瞭解其使用方式。 對於AEM6.5，請使用`classic`描述檔。

### 連AEM線至商務系統

要將項目連接到商務系統，AEM必須使用商務系統的GraphQL端點進行配置。

兩者中，由[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)或[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)產生的專案都已包含必須調整的[預設設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)。

將`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中的`url`值替換為項目所使用的商務系統的GraphQL端點。

Commerce Add-OnAEM和CIF Core Components透過伺服器直接透過瀏覽器連AEM接至commerce GraphQL端點。 用戶端CIF核心元件和CIF附加元件製作工具預設會連線至`/api/graphql`。 如果需要，可通過CIFCloud Service配置來調整此配置（見下文）。

CIF附加模組在`/api/graphql`處提供GraphQL代理Servlet。 如果您不打算使用本機Dispatcher,AEM建議您也配置GraphQL代理Servlet。

導覽至http://localhost:4502/system/console/configMgr並建立`Adobe CIF GraphQL Proxy Configuration`服務的OSGI設定。 使用與上述GraphQL客戶端相同的商務系統的GraphQL端點。

## 其他資源

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
