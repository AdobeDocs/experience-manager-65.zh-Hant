---
title: 應用程式伺服器安裝
seo-title: 應用程式伺服器安裝
description: 瞭解如何與應AEM用程式伺服器一起安裝。
seo-description: 瞭解如何與應AEM用程式伺服器一起安裝。
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
translation-type: tm+mt
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---


# 應用程式伺服器安裝{#application-server-install}

>[!NOTE]
>
>`JAR` 和 `WAR` 中是否發AEM行檔案類型。這些格式正在進行質量保證，以滿足Adobe所承諾的支援級別。


本節將告訴您如何將Adobe Experience Manager(AEM)與應用程式伺服器一起安裝。 請參閱[支援的平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers)一節，瞭解個別應用程式伺服器的特定支援等級。

說明下列應用程式伺服器的安裝步驟：

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [OracleWebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

有關安裝Web應用程式、伺服器配置以及如何啟動和停止伺服器的詳細資訊，請參閱相應的應用程式伺服器文檔。

>[!NOTE]
>
>如果您在WAR部署中使用Dynamic Media，請參閱[Dynamic Media文檔](/help/assets/config-dynamic.md#enabling-dynamic-media)。

## 一般說明{#general-description}

### 在應用程AEM序伺服器{#default-behaviour-when-installing-aem-in-an-application-server}中安裝時的預設行為

作AEM為要部署的單一戰爭檔案。

如果部署了以下內容，則預設情況下會發生：

* 運行模式為`author`
* 實例（儲存庫、Felix OSGI環境、捆綁包等） 安裝在`${user.dir}/crx-quickstart`中，其中`${user.dir}`是當前工作目錄，此crx-quickstart路徑稱為`sling.home`

* context root is the war file name efe:`aem-6`

#### 設定 {#configuration}

您可以以下列方式變更預設行為：

* 運行模式：在部署前，在war檔案的`WEB-INF/web.xml`檔案中配置`sling.run.modes`AEM參數

* sling.home:在部署前，在war檔案的`WEB-INF/web.xml`檔案中配置`sling.home`AEM參數

* 上下文根：更名AEMwar檔案

#### 發佈安裝{#publish-installation}

若要部署發佈例項，您必須將執行模式設定為發佈：

* 從war檔案中解壓縮AEMWEB-INF/web.xml檔案
* 將sling.run.modes參數變更為發佈
* 將web.xml檔案重新整AEM理為war檔案
* 部署AEMwar檔案

#### 安裝檢查{#installation-check}

若要檢查是否已安裝全部，您可以：

* 尾隨`error.log`檔案，查看所有內容已安裝
* 在`/system/console`中查看所有捆綁包

#### 同一應用程式伺服器{#two-instances-on-the-same-application-server}上的兩個實例

為了展示，您可在單一應用程式伺服器上安裝作者和發佈執行個體。 如此，請執行下列動作：

1. 變更publish例項的sling.home變數和sling.run.modes變數。
1. 從war檔案解壓縮WEB-INF/web.xmlAEM檔案。
1. 將sling.home參數變更為不同的路徑（可能有絕對和相對路徑）。
1. 將sling.run.modes變更為publish執行個體的發佈。
1. 回復web.xml檔案。
1. 更名war檔案，使它們具有不同的名稱：例如，一個重新命名為aemauthor.war，另一個重新命名為aempublish.war。
1. 使用較高的記憶體設定，例如，對於預設AEM實例，使用例如：-Xmx3072m
1. 部署兩個Web應用程式。
1. 部署後，請停止兩個Web應用程式。
1. 在作者和發佈例項中，都可確保在sling.properties檔案中，屬性felix.service.urlhandlers=false會設為false（預設值為true）。
1. 再次啟動兩個Web應用程式。

## 應用程式伺服器安裝過程{#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

部署前，請閱讀上述[一般說明](#general-description)。

**伺服器準備**

* 讓基本驗證標題傳遞：

   * 驗證用AEM戶的一種方法是禁用WebSphere伺服器的全局管理安全性，這樣做：轉至「Security -> Global Security」（安全性->全域安全性），並取消選中「Enable administrative security」（啟用管理安全性）複選框，保存並重新啟動伺服器。

* set `"JAVA_OPTS= -Xmx2048m"`
* 如果您想使用上AEM下文根= /安裝，則必須首先更改現有預設Web應用程式的上下文根

**部署網AEM頁應用程式**

* 下載AEMwar檔案
* 視需要在web.xml中進行設定（請參閱上述一般說明）

   * 解壓縮WEB-INF/web.xml檔案
   * change sling.run.modes參數以發佈
   * uncomment sling.home初始參數，並視需要設定此路徑
   * Repack web.xml檔案

* 部署AEMwar檔案

   * 選擇上下文根目錄（如果您想要設定sling執行模式，則需要選取部署精靈的詳細步驟，然後在精靈的步驟6中指定）

* 啟動WebAEM應用程式

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

部署前，請閱讀上述[一般說明](#general-description)。

**準備JBoss伺服器**

在配置檔案中設定記憶體參數(如`standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

如果您使用deployment-scanner安裝Web應用程AEM式，則最好在實例的xml檔案中增加該設定`deployment-timeout`屬性的`deployment-timeout,`(例如`configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**部署網AEM頁應用程式**

* 在JBoss管AEM理控制台中上載Web應用程式。

* 啟用網AEM頁應用程式。

#### OracleWebLogic 12.1.3/12.2 {#oracle-weblogic}

部署前，請閱讀上述[一般說明](#general-description)。

這會使用簡單的伺服器配置，僅包含管理伺服器。

**WebLogic伺服器準備**

* 在`${myDomain}/config/config.xml`中，添加到安全配置部分：

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 請參 [閱https://xmlns.oracle.com/weblogic/domain/1.0/domain.](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) xsdd以取得正確位置（依預設，將其定位在區段結尾是可以的）

* 增加虛擬機記憶體設定：

   * 開啟`${myDomain}/bin/setDomainEnv.cmd`(resp .sh)搜索WLS_MEM_ARGS，設定e.g set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * 重新啟動WebLogic Server

* 在`${myDomain}`中建立包資料夾，在cq資料夾內建立Plan資料夾

**部署網AEM頁應用程式**

* 下載AEMwar檔案
* 將AEMwar檔案放入${myDomain}/packages/cq檔案夾
* 視需要在`WEB-INF/web.xml`中進行配置（請參閱上面的「一般說明」）

   * 解壓縮`WEB-INF/web.xml`檔案
   * change sling.run.modes參數以發佈
   * uncomment sling.home初始參數，並視需要設定此路徑（請參閱一般說明）
   * Repack web.xml檔案

* 將warAEM檔案部署為應用程式（對於其他設定，請使用預設設定）
* 安裝可能需要時間……
* 檢查「General Description（一般說明）」中的上述安裝是否已完成（例如，跟蹤error.log）
* 您可以在WebLogic `/console`中更改Web應用程式的「配置」頁籤中的上下文根

#### Tomcat 8/8.5 {#tomcat}

部署前，請閱讀上述[一般說明](#general-description)。

* **準備Tomcat伺服器**

   * 增加虛擬機記憶體設定：

      * 在`bin/catalina.bat`（在unix上為`catalina.sh`）中添加以下設定：
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat在安裝時不允許管理員或管理員訪問。 因此，您必須手動編輯`tomcat-users.xml`才能允許訪問這些帳戶：

      * 編輯`tomcat-users.xml`以包含管理員和管理員的存取權。 配置看起來應類似下列範例：

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
   * 如果您想要使用上AEM下文根&quot;/&quot;進行部署，則必須更改現有ROOT Web應用程式的上下文根：

      * 停止和取消部署ROOT Webapp
      * 在tomcat的Webapps資料夾中更名ROOT.war資料夾
      * 再次啟動網頁應用程式
   * 如果您使用AEMmanager-gui安裝Web應用程式，則需要增加已上傳檔案的最大大小，因為預設僅允許50MB的上傳大小。 若要開啟管理器網頁應用程式的web.xml,

      `webapps/manager/WEB-INF/web.xml`

      並將max-file-size和max-request-size增加到至少500MB，請參閱以下此類`web.xml`檔案的`multipart-config`示例。

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **部署網AEM頁應用程式**

   * 下載AEMwar檔案
   * 視需要在web.xml中進行設定（請參閱上述一般說明）

      * 解壓縮WEB-INF/web.xml檔案
      * change sling.run.modes參數以發佈
      * uncomment sling.home初始參數，並視需要設定此路徑
      * Repack web.xml檔案
   * 如果AEM您想要將war檔案部署為根網路應用程式，請將war檔案重新命名為ROOT.war，如果您想要讓aemauthor做為內容根，請將它重新命名為eamouthor.war
   * 將其複製到tomcat的webapps資料夾
   * 等待AEM直到安裝


## 疑難排解 {#troubleshooting}

有關處理安裝過程中可能出現的問題的資訊，請參見：

* [疑難排解](/help/sites-deploying/troubleshooting.md)
