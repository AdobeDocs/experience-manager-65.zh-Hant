---
title: 應用程式伺服器安裝
seo-title: Application Server Install
description: 瞭解如何使用應AEM用程式伺服器安裝。
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
>`JAR` 和 `WAR` 是否在中AEM釋放檔案類型。 這些格式正在進行質量保證，以滿足Adobe承諾的支助級別。

本節介紹如何使用應用程式服AEM務器安裝Adobe Experience Manager。 咨詢 [支援的平台](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 查看為各個應用程式伺服器提供的特定支援級別。

介紹了以下應用程式伺服器的安裝步驟：

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0/6.4.0](#jboss-eap)
* [OracleWebLogic 12.1.3/12.2](#oracle-weblogic)
* [Tomcat 8/8.5](#tomcat)

有關安裝Web應用程式、伺服器配置以及如何啟動和停止伺服器的詳細資訊，請參閱相應的應用程式伺服器文檔。

>[!NOTE]
>
>如果在WAR部署中使用Dynamic Media，請參閱 [Dynamic Media文檔](/help/assets/config-dynamic.md#enabling-dynamic-media)。

## 一般說明 {#general-description}

### 在應用程式伺服器AEM中安裝時的預設行為 {#default-behaviour-when-installing-aem-in-an-application-server}

作AEM為一個要部署的戰爭檔案。

如果部署，則預設情況下會發生以下情況：

* 運行模式為 `author`
* 實例（儲存庫、Felix OSGI環境、捆綁包等） 安裝於 `${user.dir}/crx-quickstart`何處 `${user.dir}` 是當前工作目錄，此crx-quickstart路徑稱為 `sling.home`

* 上下文根是war檔案名，例如： `aem-6`

#### 設定 {#configuration}

可以通過以下方式更改預設行為：

* 運行模式：配置 `sling.run.modes` 參數 `WEB-INF/web.xml` 部署前AEM的war檔案

* sling.home:配置 `sling.home` 參數 `WEB-INF/web.xml`部署前AEM的war檔案

* 上下文根：更名AEMwar檔案

#### 發佈安裝 {#publish-installation}

要部署發佈實例，您需要設定要發佈的運行模式：

* 從war檔案中解壓縮AEMWEB-INF/web.xml
* 將sling.run.modes參數更改為發佈
* 將web.xml檔案重新寫AEM入war檔案
* 部署戰AEM爭檔案

#### 安裝檢查 {#installation-check}

要檢查是否已安裝所有元件，您可以：

* 尾 `error.log`檔案以查看所有內容都已安裝
* 看 `/system/console` 安裝所有捆綁包

#### 同一應用程式伺服器上的兩個實例 {#two-instances-on-the-same-application-server}

為了進行演示，可以在一個應用程式伺服器中安裝作者和發佈實例。 為此，請執行以下操作：

1. 更改發佈實例的sling.home變數和sling.run.modes變數。
1. 從war檔案中解壓縮WEB-INF/web.xmlAEM檔案。
1. 將sling.home參數更改為其他路徑（可以使用絕對路徑和相對路徑）。
1. 將sling.run.modes更改為發佈實例的發佈。
1. 重新編寫web.xml檔案。
1. 更名戰爭檔案，以便它們有不同的名稱：例如，一個更名為aemauthor.war，另一個更名為aempublish.war。
1. 使用較高的記憶體設定，例如，對於默AEM認實例，使用如：-Xmx3072m
1. 部署兩個Web應用程式。
1. 部署後停止兩個Web應用程式。
1. 在作者實例和發佈實例中，都確保在sling.properties檔案中，屬性felix.service.urlhandlers=false設定為false（預設設定為true）。
1. 再次啟動兩個Web應用程式。

## 應用程式伺服器安裝過程 {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

在部署之前，請 [一般說明](#general-description) 上。

**伺服器準備**

* 讓基本身份驗證標頭傳遞：

   * 讓用戶驗證AEM的一種方法是禁用WebSphere伺服器的全局管理安全性，以執行此操作：轉到「安全」 — >「全局安全」並取消選中「啟用管理安全」複選框，保存並重新啟動伺服器。

* set `"JAVA_OPTS= -Xmx2048m"`
* 如果要使用上AEM下文根= /進行安裝，則必須首先更改現有預設Web應用程式的上下文根

**部署AEMWeb應用程式**

* 下載AEM戰爭檔案
* 根據需要在web.xml中進行配置（請參閱上面的「一般說明」）

   * 解壓縮WEB-INF/web.xml檔案
   * 更改sling.run.modes參數以發佈
   * 取消注釋sling.home初始參數，根據需要設定此路徑
   * Repack web.xml檔案

* 部署戰AEM爭檔案

   * 選擇上下文根（如果要設定引導運行模式，則需要選擇部署嚮導的詳細步驟，然後在嚮導的步驟6中指定）

* 啟動AEMWeb應用程式

#### JBoss EAP 6.3.0/6.4.0 {#jboss-eap}

在部署之前，請 [一般說明](#general-description) 上。

**準備JBoss伺服器**

在配置檔案中設定記憶體參數(例如 `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

如果使用部署掃描程式來安裝AEMWeb應用程式，則最好增加 `deployment-timeout,` 對於那套 `deployment-timeout` 實例的xml檔案中的屬性(例如 `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**部署AEMWeb應用程式**

* 在JBoss管AEM理控制台中上載Web應用程式。

* 啟用AEMWeb應用程式。

#### OracleWebLogic 12.1.3/12.2 {#oracle-weblogic}

在部署之前，請 [一般說明](#general-description) 上。

這使用一個僅包含管理伺服器的簡單伺服器佈局。

**WebLogic伺服器準備**

* 在 `${myDomain}/config/config.xml`添加到「安全配置」部分：

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 查看 [https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) 正確位置（預設情況下，將其放置在節末端是可以的）

* 增加VM記憶體設定：

   * 開啟 `${myDomain}/bin/setDomainEnv.cmd` (resp .sh)搜索WLS_MEM_ARGS，設定如， `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * 重新啟動WebLogic伺服器

* 在中建立 `${myDomain}` 檔案包資料夾和cq資料夾及其計畫資料夾

**部署AEMWeb應用程式**

* 下載AEM戰爭檔案
* 將戰AEM爭檔案放入${myDomain}/packages/cq資料夾中
* 將配置 `WEB-INF/web.xml` 如果需要（請參閱上面的「一般說明」）

   * 解壓縮 `WEB-INF/web.xml`檔案
   * 更改sling.run.modes參數以發佈
   * 取消注釋sling.home初始參數，並根據需要設定此路徑（請參閱一般說明）
   * Repack web.xml檔案

* 將AEMwar檔案部署為應用程式（對於其他設定，使用預設設定）
* 安裝可能需要時間……
* 檢查「General Description（一般說明）」中上述安裝是否已完成（例如，跟蹤error.log）
* 可以在WebLogic中更改Web應用程式的「配置」頁籤中的上下文根 `/console`

#### Tomcat 8/8.5 {#tomcat}

在部署之前，請 [一般說明](#general-description) 上。

* **準備Tomcat伺服器**

   * 增加虛擬機記憶體設定：

      * 在 `bin/catalina.bat` (resp) `catalina.sh` 在unix上)添加以下設定：
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat在安裝時不允許管理員或管理員訪問。 因此，您必須手動編輯 `tomcat-users.xml` 允許訪問這些帳戶：

      * 編輯 `tomcat-users.xml` 以包括管理員和管理員的訪問權限。 配置應與以下示例類似：

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
   * 如果希望使用上AEM下文根「/」部署，則必須更改現有ROOT Webapp的上下文根：

      * 停止並取消部署ROOT Webapp
      * 更名tomcat的webapps資料夾中的ROOT.war資料夾
      * 再次啟動Webapp
   * 如果使用AEMmanager-gui安裝Web應用程式，則需要增加上載檔案的最大大小，因為預設情況下僅允許50MB的上載大小。 要開啟管理器Web應用程式的web.xml,

      `webapps/manager/WEB-INF/web.xml`

      並將最大檔案大小和最大請求大小增加到至少500MB，請參見以下 `multipart-config` 這樣的示例 `web.xml` 的子菜單。

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **部署AEMWeb應用程式**

   * 下載AEM戰爭檔案
   * 根據需要在web.xml中進行配置（請參閱上面的「一般說明」）

      * 解壓縮WEB-INF/web.xml檔案
      * 更改sling.run.modes參數以發佈
      * 取消注釋sling.home初始參數，根據需要設定此路徑
      * Repack web.xml檔案
   * 如果AEM希望將war檔案作為根Webapp部署，請將其更名為ROOT.war，如果希望將aemauthor作為上下文根，則將其更名為aemauthor.war
   * 將其複製到tomcat的webapps資料夾
   * 等AEM待安裝


## 疑難排解 {#troubleshooting}

有關處理安裝過程中可能出現的問題的資訊，請參閱：

* [疑難排解](/help/sites-deploying/troubleshooting.md)
