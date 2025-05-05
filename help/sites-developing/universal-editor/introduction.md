---
title: 通用編輯器
description: 瞭解通用編輯器的彈性，以及如何協助您使用AEM 6.5強化Headless體驗。
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: d3dd827e93549c558284be1c1991b4e003c9e0e8
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 1%

---


# 通用編輯器 {#universal-editor}

瞭解通用編輯器的彈性，以及如何協助您使用AEM 6.5強化Headless體驗。

## 概觀 {#overview}

通用編輯器是多功能的視覺化編輯器，屬於Adobe Experience Manager Sites的一部分。 它可讓作者對任何Headless體驗進行即席即得(WYSIWYG)編輯。

* 由於通用編輯器支援對所有形式的AEM Headless內容進行相同一致的視覺編輯，因此作者可受益於通用編輯器的彈性。
* 開發人員可受益於Universal Editor的多功能性，因為它也支援實作的真正分離。 它可讓開發人員利用他們選擇的任何架構或架構，而不受任何SDK或技術限制。

如需詳細資訊，請參閱通用編輯器[&#128279;](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)上的AEM as a Cloud Service檔案。

## 架構 {#architecture}

Universal Editor是一項與AEM搭配使用的服務，可讓您無頭製作內容。

* Universal Editor託管於`https://experience.adobe.com/#/aem/editor/canvas`，可編輯AEM 6.5轉譯的頁面。
* Universal Editor會透過AEM作者例項中的Dispatcher讀取AEM頁面。
* 與Dispatcher在相同主機上執行的Universal Editor服務會將變更寫回AEM作者例項。

![使用通用編輯器的作者流程](assets/author-flow.png)

## 要求 {#requirements}

下列專案支援通用編輯器：

* AEM 6.5 （service pack 21或22 plus a feature pack）
   * 同時支援內部部署和AMS託管。
* [AEM as a Cloud Service](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) （版本`2023.8.13099`或更新版本）

本檔案著重於通用編輯器的AEM 6.5支援。

## 設定 {#setup}

若要測試通用編輯器，您需要：

1. [更新及設定您的AEM編寫執行個體。](#update-configure-aem)
1. [設定本機通用編輯器服務。](#set-up-ue)
1. [調整您的Dispatcher以允許Universal Editor服務。](#update-dispatcher)

完成設定之後，您可以[檢測應用程式以使用通用編輯器。](#instrumentation)

### 更新AEM {#update-aem}

若要搭配AEM 6.5使用通用編輯器，需要AEM的Service Pack 21或22以及Feature Pack。

#### 套用最新Service Pack {#latest}

請確定您至少正在執行AEM 6.5適用的Service Pack 21或22。您可以從[軟體發佈](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=zh-Hant)下載最新的Service Pack。

#### 安裝通用編輯器Feature Pack {#feature-pack}

安裝Software Distribution提供的AEM 6.5 **[適用的** Universal Editor Feature Pack。](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip)

如果您已執行Service Pack 23或更新版本，則不需要此Feature Pack。

### 設定服務 {#configure-services}

此Feature Pack會安裝許多需要額外設定的新套件。

#### 設定`login-token` Cookie的SameSite屬性。 {#samesite-attribute}

1. 開啟Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Adobe Granite Token Authentication Handler**，然後按一下&#x200B;**變更組態值**。
1. 在對話方塊中，將登入權杖cookie **(`token.samesite.cookie.attr`)值的** SameSite屬性變更為`Partitioned`。
1. 按一下「**儲存**」。

#### 移除`SAMEORIGIN`標題X-Frame選項。 {#sameorigin}

1. 開啟Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Apache Sling主要Servlet**，然後按一下&#x200B;**編輯設定值**。
1. 刪除&#x200B;**其他回應標頭**&#x200B;屬性(`sling.additional.response.headers`)中的`X-Frame-Options=SAMEORIGIN`值（如果存在）。
1. 按一下「**儲存**」。

#### 設定Adobe Granite查詢引數驗證處理常式。 {#query-parameter}

1. 開啟Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Adobe Granite查詢引數驗證處理常式**，然後按一下&#x200B;**編輯組態值**。
1. 在&#x200B;**路徑**&#x200B;欄位(`path`)中新增`/`以啟用。
   * 空值會停用驗證處理常式。
1. 按一下「**儲存**」。

#### 定義應開啟通用編輯器的內容路徑或`sling:resourceTypes`。 {#paths}

1. 開啟Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**通用編輯器URL服務**，然後按一下&#x200B;**編輯設定值**。
1. 定義應開啟通用編輯器的內容路徑或`sling:resourceTypes`。
   * 在&#x200B;**Universal Editor Opening Mapping**&#x200B;欄位中，提供開啟Universal Editor的路徑。
   * 在應由通用編輯器開啟的&#x200B;**Sling：resourceTypes**&#x200B;欄位中，提供由通用編輯器直接開啟的資源清單。
1. 按一下「**儲存**」。
1. 檢查您的[外部化程式組態](/help/sites-developing/externalizer.md)，並確定您至少有本機、作者和發佈環境設定，如下列範例所示。

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

完成這些設定步驟後，AEM將依下列順序開啟頁面的通用編輯器。

1. AEM將檢查`Universal Editor Opening Mapping`底下的對應，如果內容位於該處定義的任何路徑下，則會為其開啟通用編輯器。
1. 對於不在`Universal Editor Opening Mapping`中定義的路徑下的內容，AEM會檢查內容的`resourceType`是否與&#x200B;**Sling：resourceTypes （應由通用編輯器**&#x200B;開啟）中定義的內容相符，如果內容符合其中一個型別，則在`${author}${path}.html`為其開啟通用編輯器。
1. 否則，AEM會開啟頁面編輯器。

下列變數可用來定義`Universal Editor Opening Mapping`下的對應。

* `path`：要開啟之資源的內容路徑
* `localhost`： `localhost`的Externalizer專案沒有結構描述，例如`localhost:4502`
* `author`：沒有結構描述的作者的Externalizer專案，例如`localhost:4502`
* `publish`：用於沒有結構描述的發行的Externalizer專案，例如`localhost:4503`
* `preview`：預覽的外部化程式專案，不含結構描述，例如`localhost:4504`
* `env`： `prod`、`stage`、`dev`根據定義的Sling執行模式
* `token`： `QueryTokenAuthenticationHandler`所需的查詢權杖

範例對應：

* 在AEM作者上開啟`/content/foo`下的所有頁面：
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * 這會導致開啟`https://localhost:4502/content/foo/x.html?login-token=<token>`
* 在遠端NextJS伺服器上開啟`/content/bar`下的所有頁面，提供所有變數作為資訊
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * 這會導致開啟`https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### 設定通用編輯器服務 {#set-up-ue}

更新並設定AEM後，您就可以設定本機通用編輯器服務，以供您自己的本機開發和測試使用。

1. 安裝Node.js version >=20。
1. 從[Software Distribution](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud/software-distribution/home)下載並解除封裝最新的Universal Editor服務
1. 透過環境變數或`.env`檔案設定Universal Editor Service。
   * [如需詳細資訊，請參閱AEM as a Cloud Service Universal Editor檔案。](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * 請注意，如果需要內部IP重寫，您可能需要使用`UES_MAPPING`選項。
1. 執行`universal-editor-service.cjs`

### 更新Dispatcher {#update-dispatcher}

設定AEM且執行本機Universal Editor服務時，您必須在Dispatcher中允許新服務[的反向Proxy。](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-dispatcher/using/dispatcher)

1. 調整製作執行個體的vhost檔案，以包含反向Proxy。

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080是預設連線埠。 如果您使用[您的`.env`檔案，](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)中的`UES_PORT`引數變更此專案，您必須在此相應地調整連線埠值。

1. 重新啟動Apache。

## 檢測您的應用程式 {#instrumentation}

更新AEM並執行本機Universal Editor Service後，您就可以使用Universal Editor開始編輯Headless內容。

不過，您的應用程式必須檢測為使用通用編輯器。 這涉及包括中繼標籤，以指示編輯器如何以及在何處保留內容。 此檢測的詳細資訊可在AEM as a Cloud Service的[通用編輯器檔案中取得。](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

請注意，在針對AEM as a Cloud Service通用編輯器編寫以下檔案時，將其與AEM 6.5搭配使用時將套用以下變更。

* 中繼標籤中的通訊協定必須是`aem65`而非`aem`。

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* 必須透過meta標籤公告Universal Editor服務端點。

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* 在元件定義的`plugins`區段中，必須使用`aem65`而非`aem`。

>[!TIP]
>
>如需開發人員快速入門通用編輯器的完整指南，請參閱AEM as a Cloud Service檔案中的檔案[AEM開發人員的通用編輯器概述](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview)，同時牢記本節所述的AEM 6.5支援所需的必要變更。

## AEM 6.5與AEM as a Cloud Service之間的差異 {#differences}

AEM 6.5中的通用編輯器的運作方式與AEM as a Cloud Service大致相同，包括UI和大部分設定。 不過，請注意其中的差異。

* 6.5中的通用編輯器僅支援Headless使用案例。
* 通用編輯器的設定對6.5稍有不同（[如目前檔案所述](#setup)）。
* 6.5中的Universal Editor使用與AEM as a Cloud Service不同的資產選擇器和內容片段選擇器。
