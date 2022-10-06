---
title: 擴展多站點管理器
seo-title: Extending the Multi Site Manager
description: 本頁面可協助您擴充多網站管理員的功能
seo-description: This page helps you extend the functionalities of the Multi Site Manager
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
source-wordcount: '2584'
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
>本頁面應與 [重複使用內容：多網站管理員](/help/sites-administering/msm.md).
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

主要MSM API物件互動如下(另請參閱 [使用的詞語](/help/sites-administering/msm.md#terms-used)):

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   A `Blueprint` (如 [Blueprint設定](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations))會指定Live Copy可繼承內容的頁面。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * Blueprint設定的使用( `Blueprint`)為選用，但：

      * 允許作者使用 **轉出** 來源上的選項(將修改推送至繼承自此來源的即時副本（明確）)。
      * 允許作者使用 **建立網站**;這可讓使用者輕鬆選取語言並設定即時副本的結構。
      * 定義任何產生的Live Copy的預設轉出設定。

* **`LiveRelationship`**

   此 `LiveRelationship` 指定即時副本分支中的資源與其等效源/藍圖資源之間的連接（關係）。

   * 在實現繼承和轉出時會使用關係。
   * `LiveRelationship` 物件提供轉出設定的存取（參考）( `RolloutConfig`), `LiveCopy`，和 `LiveStatus` 與關係相關的對象。

   * 例如，即時副本是在 `/content/copy/us` 從源/blueprint到 `/content/we-retail/language-masters`. 資源 `/content/we.retail/language-masters/en/jcr:content` 和 `/content/copy/us/en/jcr:content` 形成關係。

* **`LiveCopy`**

   `LiveCopy` 保留關係的配置詳細資訊( `LiveRelationship`)，介於即時副本資源及其來源/blueprint資源之間。

   * 使用 `LiveCopy` 類別，以存取頁面路徑、來源/blueprint頁面的路徑、轉出設定，以及子頁面是否也包含在 `LiveCopy`.

   * A `LiveCopy` 每次建立節點時 **建立網站** 或 **建立即時副本** 中所有規則的URL區段。

* **`LiveStatus`**

   `LiveStatus` 對象提供對運行時狀態的訪問 `LiveRelationship`. 用於查詢即時副本的同步狀態。

* **`LiveAction`**

   A `LiveAction` 是在轉出中涉及的每個資源上執行的動作。

   * LiveActions僅由RolloutConfigs產生。

* **`LiveActionFactory`**

   建立 `LiveAction` 給定的對象 `LiveAction` 設定。 設定會儲存為存放庫中的資源。

* **`RolloutConfig`**

   此 `RolloutConfig` 包含 `LiveActions`，以在觸發時使用。 此 `LiveCopy` 會繼承 `RolloutConfig` 結果會顯示在 `LiveRelationship`.

   * 第一次設定即時副本時，也會使用RolloutConfig（這會觸發LiveActions）。

## 建立新的同步操作 {#creating-a-new-synchronization-action}

建立要與轉出設定搭配使用的自訂同步動作。 在 [已安裝動作](/help/sites-administering/msm-sync.md#installed-synchronization-actions) 不符合您的特定應用程式要求。 要執行此操作，請建立兩個類：

* 實作 [ `com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) 執行動作的介面。
* 實作的OSGI元件 [ `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 介面和建立例項 `LiveAction` 類別。

此 `LiveActionFactory` 建立例項 `LiveAction` 類別：

* `LiveAction` 類包括以下方法：

   * `getName`:傳回動作的名稱。名稱是用來參照動作，例如轉出設定。
   * `execute`:執行動作的工作。

* `LiveActionFactory` 類包括以下成員：

   * `LIVE_ACTION_NAME`:包含關聯之 `LiveAction`. 此名稱必須與 `getName` 方法 `LiveAction` 類別。

   * `createAction`:建立例項 `LiveAction`. 選填 `Resource` 參數可用來提供設定資訊。

   * `createsAction`:傳回關聯 `LiveAction`.

### 存取LiveAction設定節點 {#accessing-the-liveaction-configuration-node}

使用 `LiveAction` 配置儲存庫中的節點，以儲存影響 `LiveAction` 例項。 儲存庫中儲存 `LiveAction` 設定可供使用 `LiveActionFactory` 物件。 因此，您可以將屬性新增至設定節點，並在 `LiveActionFactory` 視需要實作。

例如， `LiveAction` 需要儲存blueprint作者的名稱。 配置節點的屬性包括儲存資訊的Blueprint頁的屬性名稱。 在執行階段中， `LiveAction` 從設定中擷取屬性名稱，然後取得屬性值。

的參數 ` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction` 方法是 `Resource` 物件。 此 `Resource` 物件代表 `cq:LiveSyncAction` 的節點。請參閱 [建立轉出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration). 如同使用設定節點時，您應將其調整至 `ValueMap` 物件：

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

以下物件是以 `execute` 方法 `LiveAction` 物件：

* A [ `Resource`](https://helpx.adobe.com/tw/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) 代表即時副本來源的物件。
* A `Resource` 代表即時副本目標的物件。
* 此 [ `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) 即時副本的物件。
* 此 `autoSave` 值表示您 `LiveAction` 應儲存對存放庫所做的變更。

* 重設值表示轉出重設模式。

您可以從這些物件取得 `LiveCopy`. 您也可以使用 `Resource` 獲取對象 `ResourceResolver`, `Session`，和 `Node` 對象。 這些對象對於控制儲存庫內容非常有用：

在下列程式碼的第一行中，原始碼為 `Resource` 源頁的對象：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>此 `Resource` 引數可能 `null` 或 `Resources` 不適應的對象 `Node` 對象，如 [ `NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html) 對象。

## 建立新轉出設定 {#creating-a-new-rollout-configuration}

當安裝的轉出設定不符合您的應用程式需求時，建立轉出設定：

* [建立轉出設定](#create-the-rollout-configuration).
* [將同步化動作新增至轉出設定](#add-synchronization-actions-to-the-rollout-configuration).

接著，當您在Blueprint或Live Copy頁面上設定轉出設定時，即可使用新的轉出設定。

>[!NOTE]
>
>另請參閱 [自訂轉出的最佳作法](/help/sites-administering/msm-best-practices.md#customizing-rollouts).

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


1. 在此 **建立** 具有以下屬性的節點：

   * **名稱**:轉出設定的節點名稱。 md#installed-synchronization-actions)，例如 `contentCopy` 或 `workflow`.
   * **類型**: `cq:RolloutConfig`

1. 將下列屬性新增至此節點：
   * **名稱**: `jcr:title`

      **類型**: `String`
      **值**:將出現在UI中的識別標題。
   * **名稱**: `jcr:description`

      **類型**: `String`
      **值**:選擇性說明。
   * **名稱**: `cq:trigger`

      **類型**: `String`
      **值**:此 [轉出觸發器](/help/sites-administering/msm-sync.md#rollout-triggers) 來使用。 選擇：
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 按一下 **全部儲存**.

### 將同步化動作新增至轉出設定 {#add-synchronization-actions-to-the-rollout-configuration}

轉出設定儲存在 [轉出配置節點](#create-the-rollout-configuration) 建立於 `/apps/msm/<your-project>/rolloutconfigs` 節點。

添加類型的子節點 `cq:LiveSyncAction` 將同步動作新增至轉出設定。 同步操作節點的順序決定了操作發生的順序。

1. 仍在CRXDE Lite中，請選取 [轉出設定](#create-the-rollout-configuration) 節點。

   例如：
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **建立** 具有以下節點屬性的節點：

   * **名稱**:同步操作的節點名。
名稱必須與 **動作名稱** 表格下 [同步操作](/help/sites-administering/msm-sync.md#installed-synchronization-actions)，例如 `contentCopy` 或 `workflow`.
   * **類型**: `cq:LiveSyncAction`

1. 根據需要添加和配置任意數量的同步操作節點。 重新排列動作節點，使其順序符合您希望其發生的順序。 最頂端的動作節點會先發生。

## 建立和使用簡單LiveActionFactory類 {#creating-and-using-a-simple-liveactionfactory-class}

請依照本節中的程式，開發 `LiveActionFactory` 並在轉出設定中使用。 程式使用Maven和Eclipse來開發和部署 `LiveActionFactory`:

1. [建立Maven專案](#create-the-maven-project) 然後匯入Eclipse。
1. [新增相依性](#add-dependencies-to-the-pom-file) 到POM檔案。
1. [實作 `LiveActionFactory` 介面](#implement-liveactionfactory) 並部署OSGi捆綁包。
1. [建立轉出設定](#create-the-example-rollout-configuration).
1. [建立即時副本](#create-the-live-copy).

公用Git存放庫中提供Maven專案和Java類的原始碼。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟experiencemanager-java-msmrollout專案](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### 建立Maven專案 {#create-the-maven-project}

下列程式需要您將adobe-public設定檔新增至Maven設定檔。

* 如需adobe公用設定檔的相關資訊，請參閱 [取得內容套件Maven外掛程式](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* 如需Maven設定檔案的相關資訊，請參閱Maven [設定參考](https://maven.apache.org/settings.html).

1. 開啟終端或命令列工作階段，並變更目錄以指向建立專案的位置。
1. 輸入以下命令：

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在互動式提示字元時指定下列值：

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`: `MyLiveActionFactory`
   * `version`: `1.0-SNAPSHOT`
   * `package`: `MyPackage`
   * `appsFolderName`: `myapp`
   * `artifactName`: `MyLiveActionFactory package`
   * `packageGroup`: `myPackages`

1. 啟動Eclipse和 [匯入Maven專案](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse).

### 將相依性新增至POM檔案 {#add-dependencies-to-the-pom-file}

添加依賴項，以便Eclipse編譯器可以引用 `LiveActionFactory` 程式碼。

1. 從Eclipse專案總管中，開啟檔案：

   `MyLiveActionFactory/pom.xml`

1. 在編輯器中，按一下 `pom.xml` 標籤，然後找到 `project/dependencyManagement/dependencies` 區段。
1. 在 `dependencyManagement` 元素，然後儲存檔案。

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

1. 從開啟套件組合的POM檔案 **專案總管** at `MyLiveActionFactory-bundle/pom.xml`.
1. 在編輯器中，按一下 `pom.xml` 標籤，然後找出專案/相依性區段。 在相依性元素內新增下列XML，然後儲存檔案：

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

以下 `LiveActionFactory` 類實施 `LiveAction` 會記錄來源和目標頁面的相關訊息，並複製 `cq:lastModifiedBy` 屬性從源節點到目標節點。 即時動作的名稱為 `exampleLiveAction`.

1. 在Eclipse專案總管中，以滑鼠右鍵按一下 `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` 封裝，按一下 **新增** > **類別**. 若 **名稱**，輸入 `ExampleLiveActionFactory` 然後按一下 **完成**.
1. 開啟 `ExampleLiveActionFactory.java` 檔案中，使用下列程式碼取代內容，然後儲存檔案。

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

1. 使用終端或命令會話，將目錄更改為 `MyLiveActionFactory` 目錄（Maven專案目錄）。 然後，輸入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   AEM `error.log` 檔案應該會指出套件已啟動。

   例如， [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs).

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### 建立範例轉出設定 {#create-the-example-rollout-configuration}

建立使用的MSM轉出設定 `LiveActionFactory` 您建立的項目：

1. 建立及設定 [使用標準程式轉出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)  — 並使用屬性：

   * **標題**:轉出設定範例
   * **名稱**:examplolloutconfig
   * **cq:trigger**: `publish`

### 將即時動作新增至範例轉出設定 {#add-the-live-action-to-the-example-rollout-configuration}

設定您在前一個程式中建立的轉出設定，以便使用 `ExampleLiveActionFactory` 類別。

1. 開放CRXDE Lite;例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de).
1. 在下面建立以下節點 `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **名稱**: `exampleLiveAction`
   * **類型**: `cq:LiveSyncAction`

1. 按一下 **全部儲存**.
1. 選取 `exampleLiveAction` 節點，然後新增下列屬性：

   * **名稱**: `repLastModBy`
   * **類型**: `Boolean`
   * **值**: `true`

   此屬性向 `ExampleLiveAction` 類 `cq:LastModifiedBy` 屬性應從源節點複製到目標節點。

1. 按一下 **全部儲存**.

### 建立即時副本 {#create-the-live-copy}

[建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 使用您的轉出設定，取得We.Retail參考網站的英文/產品分支的名稱：

* **來源**: `/content/we-retail/language-masters/en/products`

* **轉出設定**:轉出設定範例

啟動 **產品** （英文）頁面，並觀察 `LiveAction` 類生成：

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
* 語言的預設國家/地區(適用於程式碼，例如 `en`, `de`，其中包括)

語言清單儲存在 `/libs/wcm/core/resources/languages` 節點。 每個子節點代表一種語言或語言國家：

* 節點的名稱是語言程式碼(例如 `en` 或 `de`)或language_country代碼(例如 `en_us` 或 `de_ch`)。

* 此 `language` 節點的屬性儲存代碼語言的完整名稱。
* 此 `country` 節點的屬性會儲存代碼的國家/地區完整名稱。
* 當節點名稱僅包含語言代碼時(例如 `en`)，則國家/地區屬性為 `*`，以及其他 `defaultCountry` 屬性會儲存language-country的程式碼，以指出要使用的國家/地區。

![chlimage_1-76](assets/chlimage_1-76.png)

要修改語言，請執行以下操作：

1. 在網頁瀏覽器中開啟CRXDE Lite;例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. 選取 `/apps` 資料夾，按一下 **建立**，然後 **建立資料夾。**

   為新資料夾命名 `wcm`.

1. 重複上一步以建立 `/apps/wcm/core` 資料夾樹。 建立類型的節點 `sling:Folder` in `core` 呼叫 `resources`. <!-- ![chlimage_1-77](assets/chlimage_1-77.png) -->

1. 以滑鼠右鍵按一下 `/libs/wcm/core/resources/languages` 節點，按一下 **複製**.
1. 以滑鼠右鍵按一下 `/apps/wcm/core/resources` 資料夾，按一下 **貼上**. 根據需要修改子節點。
1. 按一下 **全部儲存**.
1. 按一下 **工具**, **操作** then **Web主控台**. 在此控制台中，按一下 **OSGi**，然後 **設定**.
1. 找到並按一下 **Day CQ WCM語言管理員**，並變更 **語言清單** to `/apps/wcm/core/resources/languages`，然後按一下 **儲存**.

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

   * 會從已推出的屬性中排除；請參閱 [從同步中排除屬性和節點類型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization).

* 關鍵視覺樣式：

   * 請確保除非取消繼承，否則不允許在觸控式UI中編輯此屬性，然後您還可以恢復繼承；可通過按一下切換以指示連接狀態的鏈/斷鏈連結來控制。

是否要轉出頁面屬性，因此，在編輯時要取消/重新啟用繼承，由對話方塊屬性控制：

* `cq-msm-lockable`

   * 適用於觸控式UI對話方塊中的項目
   * 將在對話框中建立鏈結符號
   * 僅允許在取消繼承時進行編輯（鏈結斷開）
   * 僅適用於資源的第一個子級
   * **類型**: `String`

   * **值**:持有被代價物業之名稱（與該物業之價值相若） `name`;例如，請參閱
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

當 `cq-msm-lockable` 已定義，斷裂/關閉鏈將透過以下方式與MSM互動：

* 若 `cq-msm-lockable` 為：

   * **相對** (例如 `myProperty` 或 `./myProperty`)

      * 它會新增屬性，並從中移除屬性 `cq:propertyInheritanceCancelled`.
   * **絕對** (例如 `/image`)

      * 斷開鏈將通過添加 `cq:LiveSyncCancelled` 混合 `./image` 和設定 `cq:isCancelledForChildren` to `true`.

      * 關閉鏈將恢復繼承。


>[!NOTE]
>
>`cq-msm-lockable` 應用於要編輯的資源的第一個子級，而且它在任何更深層上級上都無法工作，無論該值定義為絕對值還是相對值。

>[!NOTE]
>
>當您重新啟用繼承時，即時副本頁面屬性不會自動與來源屬性同步。 如果需要，可以手動請求同步。
