---
title: 應用程式伺服器安裝
description: 瞭解如何使用應用程式伺服器安裝Adobe Experience Manager。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# 應用程式伺服器安裝{#application-server-install}

>[!NOTE]
>
>`JAR` 和 `WAR` Adobe Experience Manager (AEM)發行的檔案型別為何。 這些格式正在進行品質保證，以符合Adobe所承諾的支援等級。
>

本節將說明如何使用應用程式伺服器安裝Adobe Experience Manager (AEM)。 請參閱 [支援平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 區段，以瞭解針對個別應用程式伺服器提供的特定支援等級。

以下應用程式伺服器的安裝步驟已說明：

* [WebSphere](#websphere)
* [Jboss](#jboss-eap)
* [oracleWebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

請參閱適當的應用程式伺服器檔案，以取得有關安裝Web應用程式、伺服器設定以及如何啟動和停止伺服器的詳細資訊。

>[!NOTE]
>
>如果您在WAR部署中使用Dynamic Media，請參閱 [Dynamic Media檔案](/help/assets/config-dynamic.md#enabling-dynamic-media).

## 一般說明 {#general-description}

### 在應用程式伺服器中安裝AEM時的預設行為 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM會以單一war檔案的形式進行部署。

如果部署，預設將會發生下列情況：

* 執行模式為 `author`
* 執行個體（存放庫、Felix OSGI環境、套件組合等）安裝於中 `${user.dir}/crx-quickstart`位置 `${user.dir}` 是當前工作目錄，系統會呼叫crx-quickstart的此路徑 `sling.home`

* 前後關聯根目錄是war檔案名稱，例如，  `aem-6`

#### 設定 {#configuration}

您可以透過下列方式變更預設行為：

* 執行模式：設定 `sling.run.modes` 中的引數 `WEB-INF/web.xml` 部署前AEM war檔案的檔案

* sling.home：設定 `sling.home` 中的引數 `WEB-INF/web.xml`部署前AEM war檔案的檔案

* 內容根目錄：重新命名AEM war檔案

#### 發佈安裝 {#publish-installation}

若要部署發佈執行個體，您必須將執行模式設定為發佈：

* 從AEM war檔案中解壓縮WEB-INF/web.xml
* 將sling.run.modes引數變更為發佈
* 將web.xml檔案重新封裝成AEM war檔案
* 部署AEM war檔案

#### 安裝檢查 {#installation-check}

若要檢查是否已安裝all，您可以：

* 追蹤 `error.log`檔案以檢視是否已安裝所有內容
* 檢視 `/system/console` 已安裝所有組合

#### 同一應用程式伺服器上的兩個執行個體 {#two-instances-on-the-same-application-server}

為了示範，將製作和發佈例項安裝在一個應用程式伺服器上可能是適當的。 為此，請執行以下操作：

1. 變更發佈執行個體的sling.home變數和sling.run.modes變數。
1. 從AEM war檔案中解壓縮WEB-INF/web.xml檔案。
1. 將sling.home引數變更為不同的路徑（可以使用絕對和相對路徑）。
1. 將sling.run.modes變更為針對發佈執行個體發佈。
1. 重新封裝web.xml檔案。
1. 重新命名war檔案，使其名稱不同。 例如，一個重新命名為aemauthor.war，另一個重新命名為aempublish.war。
1. 使用較高的記憶體設定。 例如，預設AEM執行個體使用 `-Xmx3072m`
1. 部署兩個網頁應用程式。
1. 部署後，請停止兩個Web應用程式。
1. 在製作和發佈執行個體中，都會確保在sling.properties檔案中，屬性felix.service.urlhandlers=false設為false （預設為設為true）。
1. 再次啟動兩個網頁應用程式。

## 應用程式伺服器的安裝程式 {#application-servers-installation-procedures}

### WebSphere® 8.5 {#websphere}

部署前請閱讀 [一般說明](#general-description) 以上。

**伺服器準備**

* 讓基本驗證標題通過：

   * 讓AEM驗證使用者身份的一種方法是停用WebSphere®伺服器的全域管理安全性，若要這樣做：請移至[安全性] > [全域安全性]，然後取消勾選[啟用管理安全性]核取方塊，儲存並重新啟動伺服器。

* 設定 `"JAVA_OPTS= -Xmx2048m"`
* 如果您要使用內容根目錄= /安裝AEM，請變更現有預設Web應用程式的內容根目錄。

**部署AEM Web應用程式**

* 下載AEM war檔案
* 如有需要，請在web.xml中進行設定（請參閱上文「一般說明」中的）

   * 解壓縮WEB-INF/web.xml檔案
   * 將sling.run.modes引數變更為發佈
   * 取消註解sling.home初始引數，並視需要設定此路徑
   * 重新封裝web.xml檔案

* 部署AEM war檔案

   * 選擇內容根目錄（如果要設定Sling執行模式，則需要選取部署精靈的詳細步驟，然後在精靈的步驟6中指定）

* 啟動AEM網頁應用程式

#### JBoss® EAP 6.3.0/6.4.0 {#jboss-eap}

部署前請閱讀 [一般說明](#general-description) 以上。

**準備JBoss®伺服器**

在conf檔案中設定記憶體引數(例如， `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

如果您使用部署掃描器來安裝AEM Web應用程式，則增加 `deployment-timeout,` 針對該集合 `deployment-timeout` 屬性(例如： `configuration/standalone.xml)`：

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**部署AEM Web應用程式**

* 在您的JBoss®管理主控台中上傳AEM Web應用程式。

* 啟用AEM網頁應用程式。

#### oracleWebLogic 12.1.3/12.2 {#oracle-weblogic}

部署前請閱讀 [一般說明](#general-description) 以上。

這會使用僅含管理伺服器的簡單伺服器配置。

**WebLogic伺服器準備**

* 在 `${myDomain}/config/config.xml`新增至security-configuration區段：

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 檢視於 [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) 正確位置（預設情況下，將其定位在截面末尾是ok）

* 增加VM記憶體設定：

   * open `${myDomain}/bin/setDomainEnv.cmd` (resp .sh)搜尋WLS_MEM_ARGS，設定，例如，設定 `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * 重新啟動WebLogic Server

* 在中建立 `${myDomain}` 套件資料夾和cq資料夾內及Plan資料夾內

**部署AEM Web應用程式**

* 下載AEM war檔案
* 將AEM war檔案放入${myDomain}/packages/cq資料夾
* 在中進行設定 `WEB-INF/web.xml` 如有需要（請參閱上述「一般說明」）

   * 解壓縮 `WEB-INF/web.xml`檔案
   * 將sling.run.modes引數變更為發佈
   * 取消註解sling.home初始引數並視需要設定此路徑（請參閱一般說明）
   * 重新封裝web.xml檔案

* 將AEM war檔案部署為應用程式（其他設定則使用預設設定）
* 安裝可能需要一些時間……
* 檢查安裝是否已如一般說明中所述完成（例如，追蹤error.log）
* 您可以在WebLogic中Web應用程式的「組態」標籤中變更前後關聯根目錄 `/console`

#### Tomcat 8/8.5 {#tomcat}

部署前請閱讀 [一般說明](#general-description) 以上。

* **準備Tomcat伺服器**

   * 增加VM記憶體設定：

      * 在 `bin/catalina.bat` (resp `catalina.sh` 在UNIX®上)新增下列設定：
      * `set "JAVA_OPTS= -Xmx2048m`

   * Tomcat在安裝時不會啟用管理員或管理員存取權。 因此，您必須手動編輯 `tomcat-users.xml` 若要允許這些帳戶的存取：

      * 編輯 `tomcat-users.xml` 以包含「管理員」和「管理員」的存取權。 設定看起來應該類似下列範例：

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

   * 如果您想要以內容根目錄「/」部署AEM，則必須變更現有ROOT Webapp的內容根目錄：

      * 停止和取消部署ROOT Web應用程式
      * 重新命名tomcat webapps資料夾中的ROOT.war資料夾
      * 再次啟動Web應用程式

   * 如果您使用管理員gui安裝AEM Web應用程式，則需要增加上傳檔案的最大大小，因為預設僅允許50MB上傳大小。 針對開啟管理程式Web應用程式的web.xml，

     `webapps/manager/WEB-INF/web.xml`

     並將max-file-size和max-request-size增加到至少500MB，請參閱以下內容 `multipart-config` 此類的範例 `web.xml` 檔案。

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
   * 如有需要，請在web.xml中進行設定（請參閱上文「一般說明」中的）

      * 解壓縮WEB-INF/web.xml檔案
      * 將sling.run.modes引數變更為發佈
      * 取消註解sling.home初始引數，並視需要設定此路徑
      * 重新封裝web.xml檔案

   * 如果您想要將AEM war檔案部署為根webapp，請將其重新命名為ROOT.war；例如，如果您想要將aemauthor部署為內容根，請將其重新命名為aemauthor.war
   * 將其複製到tomcat的webapps資料夾
   * 等到安裝AEM為止

## 疑難排解 {#troubleshooting}

如需有關處理安裝期間可能出現問題的資訊，請參閱：

* [疑難排解](/help/sites-deploying/troubleshooting.md)
