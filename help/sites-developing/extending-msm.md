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
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 擴充多網站管理員{#extending-the-multi-site-manager}

本頁可協助您擴充多網站管理員的功能：

* 瞭解MSM Java API的主要成員。
* 建立可用於轉出設定的新同步動作。
* 移除「建立網站」精靈中的「章節」步驟。
* 修改預設語言和國家／地區代碼。

>[!NOTE]
>
>此頁面應與「重複使用內容」 [一起閱讀：多網站管理員](/help/sites-administering/msm.md)。

>[!CAUTION]
>
>「多網站管理員」及其API是在製作網站時使用的，因此僅適用於作者環境。

## Java API概觀 {#overview-of-the-java-api}

多站點管理由以下軟體包組成：

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主要MSM API物件的互動方式如下(另請參 [閱使用的詞](/help/sites-administering/msm.md#terms-used)):

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   A `Blueprint` (如 [Blueprint配置](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations))指定即時副本可繼承內容的頁面。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * 藍圖設定( `Blueprint`)是選擇性的，但：

      * 允許作者在來源上使 **用Rovolt** （明確）將修改推送至繼承自此來源的即時副本)。
      * 允許作者使用「 **Create Site**」;這可讓使用者輕鬆選擇語言並設定即時副本的結構。
      * 為任何產生的即時副本定義預設轉出設定。

* **`LiveRelationship`** 指 `LiveRelationship` 定即時副本分支中的資源與其等效源／藍圖資源之間的連接（關係）。

   * 在實現繼承和轉出時，會使用這些關係。
   * `LiveRelationship` 對象提供對轉出配置( `RolloutConfig`)的訪問 `LiveCopy`(參 `LiveStatus` 考)，以及與關係相關的對象。

   * 例如，即時副本是從source/blueprint `/content/copy/us` at.在中建立 `/content/we-retail/language-masters`。 資源 `/content/we.retail/language-masters/en/jcr:content` 與 `/content/copy/us/en/jcr:content` 關係。

* **`LiveCopy`** 保 `LiveCopy` 存即時拷貝資源與其源／藍圖資源之間關係( `LiveRelationship`)的配置詳細資訊。

   * 使用 `LiveCopy` 類別可存取頁面路徑、來源／藍圖頁面的路徑、轉出設定，以及子頁面是否也包含在中 `LiveCopy`。

   * 每次 `LiveCopy` 使用「建立網 **站」或「建** 立即時副本」時，都會建立節點 **** 。

* **`LiveStatus`**

   `LiveStatus` 對象提供對的運行時狀態的訪問 `LiveRelationship`。 用於查詢即時副本的同步狀態。

* **`LiveAction`**

   A `LiveAction` 是在轉出中涉及的每個資源上執行的動作。

   * LiveActions僅由RovoltConfigs產生。

* **`LiveActionFactory`**

   建立 `LiveAction` 給定配置的對 `LiveAction` 像。 配置作為資源儲存在儲存庫中。

* **`RolloutConfig`** 該 `RolloutConfig` 清單包含要 `LiveActions`在觸發時使用的清單。 繼 `LiveCopy` 承 `RolloutConfig` 並且結果在中出現 `LiveRelationship`。

   * 首次設定即時副本時，也會使用RovoltConfig（會觸發LiveActions）。

### 建立新的同步操作 {#creating-a-new-synchronization-action}

建立自訂同步動作，以便用於您的轉出設定。 當安裝的操作不符合您的 [特定應用程式要求時](/help/sites-administering/msm-sync.md#installed-synchronization-actions) ，建立同步操作。 若要這麼做，請建立兩個類別：

* 執行動作 [ 的介 `com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) 面實作。
* 實作介面並建立類 [ 別例 `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 項的OSGI元 `LiveAction` 件。

為 `LiveActionFactory` 給定配置創 `LiveAction` 建類的實例：

* `LiveAction` 類包括以下方法：

   * `getName`:傳回動作的名稱。名稱是用來參考動作的，例如在轉出設定中。
   * `execute`:執行動作的任務。

* `LiveActionFactory` 類包括以下成員：

   * `LIVE_ACTION_NAME`:包含關聯名稱的欄位 `LiveAction`。 此名稱必須與類方法返回 `getName` 的值相 `LiveAction` 符。

   * `createAction`:建立實例 `LiveAction`。 可選參 `Resource` 數可用於提供配置資訊。

   * `createsAction`:傳回關聯的名稱 `LiveAction`。

### 訪問LiveAction配置節點 {#accessing-the-liveaction-configuration-node}

使用存 `LiveAction` 儲庫中的配置節點來儲存影響實例運行時行為的 `LiveAction` 資訊。 儲存庫中儲存配置的節 `LiveAction` 點在運行時可供對 `LiveActionFactory` 像使用。 因此，您可以將屬性添加到配置節點，並根據需要在實施中 `LiveActionFactory` 使用這些屬性。

例如，需要 `LiveAction` 儲存Blueprint作者的名稱。 配置節點的屬性包括儲存資訊的藍圖頁的屬性名稱。 在運行時， `LiveAction` 從配置中檢索屬性名稱，然後獲取屬性值。

方法的參 ` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction` 數是對 `Resource` 像。 此物 `Resource` 件代表轉 `cq:LiveSyncAction` 出設定中此即時動作的節點；請參閱 [建立轉出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。 與常用配置節點一樣，您應將其調整為對 `ValueMap` 像：

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

以下對象作為對象方法 `execute` 的參 `LiveAction` 數：

* 表 [`Resource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) 示即時副本來源的對象。
* 代表 `Resource` 即時副本目標的物件。
* 即時 [ 副本 `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) 的物件。
* 值 `autoSave` 指示您是否 `LiveAction` 應保存對儲存庫所做的更改。

* 重設值指示轉出重設模式。

您可以從這些對象中獲取有關的所有資訊 `LiveCopy`。 您也可以使用 `Resource` 物件來取得 `ResourceResolver`、 `Session`和物 `Node` 件。 這些對象對於控制儲存庫內容非常有用：

在以下代碼的第一行中，原始碼是 `Resource` 原始碼頁的對象：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>引 `Resource` 數可以是不 `null` 適應於 `Resources` 對象（如對象）的 `Node` 對 [`NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html) 像。

### 建立新的轉出設定 {#creating-a-new-rollout-configuration}

當安裝的轉出設定不符合您的應用程式需求時，請建立轉出設定：

* [建立轉出設定](#create-the-rollout-configuration)。
* [將同步動作新增至轉出設定](#add-synchronization-actions-to-the-rollout-configuration)。

然後，當在藍圖或即時副本頁面上設定轉出設定時，您便可使用新的轉出設定。

>[!NOTE]
>
>另請參閱自 [訂推廣的最佳實務](/help/sites-administering/msm-best-practices.md#customizing-rollouts)。

#### 建立轉出設定 {#create-the-rollout-configuration}

1. 在傳統 **UI中開啟** 「工具控制台」;例如， [https://localhost:4502/miscadmin#/etc](https://localhost:4502/miscadmin#/etc)

   >[!NOTE]
   >
   >在標準的觸控式UI中，您可以使用「工具」、「操作」和「設定」欄目，導覽至 **傳統UI工具**&#x200B;主控台 ********。

1. 在資料夾樹中，選擇「工 **具**」、「 **MSM**」、「 **Rovolt Configurations** 」資料夾。
1. 按一 **下「新**」，然 **後按一下「新頁面** 」以定義「轉出設定」屬性：

   * **標題**:轉出設定的標題，例如我的轉出設定
   * **名稱**:儲存屬性值的節點的名稱，如myrolloutconfig
   * 選擇 **RolovatConfig模板**。

1. 按一下&#x200B;**「建立」**。
1. 連按兩下您建立的轉出設定，以開啟它以進一步設定。
1. 按一 **下編輯**。
1. 在「轉 **出設定** 」對話方塊中，選取「同步觸發器 **[](/help/sites-administering/msm-sync.md#rollout-triggers)**」以定義導致轉出的動作。
1. 按一下 **確定** ，保存更改。

#### 將同步操作添加到轉出配置 {#add-synchronization-actions-to-the-rollout-configuration}

轉出配置儲存在節點 `/etc/msm/rolloutconfigs` 下。 添加類型的子節 `cq:LiveSyncAction` 點以向轉出配置添加同步操作。 同步操作節點的順序決定操作的發生順序。

1. 開啟CRXDE Lite;例如 [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. 在轉出 `jcr:content` 配置節點下選擇節點。

   例如，對於具有 **Name** 屬性的轉出配 `myrolloutconfig`置，請選擇節點：

   `/etc/msm/rolloutconfigs/myrolloutconfig/jcr:content`

1. 按一 **下「建立** 」 **和「建立節點**」。 然後配置以下節點屬性並按一下「 **確定**」:

   * **名稱**:同步操作的節點名。 名稱必須與「同步操作」( **Synchronization Actions** )下表格中的「操作名稱」( [Action Name](/help/sites-administering/msm-sync.md#installed-synchronization-actions))相同 `contentCopy` ，例如 `workflow`或。

   * **類型**: `cq:LiveSyncAction`

1. 選擇剛建立的操作節點，並將以下屬性添加到節點：

   * **名稱**:動作的屬性名稱。 名稱必須與「同步操作」( **Synchronization Actions** )下表中的 [「屬性名稱」(Property Name](/help/sites-administering/msm-sync.md#installed-synchronization-actions))相同 `enabled`。

   * **類型**:字串

   * **值**:動作的屬性值。 有關有效值，請參 **閱Synchronization Actions中的** Properties列 [，例如](/help/sites-administering/msm-sync.md#installed-synchronization-actions)`true`。

1. 根據需要添加和配置任意數量的同步操作節點。 重新排列動作節點，使其順序符合您希望動作節點發生的順序。 最頂端的操作節點首先出現。
1. 按一下「 **全部儲存**」。

### 建立和使用簡單的LiveActionFactory類別 {#creating-and-using-a-simple-liveactionfactory-class}

請依照本節中的程式來開發並 `LiveActionFactory` 在轉出配置中使用它。 這些程式使用Maven和Eclipse來開發和部署 `LiveActionFactory`:

1. [建立主要專案](#create-the-maven-project) ，並將它匯入Eclipse。
1. [向POM檔案](#add-dependencies-to-the-pom-file) 添加相關性。
1. [實作介 `LiveActionFactory` 面](#implement-liveactionfactory) ，並部署OSGi套件。
1. [建立轉出設定](#create-the-example-rollout-configuration)。
1. [建立即時副本](#create-the-live-copy)。

Maven項目和Java類的原始碼可在公共Git儲存庫中使用。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟ExperienceManager-java-msmloult專案](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

#### 建立Maven專案 {#create-the-maven-project}

下列程式要求您將adobe-public設定檔新增至Maven設定檔。

* 如需adobe-public設定檔的詳細資訊，請參 [閱「取得Content Package Maven Plugin」](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* 如需Maven設定檔的詳細資訊，請參閱Maven設 [定參考](https://maven.apache.org/settings.html)。

1. 開啟終端或命令行會話並更改目錄以指向建立項目的位置。
1. 輸入以下命令：

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在互動式提示時指定下列值：

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`: `MyLiveActionFactory`
   * `version`: `1.0-SNAPSHOT`
   * `package`: `MyPackage`
   * `appsFolderName`: `myapp`
   * `artifactName`: `MyLiveActionFactory package`
   * `packageGroup`: `myPackages`

1. 啟動Eclipse並 [匯入Maven專案](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse)。

#### 向POM檔案添加相關性 {#add-dependencies-to-the-pom-file}

新增相依性，讓Eclipse編譯器可以參考程式碼中使用的 `LiveActionFactory` 類別。

1. 從Eclipse專案總管開啟檔案：

   `MyLiveActionFactory/pom.xml`

1. 在編輯器中，按一下該選 `pom.xml` 項卡並找到該 `project/dependencyManagement/dependencies` 部分。
1. 在元素中新增下列XML `dependencyManagement` ，然後儲存檔案。

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

1. 從 **Project Explorer中開啟包的POM檔案** ，位 `MyLiveActionFactory-bundle/pom.xml`置。
1. 在編輯器中，按一下該選 `pom.xml` 項卡並找到項目／依賴項部分。 在相依性元素中新增下列XML，然後儲存檔案：

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

#### 實作LiveActionFactory {#implement-liveactionfactory}

以下類 `LiveActionFactory` 別實現一個 `LiveAction` 類，它記錄有關源和目標頁的消息，並將屬性從源節點 `cq:lastModifiedBy` 複製到目標節點。 即時動作的名稱為 `exampleLiveAction`。

1. 在Eclipse專案總管中，以滑鼠右鍵按一下套件， `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` 然後按一下「新 **增** >類別 ****」。 在「名 **稱**」中輸入， `ExampleLiveActionFactory` 然後按一下 **完成**。
1. 開啟檔 `ExampleLiveActionFactory.java` 案，以下列程式碼取代內容，並儲存檔案。

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
        lastMod = sourcevm.get(com.day.cq.wcm.api.NameConstants.PN_PAGE_LAST_MOD_BY, String.class);
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

1. 使用終端或命令會話，將目錄更改為 `MyLiveActionFactory` 目錄（Maven項目目錄）。 然後，輸入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   AEM檔 `error.log` 案應指示已啟動套件。

   例如， [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs)。

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

#### 建立範例轉出設定 {#create-the-example-rollout-configuration}

建立使用您所建立之MSM轉出 `LiveActionFactory` 組態：

1. 使用標準過程 [建立並配置Rolovat Configuration](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) —— 並使用屬性：

   1. 建立:

      1. **標題**:範例轉出設定
      1. **名稱**:examplerolloutconfig
      1. 使用 **RovoltConfig範本**。
   1. 編輯:

      1. **同步觸發器**:啟動時


#### 將即時動作新增至範例轉出設定 {#add-the-live-action-to-the-example-rollout-configuration}

設定您在上一個程式中建立的轉出設定，以便使用 `ExampleLiveActionFactory` 類別。

1. 開啟CRXDE Lite;例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)。
1. 在下面建立以下節點 `/etc/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **名稱**: `exampleLiveAction`
   * **類型**: `cq:LiveSyncAction`
   ![chlimage_1-75](assets/chlimage_1-75.png)

1. 按一下「 **全部儲存**」。
1. 選擇節 `exampleLiveAction` 點並添加以下屬性：

   * **名稱**: `repLastModBy`
   * **類型**: `Boolean`
   * **值**: `true`
   此屬性向類指 `ExampleLiveAction` 示應將屬 `cq:LastModifiedBy` 性從源複製到目標節點。

1. 按一下「 **全部儲存**」。

#### 建立即時副本 {#create-the-live-copy}

[使用您的轉出設定](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) ，建立We.Retail參考網站英文／產品分支的即時副本：

* **來源**: `/content/we-retail/language-masters/en/products`

* **轉出設定**:範例轉出設定

激活源 **分支的** 「產品」（英文）頁，並觀察類生成的日 `LiveAction` 志消息：

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

### 移除「建立網站精靈」中的章節步驟 {#removing-the-chapters-step-in-the-create-site-wizard}

在某些情況下，「 **章節** 」選擇在建立網站精靈中不是必需的(只 **需選擇「語言** 」)。 若要移除預設We.Retail英文藍圖中的此步驟：

1. 在CRX瀏覽器中，刪除節點：
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. 導航到 `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` 並建立新節點：

   1. **名稱** = `chapters`; **類型** = `cq:Widget`。

1. 向新節點添加以下屬性：

   1. **名稱** = `name`; **類型** = `String`; **值** = `msm:chapterPages`

   1. **名稱** = `value`; **類型** = `String`; **值** = `all`

   1. **名稱** = `xtype`; **類型** = `String`; **值** = `hidden`

### 變更語言名稱和預設國家 {#changing-language-names-and-default-countries}

AEM使用預設的語言和國家代碼集。

* 預設語言代碼是由ISO-639-1定義的小寫雙字母代碼。
* 預設的國家／地區代碼為小寫或大寫，由ISO 3166定義的雙字母代碼。

MSM會使用儲存的語言和國家代碼清單來判斷與您頁面的語言版本名稱相關聯的國家／地區名稱。 如有需要，您可以變更清單的下列方面：

* 語言標題
* 國家／地區名稱
* 語言的預設國家(如 `en`、 `de`等等)

語言清單儲存在節點下 `/libs/wcm/core/resources/languages` 方。 每個子節點代表語言或語言國家：

* 節點的名稱是語言代碼( `en` 如 `de`或)或language_country代碼(如 `en_us` 或 `de_ch`)。

* 節 `language` 點的屬性儲存代碼語言的完整名稱。
* 節 `country` 點的屬性會儲存代碼的國家的完整名稱。
* 當節點名稱只包含語言代碼(如 `en`)時，國家屬性為 `*`，而另一 `defaultCountry` 個屬性儲存語言國家的代碼，以指出要使用的國家。

![chlimage_1-76](assets/chlimage_1-76.png)

要修改語言：

1. 在網頁瀏覽器中開啟CRXDE Lite;例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. 選擇該文 `/apps` 件夾，然後 **按一下**「建立 **」。**

   命名新資料夾 `wcm`。

1. 重複上一步以建立檔案 `/apps/wcm/core` 夾樹。 建立名為的 `sling:Folder` 類 `core` 型節點 `resources`。

   ![chlimage_1-77](assets/chlimage_1-77.png)

1. 按一下右鍵該節 `/libs/wcm/core/resources/languages` 點，然後按一下 **複製**。
1. 按一下右鍵該文 `/apps/wcm/core/resources` 件夾並單 **擊貼上**。 根據需要修改子節點。
1. 按一下「 **全部儲存**」。
1. 按一 **下「工具**」、「 **作業** 」 **和「Web Console**」。 在此控制台中，單 **擊OSGi**，然 **後按一下Configuration**。
1. 找到並單 **擊Day CQ WCM Language Manager**，將「Language List **（語言清單）」的值更改為** ，然後按一下「 `/apps/wcm/core/resources/languages`Save（保存） ****」。

   ![chlimage_1-78](assets/chlimage_1-78.png)

### 在頁面屬性上設定MSM鎖（啟用觸控的UI） {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

建立自訂頁面屬性時，您可能需要考慮新屬性是否符合推廣至任何即時副本的資格。

例如，如果新增兩個新頁面屬性：

* 連絡人電子郵件:

   * 此屬性不需要推出，因為每個國家（或品牌等）都不同。

* 關鍵視覺樣式：

   * 項目要求是，此屬性應以（通常）所有國家（或品牌等）共同的方式推出。

然後，您需要確保：

* 連絡人電子郵件:

   * 被排除在外部屬性之外；請參 [閱從同步中排除屬性和節點類型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization)。

* 關鍵視覺樣式：

   * 請確定您不允許在觸控式使用者介面中編輯此屬性，除非繼承已取消，您也可以重新建立繼承；通過按一下切換以指示連接狀態的鏈／斷鏈連結來控制此操作。

頁面屬性是否要開始，因此，在編輯時要取消／恢復繼承，由對話框屬性控制：

* `cq-msm-lockable`

   * 適用於啟用觸控的UI對話方塊中的項目
   * 將在對話框中建立連結符號
   * 僅當繼承取消（連結斷開）時才允許編輯
   * 僅適用於資源的第一個子級
   * **類型**: `String`

   * **值**:持有被代價物業之名稱(及與物業價值相若 `name`;例如，請參閱
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

當定 `cq-msm-lockable` 義後，斷開／關閉鏈將通過以下方式與MSM相互作用：

* 如果值 `cq-msm-lockable` 為：

   * **相對** (例如 `myProperty` 或 `./myProperty`)

      * 它將從中添加和刪除屬 `cq:propertyInheritanceCancelled`性。
   * **絕對** (例如 `/image`)

      * 斷開鏈將通過將混合添加到和設 `cq:LiveSyncCancelled` 置為來取 `./image` 消繼 `cq:isCancelledForChildren` 承 `true`。

      * 關閉鏈將恢復繼承。


>[!NOTE]
>
>`cq-msm-lockable` 應用於要編輯的資源的第一個子級別，而且無論該值定義為絕對或相對值，它在任何更深層級別上都不起作用。

>[!NOTE]
>
>當您重新啟用繼承時，即時副本頁面屬性不會自動與source屬性同步。 如果需要，可以手動請求同步。
