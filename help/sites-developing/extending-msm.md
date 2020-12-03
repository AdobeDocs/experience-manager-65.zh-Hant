---
title: 擴充多網站管理員
seo-title: 擴充多網站管理員
description: 本頁可協助您擴充多網站管理員的功能
seo-description: 本頁可協助您擴充多網站管理員的功能
uuid: dfa7d050-29fc-4401-8d4d-d6ace6b49bea
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6128c91a-4173-42b4-926f-bbbb2b54ba5b
docset: aem65
translation-type: tm+mt
source-git-commit: 3a1d02fc1bc561b54e57cf91abc8f4406ba8c365
workflow-type: tm+mt
source-wordcount: '2601'
ht-degree: 0%

---


# 擴展多站點管理器{#extending-the-multi-site-manager}

本頁可協助您擴充多網站管理員的功能：

* 瞭解MSM Java API的主要成員。
* 建立可用於轉出設定的新同步動作。
* 修改預設語言和國家／地區代碼。

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>此頁應與[重複使用內容一起讀取：多站點管理器](/help/sites-administering/msm.md)。
>
>AEM 6.4中的「Sites Repository Restructing」（網站資料庫重組）的下列章節可能也會受到關注：
>* [多站點管理器Blueprint配置](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-blueprint-configurations)
>* [多站點管理器推廣配置](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-rollout-configurations)


>[!CAUTION]
>
>「多網站管理員」及其API是在製作網站時使用的，因此僅適用於作者環境。

## Java API {#overview-of-the-java-api}概觀

多站點管理由以下軟體包組成：

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主要MSM API物件的互動方式如下（另請參閱[使用的詞語](/help/sites-administering/msm.md#terms-used)）:

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   `Blueprint`（如[blueprint configuration](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)中）指定即時副本可繼承內容的頁面。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * 藍圖配置(`Blueprint`)的使用是可選的，但：

      * 允許作者在源上使用&#x200B;**Rovolt**&#x200B;選項(將修改（顯式）推送到繼承自此源的即時拷貝)。
      * 允許作者使用&#x200B;**Create Site**;這可讓使用者輕鬆選擇語言並設定即時副本的結構。
      * 為任何產生的即時副本定義預設轉出設定。

* **`LiveRelationship`** 指 `LiveRelationship` 定即時副本分支中的資源與其等效源／藍圖資源之間的連接（關係）。

   * 在實現繼承和轉出時，會使用這些關係。
   * `LiveRelationship` 對象提供對轉出配置()的訪問( `RolloutConfig`引用), `LiveCopy`以及與 `LiveStatus` 關係相關的對象。

   * 例如，在`/content/copy/us`中，從`/content/we-retail/language-masters`的來源／藍圖建立即時副本。 資源`/content/we.retail/language-masters/en/jcr:content`和`/content/copy/us/en/jcr:content`形成關係。

* **`LiveCopy`** `LiveCopy` 保存即時副本資源與其源/ `LiveRelationship`Blueprint資源之間關係()的配置詳細資訊。

   * 使用`LiveCopy`類訪問頁面路徑、源／藍圖頁面的路徑、轉出配置以及子頁面是否也包含在`LiveCopy`中。

   * 每次使用「建立站點」(Create Site)「**」(Create Site)「**」(Create Live Copy)「建立即時副本」(A4/)時，都建立`LiveCopy`節點。****

* **`LiveStatus`**

   `LiveStatus` 對象提供對的運行時狀態的訪問 `LiveRelationship`。用於查詢即時副本的同步狀態。

* **`LiveAction`**

   `LiveAction`是在轉出中涉及的每個資源上執行的動作。

   * LiveActions僅由RovoltConfigs產生。

* **`LiveActionFactory`**

   建立給定`LiveAction`配置的`LiveAction`對象。 配置作為資源儲存在儲存庫中。

* **`RolloutConfig`** 此 `RolloutConfig` 清單包含一 `LiveActions`個清單，在觸發時使用。`LiveCopy`繼承`RolloutConfig`，結果出現在`LiveRelationship`中。

   * 首次設定即時副本時，也會使用RovoltConfig（會觸發LiveActions）。

## 建立新同步操作{#creating-a-new-synchronization-action}

建立自訂同步動作，以便用於轉出設定。 當安裝的[操作](/help/sites-administering/msm-sync.md#installed-synchronization-actions)不符合您的特定應用程式要求時，建立同步操作。 若要這麼做，請建立兩個類別：

* 執行動作的[ `com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html)介面的實作。
* OSGI元件實現[ `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html)介面並建立`LiveAction`類的實例。

`LiveActionFactory`會為給定配置建立`LiveAction`類的實例：

* `LiveAction` 類包括以下方法：

   * `getName`:傳回動作的名稱。名稱是用來參考動作的，例如在轉出設定中。
   * `execute`:執行動作的任務。

* `LiveActionFactory` 類包括以下成員：

   * `LIVE_ACTION_NAME`:包含關聯名稱的欄位 `LiveAction`。此名稱必須與`LiveAction`類別的`getName`方法返回的值一致。

   * `createAction`:建立實例 `LiveAction`。可選`Resource`參數可用於提供配置資訊。

   * `createsAction`:傳回關聯的名稱 `LiveAction`。

### 訪問LiveAction Configuration Node {#accessing-the-liveaction-configuration-node}

使用儲存庫中的`LiveAction`配置節點來儲存影響`LiveAction`實例的運行時行為的資訊。 儲存`LiveAction`配置的儲存庫中的節點在運行時可用於`LiveActionFactory`對象。 因此，您可以將屬性添加到配置節點中，並根據需要在`LiveActionFactory`實施中使用這些屬性。

例如，`LiveAction`需要儲存Blueprint作者的名稱。 配置節點的屬性包括儲存資訊的藍圖頁的屬性名稱。 在運行時，`LiveAction`從配置中檢索屬性名稱，然後獲取屬性值。

` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction`方法的參數是`Resource`對象。 此`Resource`物件代表轉出設定中此即時動作的`cq:LiveSyncAction`節點；請參閱[建立轉出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。 使用配置節點時，應將其調整為`ValueMap`對象：

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

以下對象是`LiveAction`對象的`execute`方法的參數：

* [ `Resource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html)物件，代表即時副本的來源。
* `Resource`物件，代表即時副本的目標。
* 即時副本的[ `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html)物件。
* `autoSave`值指示您的`LiveAction`是否應保存對儲存庫所做的更改。

* 重設值指示轉出重設模式。

您可以從這些對象中獲取有關`LiveCopy`的所有資訊。 您也可以使用`Resource`物件來取得`ResourceResolver`、`Session`和`Node`物件。 這些對象對於控制儲存庫內容非常有用：

在以下代碼的第一行中，原始碼是原始碼頁的`Resource`對象：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>`Resource`引數可以是`null`或`Resources`物件，這些物件不適應`Node`物件，例如[ `NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html)物件。

## 建立新的轉出設定{#creating-a-new-rollout-configuration}

當安裝的轉出設定不符合您的應用程式需求時，請建立轉出設定：

* [建立轉出設定](#create-the-rollout-configuration)。
* [將同步動作新增至轉出設定](#add-synchronization-actions-to-the-rollout-configuration)。

然後，當在藍圖或即時副本頁面上設定轉出設定時，您便可使用新的轉出設定。

>[!NOTE]
>
>另請參閱自訂推廣的[最佳實務](/help/sites-administering/msm-best-practices.md#customizing-rollouts)。

### 建立轉出設定{#create-the-rollout-configuration}

若要建立新的轉出設定：

1. 開啟CRXDE Lite;例如：
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 導航到 :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >這是您專案的自訂版本：
   >`/libs/msm/wcm/rolloutconfigs`
   >如果這是您的第一個配置，則必須建立。

   >[!NOTE]
   >
   >您不得更改/libs路徑中的任何內容。
   >這是因為下次升級實例時會覆寫/libs的內容（套用修補程式或功能套件時很可能會覆寫）。
   >配置和其他更改的建議方法為：
   >* 在/apps下重新建立必要項目（亦即，在/libs中存在）
   >* 在/apps中進行任何變更


1. 在此&#x200B;**Create**&#x200B;下，建立具有以下屬性的節點：

   * **名稱**:轉出配置的節點名稱。md#installed-synchronization-actions)，例如`contentCopy`或`workflow`。
   * **類型**:  `cq:RolloutConfig`

1. 將以下屬性添加到此節點：
   * **名稱**:  `jcr:title`

      **類型**:  `String`
      **值**:UI中將會顯示的識別標題。
   * **名稱**:  `jcr:description`

      **類型**:  `String`
      **值**:可選說明。
   * **名稱**:  `cq:trigger`

      **類型**:  `String`
      **值**:要使用 [的](/help/sites-administering/msm-sync.md#rollout-triggers) 轉出觸發器。從中選擇：
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 按一下&#x200B;**保存全部**。

### 將同步操作添加到轉出配置{#add-synchronization-actions-to-the-rollout-configuration}

轉出配置儲存在您在`/apps/msm/<your-project>/rolloutconfigs`節點下建立的[轉出配置節點](#create-the-rollout-configuration)下。

添加類型`cq:LiveSyncAction`的子節點，以將同步操作添加到轉出配置中。 同步操作節點的順序決定操作的發生順序。

1. 仍然在CRXDE Lite中，選擇[Rovolt Configuration](#create-the-rollout-configuration)節點。

   例如：
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **建立** 具有以下節點屬性的節點：

   * **名稱**:同步操作的節點名。名稱必須與[同步操作](/help/sites-administering/msm-sync.md#installed-synchronization-actions)下表中的&#x200B;**操作名稱**&#x200B;相同，例如`contentCopy`或`workflow`。
   * **類型**:  `cq:LiveSyncAction`

1. 根據需要添加和配置任意數量的同步操作節點。 重新排列動作節點，使其順序符合您希望動作節點發生的順序。 最頂端的操作節點首先出現。

## 建立和使用Simple LiveActionFactory類{#creating-and-using-a-simple-liveactionfactory-class}

請依照本節中的程式來開發`LiveActionFactory`，並將它用於轉出設定。 這些程式使用Maven和Eclipse來開發和部署`LiveActionFactory`:

1. [建立主要](#create-the-maven-project) 專案並匯入至Eclipse。
1. [將相](#add-dependencies-to-the-pom-file) 關內容添加到POM檔案。
1. [實作 `LiveActionFactory` ](#implement-liveactionfactory) 介面並部署OSGi套件。
1. [建立轉出設定](#create-the-example-rollout-configuration)。
1. [建立即時副本](#create-the-live-copy)。

Maven項目和Java類的原始碼可在公共Git儲存庫中使用。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟ExperienceManager-java-msmloult專案](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* 將專案下載為[a ZIP file](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### 建立Maven項目{#create-the-maven-project}

下列程式要求您將adobe-public設定檔新增至Maven設定檔。

* 如需adobe-public設定檔的詳細資訊，請參閱[取得Content Package Maven Plugin](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* 有關Maven設定檔案的資訊，請參閱Maven [設定參考](https://maven.apache.org/settings.html)。

1. 開啟終端或命令行會話並更改目錄以指向建立項目的位置。
1. 輸入以下命令：

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在互動式提示時指定下列值：

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`:  `MyLiveActionFactory`
   * `version`:  `1.0-SNAPSHOT`
   * `package`:  `MyPackage`
   * `appsFolderName`:  `myapp`
   * `artifactName`:  `MyLiveActionFactory package`
   * `packageGroup`:  `myPackages`

1. 啟動Eclipse並[匯入Maven專案](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse)。

### 向POM檔案{#add-dependencies-to-the-pom-file}添加相關性

新增相依性，讓Eclipse編譯器可以參考`LiveActionFactory`程式碼中使用的類別。

1. 從Eclipse專案總管開啟檔案：

   `MyLiveActionFactory/pom.xml`

1. 在編輯器中，按一下`pom.xml`頁籤並找到`project/dependencyManagement/dependencies`部分。
1. 在`dependencyManagement`元素中新增下列XML，然後儲存檔案。

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

1. 從&#x200B;**Project Explorer**&#x200B;的`MyLiveActionFactory-bundle/pom.xml`開啟包的POM檔案。
1. 在編輯器中，按一下`pom.xml`頁籤並找到項目／依賴項部分。 在相依性元素中新增下列XML，然後儲存檔案：

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

以下`LiveActionFactory`類實現了`LiveAction` ，該類記錄有關源和目標頁的消息，並將`cq:lastModifiedBy`屬性從源節點複製到目標節點。 即時動作的名稱為`exampleLiveAction`。

1. 在Eclipse項目瀏覽器中，按一下右鍵`MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm`包，然後按一下&#x200B;**新建** > **類**。 對於&#x200B;**名稱**，輸入`ExampleLiveActionFactory`，然後按一下&#x200B;**完成**。
1. 開啟`ExampleLiveActionFactory.java`檔案，以下列程式碼取代內容，並儲存檔案。

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

   AEM `error.log`檔案應指示已啟動套件。

   例如，[https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs)。

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### 建立範例轉出設定{#create-the-example-rollout-configuration}

建立使用您建立之`LiveActionFactory`的MSM轉出設定：

1. 使用標準過程](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)建立並配置[轉出配置——並使用屬性：

   * **標題**:範例轉出設定
   * **名稱**:examplerolloutconfig
   * **cq:trigger**:  `publish`

### 將即時動作新增至範例轉出設定{#add-the-live-action-to-the-example-rollout-configuration}

配置您在上一個過程中建立的轉出配置，使其使用`ExampleLiveActionFactory`類。

1. 開啟CRXDE Lite;例如，[https://localhost:4502/crx/de](https://localhost:4502/crx/de)。
1. 在`/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`下建立以下節點：

   * **名稱**:  `exampleLiveAction`
   * **類型**:  `cq:LiveSyncAction`

1. 按一下&#x200B;**保存全部**。
1. 選擇`exampleLiveAction`節點並添加以下屬性：

   * **名稱**:  `repLastModBy`
   * **類型**:  `Boolean`
   * **值**:  `true`

   此屬性向`ExampleLiveAction`類指示`cq:LastModifiedBy`屬性應從源節點複製到目標節點。

1. 按一下&#x200B;**保存全部**。

### 建立即時副本{#create-the-live-copy}

[使用您的](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 轉出設定，建立We.Retail參考網站英文／產品分支的即時版本：

* **來源**:  `/content/we-retail/language-masters/en/products`

* **轉出設定**:範例轉出設定

激活源分支的&#x200B;**產品**（英文）頁，並觀察`LiveAction`類生成的日誌消息：

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

## 變更語言名稱和預設國家／地區{#changing-language-names-and-default-countries}

AEM使用預設的語言和國家代碼集。

* 預設語言代碼是由ISO-639-1定義的小寫雙字母代碼。
* 預設的國家／地區代碼為小寫或大寫，由ISO 3166定義的雙字母代碼。

MSM會使用儲存的語言和國家代碼清單來判斷與您頁面的語言版本名稱相關聯的國家／地區名稱。 如有需要，您可以變更清單的下列方面：

* 語言標題
* 國家／地區名稱
* 語言的預設國家（例如`en`、`de`等程式碼）

語言清單儲存在`/libs/wcm/core/resources/languages`節點下。 每個子節點代表語言或語言國家：

* 節點的名稱是語言代碼（如`en`或`de`），或language_country代碼（如`en_us`或`de_ch`）。

* 節點的`language`屬性儲存代碼語言的完整名稱。
* 節點的`country`屬性儲存代碼的國家的完整名稱。
* 當節點名稱只包含語言代碼（如`en`）時，國家屬性為`*`，而另外的`defaultCountry`屬性則儲存語言國家的代碼，以指出要使用的國家。

![chlimage_1-76](assets/chlimage_1-76.png)

要修改語言：

1. 在網頁瀏覽器中開啟CRXDE Lite;例如[https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. 選擇`/apps`資料夾，然後按一下&#x200B;**建立**，然後按一下&#x200B;**建立資料夾。**

   為新資料夾命名`wcm`。

1. 重複上一步以建立`/apps/wcm/core`資料夾樹。 在`core`中建立名為`resources`的`sling:Folder`類型的節點。<!-- ![chlimage_1-77](assets/chlimage_1-77.png) -->

1. 按一下右鍵`/libs/wcm/core/resources/languages`節點，然後按一下&#x200B;**Copy**。
1. 按一下右鍵`/apps/wcm/core/resources`資料夾，然後按一下&#x200B;**貼上**。 根據需要修改子節點。
1. 按一下&#x200B;**保存全部**。
1. 按一下&#x200B;**工具**、**操作**，然後按一下&#x200B;**Web控制台**。 在此控制台中，按一下&#x200B;**OSGi** ，然後按一下&#x200B;**Configuration**。
1. 找到並按一下&#x200B;**Day CQ WCM Language Manager** ，將&#x200B;**Language List**&#x200B;的值更改為`/apps/wcm/core/resources/languages` ，然後按一下&#x200B;**Save**。

   ![chlimage_1-78](assets/chlimage_1-78.png)

## 在頁面屬性上配置MSM鎖（啟用觸控的UI）{#configuring-msm-locks-on-page-properties-touch-enabled-ui}

建立自訂頁面屬性時，您可能需要考慮新屬性是否符合推廣至任何即時副本的資格。

例如，如果新增兩個新頁面屬性：

* 連絡人電子郵件:

   * 此屬性不需要推出，因為每個國家（或品牌等）都不同。

* 關鍵視覺樣式：

   * 項目要求是，此屬性應以（通常）所有國家（或品牌等）共同的方式推出。

然後，您需要確保：

* 連絡人電子郵件:

   * 被排除在外部屬性之外；請參見[從同步中排除屬性和節點類型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization)。

* 關鍵視覺樣式：

   * 請確定您不允許在觸控式使用者介面中編輯此屬性，除非繼承已取消，您也可以重新建立繼承；通過按一下切換以指示連接狀態的鏈／斷鏈連結來控制此操作。

頁面屬性是否要開始，因此，在編輯時要取消／恢復繼承，由對話框屬性控制：

* `cq-msm-lockable`

   * 適用於啟用觸控的UI對話方塊中的項目
   * 將在對話框中建立連結符號
   * 僅當繼承取消（連結斷開）時才允許編輯
   * 僅適用於資源的第一個子級
   * **類型**:  `String`

   * **值**:持有被代價物業之名稱(及與物業價值相若 `name`;例如，請參閱
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

當`cq-msm-lockable`已定義時，斷開／關閉鏈將通過以下方式與MSM相互作用：

* 如果`cq-msm-lockable`的值為：

   * **相對** (例如 `myProperty` 或 `./myProperty`)

      * 它將從`cq:propertyInheritanceCancelled`中添加和刪除屬性。
   * **絕對** (例如 `/image`)

      * 斷開鏈將通過將`cq:LiveSyncCancelled`混頻添加到`./image`並將`cq:isCancelledForChildren`設定為`true`來取消繼承。

      * 關閉鏈將恢復繼承。


>[!NOTE]
>
>`cq-msm-lockable` 應用於要編輯的資源的第一個子級別，而且無論該值定義為絕對或相對值，它在任何更深層級別上都不起作用。

>[!NOTE]
>
>當您重新啟用繼承時，即時副本頁面屬性不會自動與source屬性同步。 如果需要，可以手動請求同步。
