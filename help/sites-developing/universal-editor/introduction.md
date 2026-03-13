---
title: 通用編輯器
description: 瞭解通用編輯器的靈活性，以及它如何幫助您使用6.5來提供無AEM頭的體驗。
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: 28e44586c6a8596037a44fa10d21b3fdcdea1606
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 24%

---


# 通用編輯器 {#universal-editor}

瞭解通用編輯器的靈活性，以及它如何幫助您使用6.5來提供無AEM頭的體驗。

## 概觀 {#overview}

通用編輯器是一個多功能視覺化編輯器，是 Adobe Experience Manager Sites 的一部分。它使作者能夠對任何無頭體驗進行「所見即所得」(WYSIWYG)編輯。

* 作者受益於通用編輯器的靈活性，因為它支援對所有形式的無頭內容進行相同的可AEM視編輯。
* 開發人員受益於通用編輯器的通用性，因為它還支援實現的真正解耦。 它允許開發人員利用他們選擇的幾乎任何框架或體系結構，而不施加任何SDK或技術限制。

有關詳細資訊，請參閱通用編輯器[上的](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)AEM作為雲服務文檔。

## 架構 {#architecture}

Universal Editor是一項與AEM搭配使用的服務，可讓您無頭製作內容。

* Universal Editor託管於`https://experience.adobe.com/#/aem/editor/canvas`，可編輯AEM 6.5轉譯的頁面。
* Universal Editor會透過AEM作者例項中的Dispatcher讀取AEM頁面。
* 通用編輯器服務（與Dispatcher運行在同一主機上）將更改寫回作AEM者實例。

![使用通用編輯器的作者流](assets/author-flow.png)

## 要求 {#requirements}

以下工具支援通用編輯器：

* AEM 6.5
   * 同時支援內部部署和AMS*託管。
* [AEM 6.5 LTS](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * 同時支援內部部署和AMS*託管。
* [AEM作為雲服務](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)

本檔案重點介AEM紹對通用編輯器的6.5支援。 要將通用編輯器與AEM6.5一起使用，您需要：

* AEM 6.5（帶Service Pack 23或更高版本）
   * [功能包也支援Service Pack 21和22。](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip)。
* 已正確配置調度程式

>[!NOTE]
>
>*如果您使用Managed ServicesAdobe(AMS)，請聯繫您的客戶成功工程師(CSE)，如果您希望使用通用編輯器。

## 設定 {#setup}

要測試通用編輯器，您需要：

1. [設定本地通用編輯器服務。](#set-up-ue)
1. [調整調度程式以允許通用編輯器服務。](#update-dispatcher)

完成安裝後，您可以[利用應用程式使用通用編輯器。](#instrumentation)

### 設定服務 {#configure-services}

通用編輯器利用需要附加配置的幾個包。

#### 為`login-token`cookie設定SameSite屬性。 {#samesite-attribute}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Adobe花崗岩令牌身份驗證處理程式**，然後按一下&#x200B;**更改配置值**。
1. 在對話方塊中，將登入權杖cookie **(**)值的`token.samesite.cookie.attr`SameSite屬性變更為`Partitioned`。
1. 按一下&#x200B;**儲存**。

#### 刪除`SAMEORIGIN`標頭X-Frame選項。 {#sameorigin}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Apache Sling主Servlet**，然後按一下&#x200B;**編輯配置值**。
1. 從`X-Frame-Options=SAMEORIGIN`其他響應標頭&#x200B;**屬性(**)中刪除`sling.additional.response.headers`值（如果存在）。
1. 按一下&#x200B;**儲存**。

#### 配置Adobe花崗岩查詢參數身份驗證處理程式。 {#query-parameter}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到&#x200B;**Adobe花崗岩查詢參數身份驗證處理程式**，然後按一下&#x200B;**編輯配置值**。
1. 在&#x200B;**路徑**&#x200B;欄位(`path`)中，添加`/`以啟用。
   * 空值會停用驗證處理常式。
1. 按一下&#x200B;**儲存**。

#### 定義應開啟通用編輯器的內容路徑或`sling:resourceTypes`。 {#paths}

1. 開啟 Configuration Manager。
   * `http://<host>:<port>/system/console/configMgr`
1. 在清單中找到「**通用編輯器 URL 服務**」，然後按一下「**編輯設定值**」。
1. 定義將開啟通用編輯器的內容路徑或`sling:resourceTypes`。
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

以下變數可用於定義`Universal Editor Opening Mapping`下的映射。

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
* 在遠程NextJS伺服器上開啟`/content/bar`下的所有頁面，提供所有變數作為資訊
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * 這樣會開啟 `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### 設定通用編輯器服務 {#set-up-ue}

更新並設定AEM後，您就可以設定本機通用編輯器服務，以供您自己的本機開發和測試使用。

1. 安裝Node.js version >=20。
1. 從[Software Distribution](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud/software-distribution/home)下載並解除封裝最新的Universal Editor服務
1. 透過環境變數或`.env`檔案設定Universal Editor Service。
   * [如需詳細資訊，請參閱AEM as a Cloud Service Universal Editor檔案。](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * 請注意，如果需要內部IP重寫，則可能需要使用`UES_MAPPING`選項。
1. 運行`universal-editor-service.cjs`

### 更新調度程式 {#update-dispatcher}

配AEM置並運行本地通用編輯器服務後，您需要允許調度程式中新服務[的反向代理。](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-dispatcher/using/dispatcher)

1. 調整作者實例的vhost檔案以包括反向代理。

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080是預設埠。 如果您使用`UES_PORT`[檔案中的`.env`參數更改了此項，](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)則必須相應地調整此處的埠值。

1. 重新啟動Apache。

## 檢測您的應用程式 {#instrumentation}

更新AEM並執行本機Universal Editor Service後，您就可以使用Universal Editor開始編輯Headless內容。

不過，您的應用程式必須檢測為使用通用編輯器。 這涉及包括中繼標籤，以指示編輯器如何以及在何處保留內容。 此工具的詳細資訊可在[通用編輯器文檔中找到，用於將AEM作為雲服務。](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

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

## 6.AEM5與AEM作為雲服務的區別 {#differences}

6.5中的通AEM用編輯器與AEM中的雲服務（包括UI和大部分安裝程式）的工作方式大體相同。 但是，還有一些分歧值得注意。

* 6.5中的通用編輯器僅支援無頭使用情形。
* 通用編輯器的設定在6.5時稍有變化（如當前文檔中所述[）。](#setup)
* 6.5中的通用編輯器使用與AEM不同的資產選取器和內容片段選取器作為雲服務。
