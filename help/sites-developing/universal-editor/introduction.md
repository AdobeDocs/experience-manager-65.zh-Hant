---
title: 通用編輯器
description: 瞭解通用編輯器的彈性，以及如何協助您使用AEM 6.5強化Headless體驗。
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: 28e44586c6a8596037a44fa10d21b3fdcdea1606
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 26%

---


# 通用編輯器 {#universal-editor}

瞭解通用編輯器的彈性，以及如何協助您使用AEM 6.5強化Headless體驗。

## 概觀 {#overview}

通用編輯器是一個多功能視覺化編輯器，是 Adobe Experience Manager Sites 的一部分。 它可讓作者對任何Headless體驗進行即席即得(WYSIWYG)編輯。

* 由於通用編輯器支援對所有形式的AEM Headless內容進行相同一致的視覺編輯，因此作者可受益於通用編輯器的彈性。
* 開發人員可受益於Universal Editor的多功能性，因為它也支援實作的真正分離。 它可讓開發人員利用他們選擇的任何架構或架構，而不受任何SDK或技術限制。

如需詳細資訊，請參閱通用編輯器](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)上的[AEM as a Cloud Service檔案。

## 架構 {#architecture}

Universal Editor是一項與AEM搭配使用的服務，可讓您無頭製作內容。

* Universal Editor託管於`https://experience.adobe.com/#/aem/editor/canvas`，可編輯AEM 6.5轉譯的頁面。
* Universal Editor會透過AEM作者例項中的Dispatcher讀取AEM頁面。
* 與Dispatcher在相同主機上執行的Universal Editor服務會將變更寫回AEM作者例項。

![使用通用編輯器的作者流程](assets/author-flow.png)

## 要求 {#requirements}

以下工具支援通用編輯器：

* AEM 6.5
   * 同時支援內部部署和AMS*託管。
* [AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * 同時支援內部部署和AMS*託管。
* [AEM as a Cloud Service](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)

本檔案著重於通用編輯器的AEM 6.5支援。 若要搭配AEM 6.5使用通用編輯器，您將需要：

* AEM 6.5 （含Service Pack 23或更新版本）
   * [Feature Pack.](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip)也支援Service Pack 21和22。
* Dispatcher已正確設定

>[!NOTE]
>
>*如果您使用Adobe Managed Services (AMS)，請洽詢您的客戶成功工程師(CSE)，以瞭解您是否想要使用通用編輯器。

## 設定 {#setup}

若要測試通用編輯器，您需要：

1. [設定本機通用編輯器服務。](#set-up-ue)
1. [調整您的Dispatcher以允許Universal Editor服務。](#update-dispatcher)

完成設定之後，您可以[檢測應用程式以使用通用編輯器。](#instrumentation)

### 設定服務 {#configure-services}

Universal Editor會運用多個套件，針對這些套件需要額外設定。

#### 設定`login-token` Cookie的SameSite屬性。 {#samesite-attribute}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Adobe Granite Token Authentication Handler**，然後按一下&#x200B;**變更組態值**。
1. 在對話方塊中，將登入權杖cookie **(`token.samesite.cookie.attr`)值的** SameSite屬性變更為`Partitioned`。
1. 按一下&#x200B;**儲存**。

#### 移除`SAMEORIGIN`標題X-Frame選項。 {#sameorigin}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Apache Sling主要Servlet**，然後按一下&#x200B;**編輯設定值**。
1. 刪除&#x200B;**其他回應標頭**&#x200B;屬性(`sling.additional.response.headers`)中的`X-Frame-Options=SAMEORIGIN`值（如果存在）。
1. 按一下&#x200B;**儲存**。

#### 設定Adobe Granite查詢引數驗證處理常式。 {#query-parameter}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Adobe Granite查詢引數驗證處理常式**，然後按一下&#x200B;**編輯組態值**。
1. 在&#x200B;**路徑**&#x200B;欄位(`path`)中新增`/`以啟用。
   * 空值會停用驗證處理常式。
1. 按一下&#x200B;**儲存**。

#### 定義應開啟通用編輯器的內容路徑或`sling:resourceTypes`。 {#paths}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到「**通用編輯器 URL 服務**」，然後按一下「**編輯設定值**」。
1. 定義應開啟通用編輯器的內容路徑或`sling:resourceTypes`。
   * 在「**通用編輯器開啟對應**」欄位中，提供通用編輯器的開啟路徑。
   * 在「**應由通用編輯器開啟之 Sling:resourceTypes**」欄位中，列出由通用編輯器直接開啟的資源。
1. 按一下「**儲存**」。
1. 查看您的 [Externalizer 設定](/help/sites-developing/externalizer.md)，並確保至少已設定本機、作者和發佈環境，如下列範例所示。

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

完成這些設定步驟後，AEM 會依照以下順序開啟頁面的通用編輯器。

1. AEM 會檢查 `Universal Editor Opening Mapping` 之下的對應，若內容位於該處所定義的任何路徑之下，便會針對該內容開啟通用編輯器。
1. 對於不在 `Universal Editor Opening Mapping` 中所定義路徑之下的內容，AEM 會檢查內容的 `resourceType` 是否與「**應由通用編輯器開啟之 Sling:resourceTypes**」中定義者相符，若內容符合其中一種類型，便會針對該內容在 `${author}${path}.html` 開啟通用編輯器。
1. 否則，AEM 會開啟頁面編輯器。

下列變數可用來定義`Universal Editor Opening Mapping`下的對應。

* `path`：要開啟的資源內容路徑
* `localhost`：`localhost` 的 Externalizer 項目，無結構描述，例如 `localhost:4502`
* `author`：作者的 Externalizer 項目，無結構描述，例如 `localhost:4502`
* `publish`：發佈的 Externalizer 項目，無結構描述，例如 `localhost:4503`
* `preview`：預覽的 Externalizer 項目，無結構描述，例如 `localhost:4504`
* `env`：`prod`、`stage`、`dev`，根據所定義的 Sling 執行模式
* `token`：`QueryTokenAuthenticationHandler` 所需的查詢權杖

範例對應：

* 在 AEM Author 上開啟 `/content/foo` 之下的所有頁面：
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * 這樣會開啟 `https://localhost:4502/content/foo/x.html?login-token=<token>`
* 在遠端NextJS伺服器上開啟`/content/bar`下的所有頁面，提供所有變數作為資訊
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * 這樣會開啟 `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### 設定通用編輯器服務 {#set-up-ue}

更新並設定AEM後，您就可以設定本機通用編輯器服務，以供您自己的本機開發和測試使用。

1. 安裝Node.js version >=20。
1. 從[Software Distribution](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud/software-distribution/home)下載並解除封裝最新的Universal Editor服務
1. 透過環境變數或`.env`檔案設定Universal Editor Service。
   * [如需詳細資訊，請參閱AEM as a Cloud Service Universal Editor檔案。](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
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
   >8080是預設連線埠。 如果您使用[您的`.env`檔案，](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)中的`UES_PORT`引數變更此專案，您必須在此相應地調整連線埠值。

1. 重新啟動Apache。

## 檢測您的應用程式 {#instrumentation}

更新AEM並執行本機Universal Editor Service後，您就可以使用Universal Editor開始編輯Headless內容。

不過，您的應用程式必須檢測為使用通用編輯器。 這涉及包括中繼標籤，以指示編輯器如何以及在何處保留內容。 此檢測的詳細資訊可在AEM as a Cloud Service的[通用編輯器檔案中取得。](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

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
>如需開發人員快速入門通用編輯器的完整指南，請參閱AEM as a Cloud Service檔案中的檔案[AEM開發人員的通用編輯器概述](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview)，同時牢記本節所述的AEM 6.5支援所需的必要變更。

## AEM 6.5與AEM as a Cloud Service之間的差異 {#differences}

AEM 6.5中的通用編輯器的運作方式與AEM as a Cloud Service大致相同，包括UI和大部分設定。 不過，請注意其中的差異。

* 6.5中的通用編輯器僅支援Headless使用案例。
* 通用編輯器的設定對6.5稍有不同（[如目前檔案所述](#setup)）。
* 6.5中的Universal Editor使用與AEM as a Cloud Service不同的資產選擇器和內容片段選擇器。
