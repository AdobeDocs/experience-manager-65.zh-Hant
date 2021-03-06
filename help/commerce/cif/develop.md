---
title: 開發AEM Commerce
description: 了解如何使用AEM專案原型產生啟用商務的AEM專案。 了解如何建立專案並部署至本機開發環境。
topics: Commerce, Development
feature: 商務整合架構
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 4%

---


# 開發AEM Commerce {#develop}

根據AEM的AEM Integration Framework(CIF)開發AEM Commerce專案，會遵循與其他專案相同的規則和最佳實務。 請先查看以下內容：

- [AEM 6.5 Developing 使用指南](/help/sites-developing/home.md)
- [AEM核心概念](/help/sites-developing/the-basics.md)
- [AEM開發 — 准則和最佳實務](/help/sites-developing/dev-guidelines-bestpractices.md)
- [如何使用Apache Maven建立AEM專案](/help/sites-developing/ht-projects-maven.md)

## AEM Commerce的當地開發 {#local}

若要與CIF專案搭配使用，建議使用當地開發環境。

>[!NOTE]
>
>下列指示可協助您使用CIF，針對AEM 6.5重點設定AEM Commerce的本機AEM開發環境)。 如果您使用AEM作為Cloud Service，請參閱[AEM Commerce作為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html)檔案。

適用於AEM 6.5的AEM Commerce附加元件亦稱。 CIF附加元件也適用於本機開發，並以AEM套件形式提供。 可從[軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下載為Feature Pack。

### 所需軟體

應在本機安裝下列項目：

- 本機AEM 6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7或更新版本
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 或更新版本)
- [節點LTS](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### 存取CIF附加元件

CIF附加元件可從[Software Distribution入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下載，並搜尋「AEM Commerce附加元件」。

>[!TIP]
>
>請務必一律使用最新的CIF附加元件版本。

### 本機設定

針對使用AEM和CIF附加元件的本機CIF專案開發，請執行下列步驟：

1. 取得AEM 6.5版本並安裝AEM 6.5 Service Pack。 AEM 6.5 Service Pack 7為必要項目，但建議您安裝最後一個可用的Service Pack。

1. 解壓縮AEM .jar以建立`crx-quickstart`資料夾，執行：

   ```bash
   java -jar <jar name> -unpack
   ```

1. 建立`crx-quickstart/install`資料夾

1. 將從軟體發佈入口網站下載的所有CIF附加元件套件複製至`crx-quickstart/install`資料夾。

>[!TIP]
>
>或者，您也可以透過套件管理器安裝CIF附加套件。

1. 啟動AEM快速入門

透過OSGI主控台驗證設定： `http://localhost:4502/system/console/osgi-installer`。 清單中應包含CIF附加元件相關套件組合、內容套件和OSGI設定。 請確定所有套件組合均已啟動。

## 專案設定 {#project}

使用CIF啟動AEM Commerce專案有兩種方式。

### 使用AEM專案原型

[AEM專案原型](https://github.com/adobe/aem-project-archetype)是引導預先設定專案以開始使用CIF的主要工具。 CIF核心元件和所有必要設定皆可納入產生的專案中，並提供額外選項。

>[!TIP]
>
>使用[AEM專案原型25或更新版本](https://github.com/adobe/aem-project-archetype/releases)來產生專案。

請參閱AEM專案原型[使用指示](https://github.com/adobe/aem-project-archetype#usage)，了解如何產生AEM專案。 若要將CIF納入專案，請使用`includeCommerce`選項。

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

CIF核心元件可用於任何專案，方法是納入所提供的`all`套件，或個別使用CIF內容套件和相關的OSGI套件。 若要手動將CIF核心元件新增至專案，請使用下列相依性：

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

### 使用AEM Venia Reference Store

啟動CIF專案的第二個選項是複製並使用[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)。 AEM Venia Reference Store是範例參考店面應用程式，示範AEM的CIF核心元件使用方式。 這是一組最佳實務範例，也是開發您自己功能的潛在起點。

若要開始使用Venia Reference Store，只需複製[ Git存放庫](https://github.com/adobe/aem-cif-guides-venia)，然後開始根據您的需求自訂專案。

>[!NOTE]
>
>Venia Reference Store專案包含AEM作為Cloud Service和AEM 6.5的兩個建置設定檔。請查看[專案readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md)以了解其使用方式。 若為AEM 6.5，請使用`classic`設定檔。

### 將AEM連線至Commerce System

要將項目連接到商務系統AEM，必須使用商務系統的GraphQL端點進行配置。

兩者皆為[AEM專案原型](https://github.com/adobe/aem-project-archetype)或[AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)產生的專案，已包含必須調整的[預設設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)。

將`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中的`url`值替換為項目所使用的商務系統的GraphQL端點。

AEM Commerce Add-On和CIF Core Components可透過AEM伺服器直接透過瀏覽器連線至commerce GraphQL端點。 用戶端CIF核心元件和CIF附加元件製作工具預設會連線至`/api/graphql`。 如有需要，可透過CIFCloud Service設定加以調整（請參閱下方）。

CIF附加元件提供位於`/api/graphql`的GraphQL代理Servlet。 如果您不打算使用本機AEM Dispatcher，建議您也設定GraphQL代理Servlet。

導覽至http://localhost:4502/system/console/configMgr並建立`Adobe CIF GraphQL Proxy Configuration`服務的OSGI設定。 使用與上述GraphQL客戶端所用的商務系統的相同GraphQL端點。

## 其他資源

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
