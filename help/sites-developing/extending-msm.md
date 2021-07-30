---
title: 擴展多站點管理器
seo-title: 擴展多站點管理器
description: 本頁面可協助您擴充多網站管理員的功能
seo-description: 本頁面可協助您擴充多網站管理員的功能
uuid: dfa7d050-29fc-4401-8d4d-d6ace6b49bea
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6128c91a-4173-42b4-926f-bbbb2b54ba5b
docset: aem65
exl-id: bba64ce6-8b74-4be1-bf14-cfdf3b9b60e1
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '2601'
ht-degree: 0%

---

# 擴展多站點管理器{#extending-the-multi-site-manager}

本頁面可協助您擴充多網站管理員的功能：

* 了解MSM Java API的主要成員。
* 建立可用於轉出設定的新同步動作。
* 修改預設語言和國家/地區代碼。

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>此頁面應與[重複使用內容一起閱讀：多站點管理員](/help/sites-administering/msm.md)。
>
>AEM 6.4中的以下網站存放庫重新調整可能也值得關注：
>* [多站點管理器Blueprint配置](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-blueprint-configurations)
>* [多網站管理員轉出設定](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-rollout-configurations)


>[!CAUTION]
>
>製作網站時會使用「多網站管理員」及其API，因此這些管理工具僅用於製作環境。

## Java API概觀 {#overview-of-the-java-api}

「多站點管理」包含以下包：

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主要MSM API物件互動如下（另請參閱[使用的詞語](/help/sites-administering/msm.md#terms-used)）:

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   `Blueprint`（如[blueprint configuration](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)中）指定即時副本可繼承內容的頁面。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * Blueprint配置(`Blueprint`)是可選的，但是：

      * 允許作者在來源上使用&#x200B;**轉出**&#x200B;選項（明確地）推送修改至繼承自此來源的即時副本。
      * 允許作者使用&#x200B;**建立網站**;這可讓使用者輕鬆選取語言並設定即時副本的結構。
      * 定義任何產生的Live Copy的預設轉出設定。

* **`LiveRelationship`**

   `LiveRelationship`指定即時副本分支中的資源與其等效源/藍圖資源之間的連接（關係）。

   * 在實現繼承和轉出時會使用關係。
   * `LiveRelationship` 物件提供對轉出設定( `RolloutConfig`)、和關 `LiveCopy`系相 `LiveStatus` 關物件的存取（參考）。

   * 例如，在`/content/copy/us`中，從`/content/we-retail/language-masters`的來源/Blueprint建立即時副本。 資源`/content/we.retail/language-masters/en/jcr:content`和`/content/copy/us/en/jcr:content`形成關係。

* **`LiveCopy`**

   `LiveCopy` 保留即時副本資源與其來源/blueprint資源之間關係( `LiveRelationship`)的設定詳細資料。

   * 使用`LiveCopy`類訪問頁面路徑、源/Blueprint頁面路徑、轉出配置以及子頁面是否也包含在`LiveCopy`中。

   * 每次使用&#x200B;**建立網站**&#x200B;或&#x200B;**建立即時副本**&#x200B;時，都會建立`LiveCopy`節點。

* **`LiveStatus`**

   `LiveStatus` 物件可提供對的執行階段狀態的存 `LiveRelationship`取。用於查詢即時副本的同步狀態。

* **`LiveAction`**

   `LiveAction`是在轉出中涉及的每個資源上執行的動作。

   * LiveActions僅由RolloutConfigs產生。

* **`LiveActionFactory`**

   建立給定`LiveAction`配置的`LiveAction`對象。 設定會儲存為存放庫中的資源。

* **`RolloutConfig`**

   `RolloutConfig`包含`LiveActions`清單，當觸發時使用。 `LiveCopy`繼承`RolloutConfig`，結果在`LiveRelationship`中顯示。

   * 第一次設定即時副本時，也會使用RolloutConfig（這會觸發LiveActions）。

## 建立新的同步操作 {#creating-a-new-synchronization-action}

建立要與轉出設定搭配使用的自訂同步動作。 當[已安裝的操作](/help/sites-administering/msm-sync.md#installed-synchronization-actions)不符合您的特定應用程式要求時，建立同步操作。 要執行此操作，請建立兩個類：

* 執行動作的[ `com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html)介面的實作。
* 實作[ `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html)介面並建立`LiveAction`類實例的OSGI元件。

`LiveActionFactory`為給定配置建立`LiveAction`類的實例：

* `LiveAction` 類包括以下方法：

   * `getName`:傳回動作的名稱。名稱是用來參照動作，例如轉出設定。
   * `execute`:執行動作的工作。

* `LiveActionFactory` 類包括以下成員：

   * `LIVE_ACTION_NAME`:包含關聯名稱的欄位 `LiveAction`。此名稱必須與`LiveAction`類的`getName`方法返回的值一致。

   * `createAction`:建立的例 `LiveAction`項。可選`Resource`參數可用於提供配置資訊。

   * `createsAction`:傳回關聯的名 `LiveAction`稱。

### 存取LiveAction設定節點 {#accessing-the-liveaction-configuration-node}

在儲存庫中使用`LiveAction`配置節點來儲存影響`LiveAction`實例的運行時行為的資訊。 儲存`LiveAction`配置的儲存庫中的節點在運行時可用於`LiveActionFactory`對象。 因此，您可以將屬性新增至的設定節點，並視需要在`LiveActionFactory`實作中使用。

例如， `LiveAction`需要儲存Blueprint作者的名稱。 配置節點的屬性包括儲存資訊的Blueprint頁的屬性名稱。 在執行階段， `LiveAction`會從設定中擷取屬性名稱，然後取得屬性值。

` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction`方法的參數是`Resource`對象。 此`Resource`物件代表轉出設定中此即時動作的`cq:LiveSyncAction`節點；請參閱[建立轉出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。 與通常使用配置節點時一樣，您應將其調整為`ValueMap`對象：

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### 訪問目標節點、源節點和LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

以下對象作為`LiveAction`對象的`execute`方法的參數提供：

* 代表即時副本來源的[ `Resource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html)物件。
* 代表即時副本目標的`Resource`物件。
* 即時副本的[ `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html)物件。
* `autoSave`值指示您的`LiveAction`是否應儲存對儲存庫所做的更改。

* 重設值表示轉出重設模式。

從這些對象中，可以獲取有關`LiveCopy`的所有資訊。 您也可以使用`Resource`物件來取得`ResourceResolver`、`Session`和`Node`物件。 這些對象對於控制儲存庫內容非常有用：

在以下代碼的第一行中，源是源頁的`Resource`對象：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>`Resource`參數可以是不適應`Node`對象（如[ `NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html)對象）的`null`或`Resources`對象。

## 建立新轉出設定 {#creating-a-new-rollout-configuration}

當安裝的轉出設定不符合您的應用程式需求時，建立轉出設定：

* [建立轉出設定](#create-the-rollout-configuration)。
* [將同步化動作新增至轉出設定](#add-synchronization-actions-to-the-rollout-configuration)。

接著，當您在Blueprint或Live Copy頁面上設定轉出設定時，即可使用新的轉出設定。

>[!NOTE]
>
>另請參閱自訂轉出的[最佳實務](/help/sites-administering/msm-best-practices.md#customizing-rollouts)。

### 建立轉出設定 {#create-the-rollout-configuration}

若要建立新轉出設定：

1. 開放CRXDE Lite;例如：
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 導航到 :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >這是您專案的自訂版本：
   >`/libs/msm/wcm/rolloutconfigs`
   >如果這是您的第一個設定，則必須建立。

   >[!NOTE]
   >
   >您不得變更/libs路徑中的任何項目。
   >這是因為下次升級執行個體時會覆寫/libs的內容（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
   >設定和其他變更的建議方法為：
   >* 在/apps下重新建立所需項目（即/libs中存在的項目）
   >* 在/apps內進行任何變更


1. 在此&#x200B;**Create**&#x200B;下，建立具有以下屬性的節點：

   * **名稱**:轉出設定的節點名稱。md#installed-synchronization-actions)，例如`contentCopy`或`workflow`。
   * **類型**:  `cq:RolloutConfig`

1. 將下列屬性新增至此節點：
   * **名稱**:  `jcr:title`

      **類型**:  `String`
      **值**:將出現在UI中的識別標題。
   * **名稱**:  `jcr:description`

      **類型**:  `String`
      **值**:選擇性說明。
   * **名稱**:  `cq:trigger`

      **類型**:  `String`
      **值**:要 [使用的](/help/sites-administering/msm-sync.md#rollout-triggers) 轉出觸發器。選擇：
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 按一下「**全部保存**」。

### 將同步化動作新增至轉出設定 {#add-synchronization-actions-to-the-rollout-configuration}

轉出配置儲存在您已在`/apps/msm/<your-project>/rolloutconfigs`節點下建立的[轉出配置節點](#create-the-rollout-configuration)下。

新增`cq:LiveSyncAction`類型的子節點，將同步動作新增至轉出設定。 同步操作節點的順序決定了操作發生的順序。

1. 仍在CRXDE Lite中，選取您的[轉出設定](#create-the-rollout-configuration)節點。

   例如：
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **** 建立節點，其節點屬性如下：

   * **名稱**:同步操作的節點名。名稱必須與[Synchronization Actions](/help/sites-administering/msm-sync.md#installed-synchronization-actions)下表格中的&#x200B;**Action Name**&#x200B;相同，例如`contentCopy`或`workflow`。
   * **類型**:  `cq:LiveSyncAction`

1. 根據需要添加和配置任意數量的同步操作節點。 重新排列動作節點，使其順序符合您希望其發生的順序。 最頂端的動作節點會先發生。

## 建立和使用簡單LiveActionFactory類 {#creating-and-using-a-simple-liveactionfactory-class}

請依照本節中的程式開發`LiveActionFactory`，並在轉出設定中使用。 該過程使用Maven和Eclipse來開發和部署`LiveActionFactory`:

1. [建立Maven](#create-the-maven-project) 專案並將其匯入Eclipse。
1. [將相](#add-dependencies-to-the-pom-file) 依性新增至POM檔案。
1. [實作介 `LiveActionFactory` ](#implement-liveactionfactory) 面並部署OSGi套件組合。
1. [建立轉出設定](#create-the-example-rollout-configuration)。
1. [建立即時副本](#create-the-live-copy)。

公用Git存放庫中提供Maven專案和Java類的原始碼。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟experiencemanager-java-msmrollout專案](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* 將專案下載為[a ZIP檔案](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### 建立Maven專案 {#create-the-maven-project}

下列程式需要您將adobe-public設定檔新增至Maven設定檔。

* 如需adobe-public設定檔的相關資訊，請參閱[取得內容套件Maven外掛程式](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* 有關Maven設定檔案的資訊，請參閱Maven [設定參考](https://maven.apache.org/settings.html)。

1. 開啟終端或命令列工作階段，並變更目錄以指向建立專案的位置。
1. 輸入以下命令：

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在互動式提示字元時指定下列值：

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`:  `MyLiveActionFactory`
   * `version`:  `1.0-SNAPSHOT`
   * `package`:  `MyPackage`
   * `appsFolderName`:  `myapp`
   * `artifactName`:  `MyLiveActionFactory package`
   * `packageGroup`:  `myPackages`

1. 啟動Eclipse並[匯入Maven專案](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse)。

### 將相依性新增至POM檔案 {#add-dependencies-to-the-pom-file}

添加依賴項，以便Eclipse編譯器可以引用`LiveActionFactory`代碼中使用的類。

1. 從Eclipse專案總管中，開啟檔案：

   `MyLiveActionFactory/pom.xml`

1. 在編輯器中，按一下`pom.xml`標籤，然後找到`project/dependencyManagement/dependencies`區段。
1. 在`dependencyManagement`元素內新增下列XML，然後儲存檔案。

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. 從&#x200B;**Project Explorer**&#x200B;的`MyLiveActionFactory-bundle/pom.xml`開啟套件組合的POM檔案。
1. 在編輯器中，按一下`pom.xml`標籤，然後找出專案/相依性區段。 在相依性元素內新增下列XML，然後儲存檔案：

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### 實作LiveActionFactory {#implement-liveactionfactory}

以下`LiveActionFactory`類實現了`LiveAction`，該記錄有關源頁和目標頁的消息，並將`cq:lastModifiedBy`屬性從源節點複製到目標節點。 即時動作的名稱為`exampleLiveAction`。

1. 在Eclipse項目資源管理器中，按一下右鍵`MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm`包，然後按一下&#x200B;**New** > **Class**。 對於&#x200B;**Name**，輸入`ExampleLiveActionFactory`，然後按一下&#x200B;**Finish**。
1. 開啟`ExampleLiveActionFactory.java`檔案，使用下列程式碼取代內容，然後儲存檔案。

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. 使用終端或命令會話，將目錄更改為`MyLiveActionFactory`目錄（Maven項目目錄）。 然後，輸入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   AEM `error.log`檔案應指示套件組合已啟動。

   例如， [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs)。

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### 建立範例轉出設定 {#create-the-example-rollout-configuration}

建立使用您建立之`LiveActionFactory`的MSM轉出設定：

1. 使用標準程式](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)建立並設定[轉出設定 — 並使用屬性：

   * **標題**:轉出設定範例
   * **名稱**:examplolloutconfig
   * **cq:trigger**:  `publish`

### 將即時動作新增至範例轉出設定 {#add-the-live-action-to-the-example-rollout-configuration}

設定您在前一個程式中建立的轉出設定，使其使用`ExampleLiveActionFactory`類別。

1. 開放CRXDE Lite;例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)。
1. 在`/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`下建立以下節點：

   * **名稱**:  `exampleLiveAction`
   * **類型**:  `cq:LiveSyncAction`

1. 按一下「**全部保存**」。
1. 選擇`exampleLiveAction`節點並添加以下屬性：

   * **名稱**:  `repLastModBy`
   * **類型**:  `Boolean`
   * **值**:  `true`

   此屬性向`ExampleLiveAction`類指示應將`cq:LastModifiedBy`屬性從源複製到目標節點。

1. 按一下「**全部保存**」。

### 建立即時副本 {#create-the-live-copy}

[使用您的轉](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 出設定，建立We.Retail參考網站的英文/產品分支的即時副本：

* **來源**:  `/content/we-retail/language-masters/en/products`

* **轉出設定**:轉出設定範例

激活源分支的&#x200B;**產品**（英語）頁，並觀察`LiveAction`類生成的日誌消息：

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

<!--
## Removing the Chapters Step in the Create Site Wizard {#removing-the-chapters-step-in-the-create-site-wizard}

In some cases, the **Chapters** selection is not required in the create site wizard (only the **Languages** selection is required). To remove this step in the default We.Retail English blueprint:

1. In CRX Explorer, remove the node:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigate to `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` and create a new node:

    1. **Name** = `chapters`; **Type** = `cq:Widget`.

1. Add following properties to the new node:

    1. **Name** = `name`; **Type** = `String`; **Value** = `msm:chapterPages`

    1. **Name** = `value`; **Type** = `String`; **Value** = `all`

    1. **Name** = `xtype`; **Type** = `String`; **Value** = `hidden`
-->

## 更改語言名稱和預設國家 {#changing-language-names-and-default-countries}

AEM使用一組預設的語言和國家/地區代碼。

* 預設語言代碼是由ISO-639-1定義的小寫、雙字母代碼。
* 預設國家/地區代碼是ISO 3166所定義的小寫或大寫雙字母代碼。

MSM會使用儲存的語言和國家/地區代碼清單，來判斷與頁面語言版本名稱相關聯的國家/地區名稱。 您可以視需要變更清單的下列方面：

* 語言標題
* 國家/地區名稱
* 語言的預設國家/地區（適用於`en`、`de`等代碼）

語言清單儲存在`/libs/wcm/core/resources/languages`節點下。 每個子節點代表一種語言或語言國家：

* 節點的名稱是語言代碼（如`en`或`de`），或language_country代碼（如`en_us`或`de_ch`）。

* 節點的`language`屬性儲存代碼語言的完整名稱。
* 節點的`country`屬性儲存代碼的國家/地區的完整名稱。
* 當節點名稱僅包含語言代碼時（如`en`），國家/地區屬性為`*`，而另一個`defaultCountry`屬性會儲存language-country的代碼，以指出要使用的國家/地區。

![chlimage_1-76](assets/chlimage_1-76.png)

要修改語言，請執行以下操作：

1. 在網頁瀏覽器中開啟CRXDE Lite;例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. 選擇`/apps`資料夾，然後按一下&#x200B;**Create**，然後按一下&#x200B;**Create Folder。**

   將新資料夾命名為`wcm`。

1. 重複上一步以建立`/apps/wcm/core`資料夾樹。 在`core`中建立名為`resources`的`sling:Folder`類型的節點。 <!-- ![chlimage_1-77](assets/chlimage_1-77.png) -->

1. 按一下右鍵`/libs/wcm/core/resources/languages`節點，然後按一下&#x200B;**Copy**。
1. 按一下右鍵`/apps/wcm/core/resources`資料夾，然後按一下&#x200B;**貼上**。 根據需要修改子節點。
1. 按一下「**全部保存**」。
1. 按一下&#x200B;**工具**, **操作**，然後按一下&#x200B;**Web控制台**。 在此控制台中，按一下&#x200B;**OSGi**，然後按一下&#x200B;**Configuration**。
1. 找到並按一下「**Day CQ WCM Language Manager**」，然後將「**Language List**」的值更改為`/apps/wcm/core/resources/languages`，然後按一下「**Save**」。

   ![chlimage_1-78](assets/chlimage_1-78.png)

## 在頁面屬性上設定MSM鎖（觸控式UI） {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

建立自訂頁面屬性時，您可能需要考慮新屬性是否有資格轉出至任何即時副本。

例如，如果新增兩個頁面屬性：

* 連絡人電子郵件:

   * 此屬性不需要推出，因為每個國家/地區（或品牌等）的屬性會不同。

* 關鍵視覺樣式：

   * 項目要求是，此屬性將按所有國家（地區或品牌等）通用的方式（通常）推出。

然後，您需要確保：

* 連絡人電子郵件:

   * 會從已推出的屬性中排除；請參閱[從同步中排除屬性和節點類型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization)。

* 關鍵視覺樣式：

   * 請確保除非取消繼承，否則不允許在觸控式UI中編輯此屬性，然後您還可以恢復繼承；可通過按一下切換以指示連接狀態的鏈/斷鏈連結來控制。

是否要轉出頁面屬性，因此，在編輯時要取消/重新啟用繼承，由對話方塊屬性控制：

* `cq-msm-lockable`

   * 適用於觸控式UI對話方塊中的項目
   * 將在對話框中建立鏈結符號
   * 僅允許在取消繼承時進行編輯（鏈結斷開）
   * 僅適用於資源的第一個子級
   * **類型**:  `String`

   * **值**:持有被代價物業之名稱(及與物業價值相若 `name`;例如，請參閱
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

當`cq-msm-lockable`已定義時，斷開/關閉鏈將以下方式與MSM交互：

* 如果值`cq-msm-lockable`為：

   * **相對** (例如 `myProperty` 或 `./myProperty`)

      * 它會從`cq:propertyInheritanceCancelled`中新增及移除屬性。
   * **絕對** (例如 `/image`)

      * 將`cq:LiveSyncCancelled` mixin添加到`./image`並將`cq:isCancelledForChildren`設定為`true`將取消繼承。

      * 關閉鏈將恢復繼承。


>[!NOTE]
>
>`cq-msm-lockable` 應用於要編輯的資源的第一個子級，而且它在任何更深層上級上都無法工作，無論該值定義為絕對值還是相對值。

>[!NOTE]
>
>當您重新啟用繼承時，即時副本頁面屬性不會自動與來源屬性同步。 如果需要，可以手動請求同步。
