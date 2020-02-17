---
title: 應用程式伺服器安裝
seo-title: 應用程式伺服器安裝
description: 瞭解如何與應用程式伺服器一起安裝AEM。
seo-description: 瞭解如何與應用程式伺服器一起安裝AEM。
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 應用程式伺服器安裝{#application-server-install}

>[!NOTE]
>
>`JAR` 以 `WAR` 及AEM是否在中發行檔案類型。 這些格式正在進行品質保證，以符合Adobe所承諾的支援等級。


本節會告訴您如何與應用程式伺服器一起安裝Adobe Experience Manager(AEM)。 請參閱「 [支援的平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 」一節，瞭解個別應用程式伺服器的特定支援等級。

說明下列應用程式伺服器的安裝步驟：

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [Oracle webLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

有關安裝Web應用程式、伺服器配置以及如何啟動和停止伺服器的詳細資訊，請參閱相應的應用程式伺服器文檔。

>[!NOTE]
>
>如果您在WAR部署中使用動態媒體，請參閱動態 [媒體檔案](/help/assets/config-dynamic.md#enabling-dynamic-media)。

## 一般說明 {#general-description}

### 在應用程式伺服器中安裝AEM時的預設行為 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM是要部署的單一戰爭檔案。

如果部署了以下內容，則預設情況下會發生：

* 運行模式為 `author`
* 實例（儲存庫、Felix OSGI環境、捆綁包等）安裝在當 `${user.dir}/crx-quickstart`前工 `${user.dir}` 作目錄中，則此crx-quickstart路徑稱為 `sling.home`

* context root is the war file name, ef: `aem-6`

#### 設定 {#configuration}

您可以以下列方式變更預設行為：

* 運行模式：在部署 `sling.run.modes` 前，先在AEM `WEB-INF/web.xml` war檔案的檔案中設定參數

* sling.home:在部署 `sling.home` 前，先在AEM `WEB-INF/web.xml`war檔案的檔案中設定參數

* 上下文根：重新命名AEM war檔案

#### 發佈安裝 {#publish-installation}

若要部署發佈例項，您必須將執行模式設定為發佈：

* 從AEM war檔案解壓縮WEB-INF/web.xml
* 將sling.run.modes參數變更為發佈
* 將web.xml檔案重新整理為AEM war檔案
* 部署AEM war檔案

#### 安裝檢查 {#installation-check}

若要檢查是否已安裝全部，您可以：

* 尾隨檔 `error.log`案，查看所有內容都已安裝
* 查看所 `/system/console` 有捆綁包

#### 同一應用程式伺服器上的兩個實例 {#two-instances-on-the-same-application-server}

為了展示，您可在單一應用程式伺服器上安裝作者和發佈執行個體。 如此，請執行下列動作：

1. 變更publish例項的sling.home變數和sling.run.modes變數。
1. 從AEM war檔案解壓縮WEB-INF/web.xml檔案。
1. 將sling.home參數變更為不同的路徑（可能有絕對和相對路徑）。
1. 將sling.run.modes變更為publish執行個體的發佈。
1. 回復web.xml檔案。
1. 更名war檔案，使它們具有不同的名稱：例如，一個重新命名為aemauthor.war，另一個重新命名為aempublish.war。
1. 使用較高的記憶體設定，例如，若是預設的AEM例項，則使用例如：-Xmx3072m
1. 部署兩個Web應用程式。
1. 部署後，請停止兩個Web應用程式。
1. 在作者和發佈例項中，都可確保在sling.properties檔案中，屬性felix.service.urlhandlers=false會設為false（預設值為true）。
1. 再次啟動兩個Web應用程式。

## 應用程式伺服器安裝過程 {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

部署前，請閱讀上 [述一般說明](#general-description) 。

**伺服器準備**

* 讓基本驗證標題傳遞：

   * 讓AEM驗證使用者的一種方式是停用WebSphere伺服器的全域管理安全性，以執行下列動作：轉至「Security -> Global Security」（安全性->全域安全性），並取消選中「Enable administrative security」（啟用管理安全性）複選框，保存並重新啟動伺服器。

* 設定`"JAVA_OPTS= -Xmx2048m"`
* 如果您想使用內容根目錄= /安裝AEM，則必須先變更現有預設Web應用程式的內容根目錄

**部署AEM網頁應用程式**

* 下載AEM war檔案
* 視需要在web.xml中進行設定（請參閱上述一般說明）

   * 解壓縮WEB-INF/web.xml檔案
   * change sling.run.modes參數以發佈
   * uncomment sling.home初始參數，並視需要設定此路徑
   * Repack web.xml檔案

* 部署AEM war檔案

   * 選擇上下文根目錄（如果您想要設定sling執行模式，則需要選取部署精靈的詳細步驟，然後在精靈的步驟6中指定）

* 啟動AEM web應用程式

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

部署前，請閱讀上 [述一般說明](#general-description) 。

**準備JBoss伺服器**

在配置檔案中設定記憶體參數(如 `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

如果您使用deployment-scanner來安裝AEM網頁應用程式，則最好在例項的xml檔案中增加該 `deployment-timeout,` 設定 `deployment-tiimeout` 屬性的值(例如 `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**部署AEM網頁應用程式**

* 在JBoss管理控制台中上傳AEM網頁應用程式。

* 啟用AEM網頁應用程式。

#### Oracle webLogic 12.1.3/12.2 {#oracle-weblogic}

部署前，請閱讀上 [述一般說明](#general-description) 。

這會使用簡單的伺服器配置，僅包含管理伺服器。

**WebLogic伺服器準備**

* 在添 `${myDomain}/config/config.xml`加到安全配置部分中：

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 請參 [閱https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) ，以取得正確的位置（依預設，若將其定位在區段結尾，則可以）

* 增加虛擬機記憶體設定：

   * 開 `${myDomain}/bin/setDomainEnv.cmd` 啟(resp.sh)搜尋WLS_MEM_ARGS，設定e.g set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * 重新啟動WebLogic Server

* 在包文 `${myDomain}` 件夾中建立，在cq資料夾內建立，並在其中建立Plan資料夾

**部署AEM網頁應用程式**

* 下載AEM war檔案
* 將AEM war檔案放入${myDomain}/packages/cq檔案夾
* 視需要進行 `WEB-INF/web.xml` 配置（請參閱上述一般說明）

   * 解壓縮檔 `WEB-INF/web.xml`案
   * change sling.run.modes參數以發佈
   * uncomment sling.home初始參數，並視需要設定此路徑（請參閱一般說明）
   * Repack web.xml檔案

* 將AEM war檔案部署為「應用程式」（對於其他設定，請使用預設設定）
* 安裝可能需要時間……
* 檢查「General Description（一般說明）」中的上述安裝是否已完成（例如，跟蹤error.log）
* 您可以在WebLogic中更改Web應用程式的「配置」頁籤中的上下文根 `/console`

#### Tomcat 8/8.5 {#tomcat}

部署前，請閱讀上 [述一般說明](#general-description) 。

* **準備Tomcat伺服器**

   * 增加虛擬機記憶體設定：

      * 在( `bin/catalina.bat` 在unix `catalina.sh` 上)中添加以下設定：
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat在安裝時不允許管理員或管理員訪問。 因此，您必須手動編輯才 `tomcat-users.xml` 能允許存取這些帳戶：

      * 編輯 `tomcat-users.xml` 以包含管理員和管理員的存取權。 配置看起來應類似下列範例：
      * 
         ```
         <?xml version='1.0' encoding='utf-8'?>
          <tomcat-users>
          <role rolename="manager"/>
          <role rolename="tomcat"/>
          <role rolename="admin"/>
          <role rolename="role1"/>
          <role rolename="manager-gui"/>
          <user username="both" password="tomcat" roles="tomcat,role1"/>
          <user username="tomcat" password="tomcat" roles="tomcat"/>
          <user username="admin" password="admin" roles="admin,manager-gui"/>
          <user username="role1" password="tomcat" roles="role1"/>
          </tomcat-users>
         ```
   * 如果您想要部署內容根目錄&quot;/&quot;的AEM，則必須變更現有ROOT網頁應用程式的內容根目錄：

      * 停止和取消部署ROOT Webapp
      * 在tomcat的Webapps資料夾中更名ROOT.war資料夾
      * 再次啟動網頁應用程式
   * 如果您使用Manager-gui安裝AEM web應用程式，則需要增加上傳檔案的最大大小，因為預設僅允許50MB的上傳大小。 若要開啟管理器網頁應用程式的web.xml,

      `webapps/manager/WEB-INF/web.xml`

      並將最大檔案大小和最大請求大小增加至至少500MB，請參閱下 `multipart-config` 列此類檔案范 `web.xml` 例：

      ```
        <multipart-config>
         <!-- 500MB max -->
         <max-file-size>524288000</max-file-size>
         <max-request-size>524288000</max-request-size>
         <file-size-threshold>0</file-size-threshold>
         </multipart-config>
      ```




* **部署AEM網頁應用程式**

   * 下載AEM war檔案
   * 視需要在web.xml中進行設定（請參閱上述一般說明）

      * 解壓縮WEB-INF/web.xml檔案
      * change sling.run.modes參數以發佈
      * uncomment sling.home初始參數，並視需要設定此路徑
      * Repack web.xml檔案
   * 如果您想要將AEM war檔案部署為根網路應用程式，請將它重新命名為ROOT.war，如果您想要讓aemauthor做為內容根目錄，請將它重新命名為eamouthor.war
   * 將其複製到tomcat的webapps資料夾
   * 等到安裝AEM為止


## 疑難排解 {#troubleshooting}

有關處理安裝過程中可能出現的問題的資訊，請參見：

* [疑難排解](/help/sites-deploying/troubleshooting.md)

