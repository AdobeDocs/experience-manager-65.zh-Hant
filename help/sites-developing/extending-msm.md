---
title: 擴展多站點管理器
seo-title: Extending the Multi Site Manager
description: 此頁可幫助您擴展多站點管理器的功能
seo-description: This page helps you extend the functionalities of the Multi Site Manager
uuid: dfa7d050-29fc-4401-8d4d-d6ace6b49bea
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6128c91a-4173-42b4-926f-bbbb2b54ba5b
docset: aem65
exl-id: bba64ce6-8b74-4be1-bf14-cfdf3b9b60e1
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '2575'
ht-degree: 1%

---

# 擴展多站點管理器{#extending-the-multi-site-manager}

此頁可幫助您擴展多站點管理器的功能：

* 瞭解MSM Java API的主要成員。
* 建立新同步操作，該操作可用於部署配置。
* 修改預設語言和國家代碼。

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>此頁應與 [重新使用內容：多站點管理器](/help/sites-administering/msm.md)。
>
>站點資源庫重組的以下部分可能也值得關注：
>* [多站點管理器藍圖配置](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/sites-repository-restructuring-in-aem-6-5.html#multi-site-manager-blueprint-configurations)
>* [多站點管理器部署配置](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/sites-repository-restructuring-in-aem-6-5.html#multi-site-manager-rollout-configurations)


>[!CAUTION]
>
>創作網站時使用多站點管理器及其API，因此僅用於作者環境。

## Java API概述 {#overview-of-the-java-api}

多站點管理由以下包組成：

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主MSM API對象交互如下（另請參見） [使用的術語](/help/sites-administering/msm.md#terms-used)):

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   A `Blueprint` (如 [藍圖配置](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations))指定即時副本可從其繼承內容的頁面。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * 藍圖配置的使用( `Blueprint`)是可選的，但是：

      * 允許作者使用 **推廣** 選項（將修改推送到從此源繼承的活動副本）。
      * 允許作者使用 **建立站點**;這允許用戶輕鬆選擇語言並配置即時副本的結構。
      * 定義所有生成的即時副本的預設部署配置。

* **`LiveRelationship`**

   的 `LiveRelationship` 指定即時複製分支中的資源與其等效源/藍圖資源之間的連接（關係）。

   * 在實現繼承和展出時使用這些關係。
   * `LiveRelationship` 對象提供對部署配置的訪問（引用）( `RolloutConfig`) `LiveCopy`, `LiveStatus` 與關係相關的對象。

   * 例如，在 `/content/copy/us` 從源/藍圖 `/content/we-retail/language-masters`。 資源 `/content/we.retail/language-masters/en/jcr:content` 和 `/content/copy/us/en/jcr:content` 形成關係。

* **`LiveCopy`**

   `LiveCopy` 保存關係的配置詳細資訊( `LiveRelationship`)與其源/藍圖資源之間。

   * 使用 `LiveCopy` 類以訪問頁面的路徑、源/藍圖頁的路徑、部署配置以及子頁面是否也包含在 `LiveCopy`。

   * A `LiveCopy` 每次建立節點 **建立站點** 或 **建立即時拷貝** 的子菜單。

* **`LiveStatus`**

   `LiveStatus` 對象提供對 `LiveRelationship`。 用於查詢即時副本的同步狀態。

* **`LiveAction`**

   A `LiveAction` 是在部署中涉及的每個資源上執行的操作。

   * LiveActions僅由SolutConfigs生成。

* **`LiveActionFactory`**

   建立 `LiveAction` 給定的對象 `LiveAction` 配置。 配置作為資源儲存在儲存庫中。

* **`RolloutConfig`**

   的 `RolloutConfig` 包含 `LiveActions`，在觸發時使用。 的 `LiveCopy` 繼承 `RolloutConfig` 結果出現在 `LiveRelationship`。

   * 首次設定即時拷貝時還使用SollutConfig（觸發LiveActions）。

## 建立新同步操作 {#creating-a-new-synchronization-action}

建立要用於部署配置的自定義同步操作。 在 [已安裝的操作](/help/sites-administering/msm-sync.md#installed-synchronization-actions) 不符合您的特定應用程式要求。 為此，請建立兩個類：

* 執行 [ `com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) 執行操作的介面。
* 實現OSGI的OSGI元件 [ `com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 介面和建立實例 `LiveAction` 類。

的 `LiveActionFactory` 建立實例 `LiveAction` 給定配置的類：

* `LiveAction` 類包括以下方法：

   * `getName`:返回操作的名稱該名稱用於引用操作，例如在部署配置中。
   * `execute`:執行操作的任務。

* `LiveActionFactory` 類包括以下成員：

   * `LIVE_ACTION_NAME`:包含關聯名稱的欄位 `LiveAction`。 此名稱必須與 `getName` 方法 `LiveAction` 類。

   * `createAction`:建立實例 `LiveAction`。 可選 `Resource` 參數可用於提供配置資訊。

   * `createsAction`:返回關聯的名稱 `LiveAction`。

### 訪問LiveAction配置節點 {#accessing-the-liveaction-configuration-node}

使用 `LiveAction` 儲存庫中的配置節點，用於儲存影響 `LiveAction` 實例。 儲存庫中儲存 `LiveAction` 配置可用於 `LiveActionFactory` 運行時的對象。 因此，您可以將屬性添加到配置節點中，並在 `LiveActionFactory` 執行。

例如， `LiveAction` 需要儲存藍圖作者的姓名。 配置節點的屬性包括儲存資訊的藍圖頁的屬性名稱。 在運行時， `LiveAction` 從配置中檢索屬性名稱，然後獲取屬性值。

的參數 [`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 方法是 `Resource` 的雙曲餘切值。 此 `Resource` 對象表示 `cq:LiveSyncAction` 此即時操作的節點；見 [建立部署配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。 與通常使用配置節點時一樣，您應將其調整為 `ValueMap` 對象：

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

以下對象作為 `execute` 方法 `LiveAction` 對象：

* A [ `Resource`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) 表示Live Copy源的對象。
* A `Resource` 表示Live Copy目標的對象。
* 的 [ `LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) 即時副本的對象。
* 的 `autoSave` 值指示 `LiveAction` 應保存對儲存庫所做的更改。

* 重置值指示重新部署重置模式。

從這些對象中，您可以獲取有關 `LiveCopy`。 您還可以使用 `Resource` 對象 `ResourceResolver`。 `Session`, `Node` 對象。 這些對象對於處理儲存庫內容非常有用：

在以下代碼的第一行中，原始碼是 `Resource` 源頁的對象：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>的 `Resource` 參數 `null` 或 `Resources` 不適應的對象 `Node` 對象，如 [ `NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/NonExistingResource.html) 對象。

## 建立新的展示配置 {#creating-a-new-rollout-configuration}

當安裝的部署配置不滿足您的應用程式要求時，建立部署配置：

* [建立部署配置](#create-the-rollout-configuration)。
* [將同步操作添加到展示配置](#add-synchronization-actions-to-the-rollout-configuration)。

然後，在藍圖或即時複製頁上設定部署配置時，您可以使用新的部署配置。

>[!NOTE]
>
>另請參閱 [自定義部署的最佳做法](/help/sites-administering/msm-best-practices.md#customizing-rollouts)。

### 建立推廣配置 {#create-the-rollout-configuration}

要建立新的展開配置：

1. 開放CRXDE Lite;例如：
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 瀏覽到 :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >這是您的項目的自定義版本：
   >`/libs/msm/wcm/rolloutconfigs`
   >如果這是您的第一個配置，則 `/libs` 分支必須用作模板，以在 `/apps`。

   >[!NOTE]
   >
   >您不能更改 `/libs` 路徑。
   >這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時很可能被覆蓋）。
   >建議的配置和其他更改方法是：
   >
   >* 重新建立所需項(如 `/libs`) `/apps`
   >* 在 `/apps`


1. 在此下 **建立** 具有以下屬性的節點：

   * **名稱**:推廣配置的節點名稱。 md#installedsynchronization-actions)，例如 `contentCopy` 或 `workflow`。
   * **類型**: `cq:RolloutConfig`

1. 將以下屬性添加到此節點：
   * **名稱**: `jcr:title`

      **類型**: `String`
      **值**:將在UI中顯示的標識標題。
   * **名稱**: `jcr:description`

      **類型**: `String`
      **值**:可選說明。
   * **名稱**: `cq:trigger`

      **類型**: `String`
      **值**:的 [推廣觸發器](/help/sites-administering/msm-sync.md#rollout-triggers) 的下界。 從以下位置選擇：
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 按一下 **全部保存**。

### 將同步操作添加到展示配置 {#add-synchronization-actions-to-the-rollout-configuration}

部署配置儲存在 [部署配置節點](#create-the-rollout-configuration) 你創造的 `/apps/msm/<your-project>/rolloutconfigs` 的下界。

添加類型的子節點 `cq:LiveSyncAction` 將同步操作添加到展示配置。 同步操作節點的順序決定了操作發生的順序。

1. 仍處於CRXDE Lite中，請選擇 [部署配置](#create-the-rollout-configuration) 的下界。

   例如：
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **建立** 具有以下節點屬性的節點：

   * **名稱**:同步操作的節點名稱。
名稱必須與 **操作名稱** 在 [同步操作](/help/sites-administering/msm-sync.md#installed-synchronization-actions)，例如 `contentCopy` 或 `workflow`。
   * **類型**: `cq:LiveSyncAction`

1. 根據需要添加和配置任意數量的同步操作節點。 重新排列操作節點，使其順序與您希望其發生的順序相匹配。 最頂層的操作節點首先出現。

## 建立和使用簡單LiveActionFactory類 {#creating-and-using-a-simple-liveactionfactory-class}

按照本節中的步驟開發 `LiveActionFactory` 並將其用於部署配置。 該過程使用Maven和Eclipse開發和部署 `LiveActionFactory`:

1. [建立主項目](#create-the-maven-project) 並導入Eclipse。
1. [添加依賴項](#add-dependencies-to-the-pom-file) 到POM檔案。
1. [實施 `LiveActionFactory` 面](#implement-liveactionfactory) 部署OSGi捆綁包。
1. [建立部署配置](#create-the-example-rollout-configuration)。
1. [建立即時副本](#create-the-live-copy)。

Maven項目和Java類的原始碼可在公共Git儲存庫中使用。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟體驗管理器 — java-msmloult項目](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### 建立Maven項目 {#create-the-maven-project}

以下過程要求您已將adobe-public配置檔案添加到Maven設定檔案中。

* 有關adobe-public配置檔案的資訊，請參見 [獲取內容包Maven插件](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* 有關Maven設定檔案的資訊，請參見Maven [設定引用](https://maven.apache.org/settings.html)。

1. 開啟終端或命令行會話，並更改目錄以指向建立項目的位置。
1. 輸入以下命令：

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在互動式提示時指定以下值：

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`: `MyLiveActionFactory`
   * `version`: `1.0-SNAPSHOT`
   * `package`: `MyPackage`
   * `appsFolderName`: `myapp`
   * `artifactName`: `MyLiveActionFactory package`
   * `packageGroup`: `myPackages`

1. 啟動Eclipse和 [導入Maven項目](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse)。

### 向POM檔案添加依賴項 {#add-dependencies-to-the-pom-file}

添加依賴關係，以便Eclipse編譯器可以引用在 `LiveActionFactory` 代碼。

1. 從Eclipse項目資源管理器中，開啟檔案：

   `MyLiveActionFactory/pom.xml`

1. 在編輯器中，按一下 `pom.xml` 的子菜單 `project/dependencyManagement/dependencies` 的子菜單。
1. 在 `dependencyManagement` 元素，然後保存檔案。

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

1. 從中開啟捆綁包的POM檔案 **項目瀏覽器** 在 `MyLiveActionFactory-bundle/pom.xml`。
1. 在編輯器中，按一下 `pom.xml` 頁籤，然後找到項目/依賴項部分。 在依賴關係元素內添加以下XML，然後保存檔案：

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

### 實施LiveActionFactory {#implement-liveactionfactory}

以下 `LiveActionFactory` 類實現 `LiveAction` 記錄有關源和目標頁的消息，並複製 `cq:lastModifiedBy` 從源節點到目標節點的屬性。 即時操作的名稱為 `exampleLiveAction`。

1. 在Eclipse項目瀏覽器中，按一下右鍵 `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` 包，按一下 **新建** > **類**。 對於 **名稱**&#x200B;輸入 `ExampleLiveActionFactory` 然後按一下 **完成**。
1. 開啟 `ExampleLiveActionFactory.java` 檔案，用以下代碼替換內容並保存檔案。

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

1. 使用終端或命令會話，將目錄更改為 `MyLiveActionFactory` 目錄（Maven項目目錄）。 然後，輸入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   AEM `error.log` 檔案應指示捆綁已啟動。

   比如說， [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs)。

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### 建立示例展示配置 {#create-the-example-rollout-configuration}

建立使用 `LiveActionFactory` 建立的：

1. 建立和配置 [使用標準過程進行部署配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)  — 並使用屬性：

   * **標題**:示例部署配置
   * **名稱**:示例olloutconfig
   * **cq：觸發器**: `publish`

### 將即時操作添加到示例部署配置 {#add-the-live-action-to-the-example-rollout-configuration}

配置在上一步驟中建立的展示配置，以便使用 `ExampleLiveActionFactory` 類。

1. 開放CRXDE Lite;比如說， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)。
1. 在下面建立以下節點 `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **名稱**: `exampleLiveAction`
   * **類型**: `cq:LiveSyncAction`

1. 按一下 **全部保存**。
1. 選擇 `exampleLiveAction` 並添加以下屬性：

   * **名稱**: `repLastModBy`
   * **類型**: `Boolean`
   * **值**: `true`

   此屬性向 `ExampleLiveAction` 類 `cq:LastModifiedBy` 屬性應從源節點複製到目標節點。

1. 按一下 **全部保存**。

### 建立即時副本 {#create-the-live-copy}

[建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 使用您的推廣配置，在We.Retail Reference Site的英文/產品分支中：

* **源**: `/content/we-retail/language-masters/en/products`

* **部署配置**:示例部署配置

激活 **產品** （英文）頁，並觀察 `LiveAction` 類生成：

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

## 更改語言名稱和預設國家/地區 {#changing-language-names-and-default-countries}

使AEM用預設語言和國家代碼集。

* 預設語言代碼是ISO-639-1定義的小寫雙字母代碼。
* 預設國家代碼是ISO 3166定義的小寫或大寫兩字母代碼。

MSM使用儲存的語言和國家代碼清單來確定與頁面的語言版本名稱關聯的國家/地區名稱。 如果需要，可以更改清單的以下方面：

* 語言標題
* 國家/地區名稱
* 語言的預設國家(對於代碼，如 `en`。 `de`，其中包括

語言清單儲存在 `/libs/wcm/core/resources/languages` 的下界。 每個子節點表示語言或語言國家/地區：

* 節點的名稱是語言代碼(如 `en` 或 `de`)或language_country代碼(例如 `en_us` 或 `de_ch`)。

* 的 `language` 節點的屬性儲存代碼語言的全名。
* 的 `country` 節點的屬性儲存代碼的國家/地區的全名。
* 當節點名稱僅包含語言代碼時(如 `en`)，國家/地區 `*`，以及 `defaultCountry` 屬性儲存語言國家（地區）的代碼，以指示要使用的國家（地區）。

![chlimage_1-76](assets/chlimage_1-76.png)

要修改語言：

1. 在Web瀏覽器中開啟CRXDE Lite;比如說， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. 選擇 `/apps` 資料夾，按一下 **建立**，則 **建立資料夾。**

   命名新資料夾 `wcm`。

1. 重複上一步以建立 `/apps/wcm/core` 資料夾樹。 建立類型的節點 `sling:Folder` 在 `core` 調用 `resources`。 <!-- ![chlimage_1-77](assets/chlimage_1-77.png) -->

1. 按一下右鍵 `/libs/wcm/core/resources/languages` 按一下 **複製**。
1. 按一下右鍵 `/apps/wcm/core/resources` 資料夾，按一下 **貼上**。 根據需要修改子節點。
1. 按一下 **全部保存**。
1. 按一下 **工具**。 **操作** 然後 **Web控制台**。 在此控制台中按一下 **OSGi**，則 **配置**。
1. 查找並按一下 **第CQ WCM語言管理器**，並更改 **語言清單** 至 `/apps/wcm/core/resources/languages`，然後按一下 **保存**。

   ![chlimage_1-78](assets/chlimage_1-78.png)

## 在頁面屬性上配置MSM鎖（啟用觸摸的UI） {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

在建立自定義頁面屬性時，您可能需要考慮新屬性是否有資格向任何即時副本發佈。

例如，如果添加了兩個新頁面屬性：

* 連絡人電子郵件:

   * 無需推出此屬性，因為它在每個國家/地區（或品牌等）都不同。

* 關鍵視覺樣式：

   * 項目要求是，此房產將按所有國家（或品牌等）共有的方式推出。

然後，您需要確保：

* 連絡人電子郵件:

* 從展開的屬性中排除；見 [從同步中排除屬性和節點類型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization)。

* 關鍵視覺樣式：

* 確保不允許在啟用觸摸的用戶介面中編輯此屬性，除非取消繼承，還可以恢復繼承；通過按一下可切換以指示連接狀態的鏈/斷鏈鏈鏈來控制此操作。

頁面屬性是否要展開，因此編輯時要取消/恢復繼承，由對話框屬性控制：

* `cq-msm-lockable`

   * 適用於啟用觸摸的用戶介面對話框中的項
   * 將在對話框中建立連結符號
   * 僅允許在取消繼承（鏈鏈斷開）時編輯
   * 僅適用於資源的第一個子級
      * **類型**: `String`

      * **值**:持有被代價物業之名稱（與物業價值相若） `name`;例如，請參見
         `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

當 `cq-msm-lockable` 已定義，斷開/關閉鏈將以下方式與MSM相互作用：

* 如果 `cq-msm-lockable` 為：

   * **相對** (例如 `myProperty` 或 `./myProperty`)

      * 它將從中添加和刪除屬性 `cq:propertyInheritanceCancelled`。
   * **絕對** (例如 `/image`)

      * 通過添加 `cq:LiveSyncCancelled` 混入 `./image` 設定 `cq:isCancelledForChildren` 至 `true`。

      * 關閉鏈將還原繼承。


>[!NOTE]
>
>`cq-msm-lockable` 應用於要編輯的資源的第一個子級，而且無論該值定義為絕對值還是相對值，它在任何更深層的祖先級上都不起作用。

>[!NOTE]
>
>重新啟用繼承時，即時複製頁屬性不會自動與source屬性同步。 如果需要，可手動請求同步。
