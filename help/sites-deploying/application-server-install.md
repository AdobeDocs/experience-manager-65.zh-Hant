---
title: 應用程式伺服器安裝
seo-title: Application Server Install
description: 了解如何使用應用程式伺服器安裝AEM。
seo-description: Learn how to install AEM with an application server.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# 應用程式伺服器安裝{#application-server-install}

>[!NOTE]
>
>`JAR` 和 `WAR` 是否在中發行檔案類型AEM。 這些格式正在進行質量保證，以滿足Adobe所承諾的支援級別。

本節說明如何使用應用程式伺服器安裝Adobe Experience Manager(AEM)。 請參閱 [支援平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 區段，查看為個別應用程式伺服器提供的特定支援層級。

以下應用程式伺服器的安裝步驟說明：

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [OracleWebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

有關安裝Web應用程式、伺服器配置以及如何啟動和停止伺服器的詳細資訊，請參閱相應的應用程式伺服器文檔。

>[!NOTE]
>
>如果您在WAR部署中使用Dynamic Media，請參閱 [Dynamic Media檔案](/help/assets/config-dynamic.md#enabling-dynamic-media).

## 一般說明 {#general-description}

### 在應用程式伺服器中安裝AEM時的預設行為 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM是要部署的單一戰爭檔案。

如果部署，預設會發生下列情況：

* 執行模式為 `author`
* 例項（存放庫、Felix OSGI環境、套件組合等） 安裝於 `${user.dir}/crx-quickstart`where `${user.dir}` 是當前工作目錄，此crx-quickstart路徑稱為 `sling.home`

* 上下文根是戰爭檔案名，例如： `aem-6`

#### 設定 {#configuration}

您可以透過下列方式變更預設行為：

* 執行模式：設定 `sling.run.modes` 參數 `WEB-INF/web.xml` 部署前的AEM war檔案

* sling.home:設定 `sling.home` 參數 `WEB-INF/web.xml`部署前的AEM war檔案

* 內容根：重新命名AEM戰爭檔案

#### 發佈安裝 {#publish-installation}

若要部署發佈執行個體，您必須將執行模式設為發佈：

* 從AEM War檔案中解壓縮WEB-INF/web.xml
* 將sling.run.modes參數變更為發佈
* 將web.xml檔案重寫為AEM war檔案
* 部署AEM war檔案

#### 安裝檢查 {#installation-check}

若要檢查是否已安裝全部，您可以：

* 跟蹤 `error.log`檔案，查看所有內容都已安裝
* 查看 `/system/console` 安裝所有套件

#### 同一應用程式伺服器上的兩個執行個體 {#two-instances-on-the-same-application-server}

為了示範的目的，可以在一個應用程式伺服器中安裝製作和發佈執行個體。 為此，請執行以下操作：

1. 變更發佈例項的sling.home變數和sling.run.modes變數。
1. 從AEM war檔案中解壓縮WEB-INF/web.xml檔案。
1. 將sling.home參數變更為不同的路徑（可使用絕對和相對路徑）。
1. 將sling.run.modes變更為發佈執行個體的發佈。
1. 重新修復web.xml檔案。
1. 更名戰爭檔案，以便它們有不同的名稱：例如，其中一個更名為aemauthor.war，而另一個更名為aempublish.war。
1. 使用較高的記憶體設定，例如，對於預設AEM例項，請使用：-Xmx3072m
1. 部署兩個Web應用程式。
1. 部署後停止兩個Web應用程式。
1. 在製作例項和發佈例項中，請確保在sling.properties檔案中，屬性felix.service.urlhandlers=false已設為false（預設為將其設為true）。
1. 重新啟動兩個Web應用程式。

## 應用程式伺服器安裝過程 {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

部署之前，請閱讀 [一般說明](#general-description) 上。

**伺服器準備**

* 讓基本驗證標題傳遞：

   * 允許AEM驗證用戶的一種方法是禁用WebSphere伺服器的全局管理安全性，這樣做：轉到「安全 — >全局安全」，並取消選中「啟用管理安全」複選框，保存並重新啟動伺服器。

* set `"JAVA_OPTS= -Xmx2048m"`
* 如果您想使用內容根= /安裝AEM，則必須先變更現有預設Web應用程式的內容根

**部署AEM Web應用程式**

* 下載AEM war檔案
* 視需要在web.xml中進行設定（請參閱上方的一般說明）

   * 解壓縮WEB-INF/web.xml檔案
   * 將sling.run.modes參數變更為發佈
   * 取消註解sling.home初始參數，並視需要設定此路徑
   * 重新修復web.xml檔案

* 部署AEM war檔案

   * 選擇上下文根（如果要設定Sling運行模式，則需要選擇部署嚮導的詳細步驟，然後在嚮導的步驟6中指定）

* 啟動AEM Web應用程式

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

部署之前，請閱讀 [一般說明](#general-description) 上。

**準備JBoss伺服器**

在您的「conf」檔案中設定記憶體引數(例如 `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

如果您使用的deployment-scanner來安裝AEM web應用程式，則增加 `deployment-timeout,` 對於 `deployment-timeout` 屬性(例如 `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**部署AEM Web應用程式**

* 在您的JBoss管理控制台中上傳AEM Web應用程式。

* 啟用AEM Web應用程式。

#### OracleWebLogic 12.1.3/12.2 {#oracle-weblogic}

部署之前，請閱讀 [一般說明](#general-description) 上。

這會使用簡單的伺服器配置，而只使用管理伺服器。

**WebLogic伺服器準備**

* 在 `${myDomain}/config/config.xml`新增至「安全設定」區段：

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 查看 [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) 對於正確位置（預設情況下，將其定位在截面末端為ok）

* 增加VM記憶體設定：

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp .sh)搜索WLS_MEM_ARGS，設定如下： `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * 重新啟動WebLogic伺服器

* 在中建立 `${myDomain}` 包資料夾和cq資料夾內，以及它的Plan資料夾

**部署AEM Web應用程式**

* 下載AEM war檔案
* 將AEM War檔案放入${myDomain}/packages/cq資料夾
* 在 `WEB-INF/web.xml` 視需要（請參閱上文的一般說明）

   * 解包 `WEB-INF/web.xml`檔案
   * 將sling.run.modes參數變更為發佈
   * 取消註解sling.home初始參數，並視需要設定此路徑（請參閱一般說明）
   * 重新修復web.xml檔案

* 將AEM war檔案部署為應用程式（對於其他設定，請使用預設設定）
* 安裝可能需要時間……
* 檢查安裝是否已如「一般說明」中所述完成（例如追蹤error.log）
* 您可以在WebLogic中Web應用程式的「配置」頁簽中更改上下文根 `/console`

#### Tomcat 8/8.5 {#tomcat}

部署之前，請閱讀 [一般說明](#general-description) 上。

* **準備Tomcat伺服器**

   * 增加VM記憶體設定：

      * 在 `bin/catalina.bat` (resp `catalina.sh` 在unix上)新增下列設定：
      * `set "JAVA_OPTS= -Xmx2048m`
   * 安裝時，Tomcat不會啟用管理員或管理員的訪問權限。 因此，您必須手動編輯 `tomcat-users.xml` 允許訪問這些帳戶：

      * 編輯 `tomcat-users.xml` 包括管理員和管理員的存取權。 設定看起來應類似下列範例：

         ```xml
         <?xml version='1.0' encoding='utf-8'?>
         <tomcat-users>
         role rolename="manager"/>
         role rolename="tomcat"/>
         <role rolename="admin"/>
         <role rolename="role1"/>
         <role rolename="manager-gui"/>
         <user username="both" password="tomcat" roles="tomcat,role1"/>
         <user username="tomcat" password="tomcat" roles="tomcat"/>
         <user username="admin" password="admin" roles="admin,manager-gui"/>
         <user username="role1" password="tomcat" roles="role1"/>
         </tomcat-users>
         ```
   * 如果您想使用內容根「/」部署AEM，則必須變更現有ROOT網頁應用程式的內容根：

      * 停止和取消部署ROOT Webapp
      * 更名tomcat的Webapps資料夾中的ROOT.war資料夾
      * 再次啟動網頁應用
   * 如果您使用管理器 — gui安裝AEM Web應用程式，則需要增加上傳檔案的最大大小，因為預設僅允許50MB的上傳大小。 為了開啟管理器Web應用程式的web.xml,

      `webapps/manager/WEB-INF/web.xml`

      並將檔案大小上限和請求大小上限增加到至少500MB，請參閱下列內容 `multipart-config` 這樣a `web.xml` 檔案。

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **部署AEM Web應用程式**

   * 下載AEM war檔案
   * 視需要在web.xml中進行設定（請參閱上方的一般說明）

      * 解壓縮WEB-INF/web.xml檔案
      * 將sling.run.modes參數變更為發佈
      * 取消註解sling.home初始參數，並視需要設定此路徑
      * 重新修復web.xml檔案
   * 如果您想要將AEM war檔案部署為根Web應用程式，請將其更名為ROOT.war，如果您想要將aemouther作為上下文根，請將其更名為eamouthor.war
   * 將其複製到tomcat的webapps資料夾中
   * 等到安裝AEM為止


## 疑難排解 {#troubleshooting}

有關處理安裝過程中可能出現的問題的資訊，請參閱：

* [疑難排解](/help/sites-deploying/troubleshooting.md)
