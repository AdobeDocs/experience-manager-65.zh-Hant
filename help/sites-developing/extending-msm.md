---
title: 擴充多網站管理員
description: 此頁面可協助您擴充多網站管理員的功能
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: bba64ce6-8b74-4be1-bf14-cfdf3b9b60e1
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '2582'
ht-degree: 58%

---

# 擴充多網站管理員{#extending-the-multi-site-manager}

此頁面可協助您擴充「多網站管理員」的功能：

* 了解 MSM Java API 的主要成員.
* 建立可用於轉出設定的同步化動作。
* 修改預設的語言和國家/地區代碼.

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>本頁應與 [重複使用內容：多網站管理員](/help/sites-administering/msm.md).
>
>下列網站存放庫重組的章節可能也會有意義：
>* [多站點管理員藍圖設定](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/sites-repository-restructuring-in-aem-6-5.html#multi-site-manager-blueprint-configurations)
>* [多網站管理員轉出設定](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/sites-repository-restructuring-in-aem-6-5.html#multi-site-manager-rollout-configurations)

>[!CAUTION]
>
>多網站管理員及其API在製作網站時使用，因此僅適用於製作環境。

## Java API 的概觀 {#overview-of-the-java-api}

多網站管理由以下套件組成：

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主要MSM API物件的互動如下(另請參閱 [使用的辭彙](/help/sites-administering/msm.md#terms-used))：

![主要 MSM API 物件](assets/chlimage_1-73.png)

* **`Blueprint`**

  A `Blueprint` （如所示） [Blueprint設定](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations))指定即時副本可以繼承內容的頁面。

  ![藍圖](assets/chlimage_1-74.png)

   * 藍圖設定 (`Blueprint`) 的使用為選用，但是：

      * 允許作者使用 **轉出** 來源上的選項(以（明確）推送修改至繼承自此來源的即時副本)。
      * 允許作者使用 **建立網站**；這可讓使用者輕鬆選取語言並設定即時副本的結構。
      * 為任何產生的即時副本定義預設轉出設定。

* **`LiveRelationship`**

  此 `LiveRelationship` 指定即時副本分支中的資源與其對等來源/Blueprint資源之間的連線（關係）。

   * 實現繼承和推出時會使用此關係。
   * `LiveRelationship` 物件會針對和該關係相關之推出設定 (`RolloutConfig`)、`LiveCopy` 以及 `LiveStatus` 物件提供存取 (參照)。

   * 例如，在 `/content/copy/us` (來自 `/content/we-retail/language-masters` 的來源/藍圖) 中會建立 Live Copy。 資源 `/content/we.retail/language-masters/en/jcr:content` 和 `/content/copy/us/en/jcr:content` 會建立關係。

* **`LiveCopy`**

  `LiveCopy` 保留關係的設定詳細資料( `LiveRelationship`)，位於即時副本資源及其來源/Blueprint資源之間。

   * 使用 `LiveCopy` 類別存取頁面的路徑、來源/藍圖頁面的路徑、推出設定，而子頁面是否也包含在 `LiveCopy` 中。

   * `LiveCopy` 節點會在每次使用「**建立網站**」或者「**建立 Live Copy**」時建立。

* **`LiveStatus`**

  `LiveStatus` 物件可讓您存取的執行階段狀態 `LiveRelationship`. 用於查詢 Live Copy 的同步狀態。

* **`LiveAction`**

  A `LiveAction` 是在轉出涉及的每個資源上執行的動作。

   * LiveActions僅由RolloutConfigs產生。

* **`LiveActionFactory`**

  建立 `LiveAction` 物件已指定 `LiveAction` 設定。 設定會在存放庫中儲存為資源。

* **`RolloutConfig`**

  此 `RolloutConfig` 儲存清單 `LiveActions`，以便在觸發時使用。 `LiveCopy` 會繼承 `RolloutConfig`，而結果會在 `LiveRelationship` 中顯示。

   * 第一次設定即時副本時，也會使用RolloutConfig （這會觸發LiveActions）。

## 建立新的同步動作 {#creating-a-new-synchronization-action}

建立自訂同步操作以與您的轉出設定一起使用。 建立同步化動作，當 [已安裝的動作](/help/sites-administering/msm-sync.md#installed-synchronization-actions) 不符合您特定的應用程式需求。 為此，請建立兩個類別：

* 執行動作的 [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) 介面的實作。
* 實作的OSGI元件 [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 介面並建立您的執行個體 `LiveAction` 類別。

`LiveActionFactory` 會針對以下特定設定建立 `LiveAction` 類別的執行個體：

* `LiveAction` 類別會包括以下方法：

   * `getName`: 傳回動作的名稱. 此名稱是用來參照動作，例如在轉出設定中。
   * `execute`: 執行動作的任務.

* `LiveActionFactory` 類別會包括以下項目：

   * `LIVE_ACTION_NAME`：包含關聯欄位名稱的欄位 `LiveAction`. 此名稱必須和由 `getName` 方法 (屬於 `LiveAction` 類別) 傳回的值相符。

   * `createAction`：建立例項 `LiveAction`. 選用的 `Resource` 參數可用於提供設定資訊。

   * `createsAction`：傳回關聯專案的名稱 `LiveAction`.

### 存取 LiveAction 設定節點 {#accessing-the-liveaction-configuration-node}

使用存放庫中的 `LiveAction` 設定節點，以儲存會影響 `LiveAction` 執行個體執行階段行為的資訊。儲存 `LiveAction` 設定的存放庫中的節點可用於執行階段時的 `LiveActionFactory` 物件。因此，您可以對設定節點新增屬性，且必要時在您的 `LiveActionFactory` 實作中使用這些屬性。

例如，`LiveAction` 需要儲存藍圖作者的名稱。設定節點的屬性包括儲存該資訊的藍圖頁面屬性名稱。在執行階段時，`LiveAction` 會從設定中擷取屬性名稱，然後獲取屬性值。

[`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 方法的參數是一種 `Resource` 物件。這個 `Resource` 物件代表 `cq:LiveSyncAction` 轉出設定中此即時動作的節點；請參閱 [建立轉出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration). 和平常一樣，使用設定節點時，您應該將其調整為 `ValueMap` 物件：

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

### 存取目標節點、來源節點和 LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

下列物件會以 `LiveAction` 物件之 `execute` 方法的參數提供：

* A [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) 代表即時副本來源的物件。
* A `Resource` 代表即時副本目標的物件。
* Live Copy 的 [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) 物件.
* 此 `autoSave` 值會指出您的 `LiveAction` 應儲存對存放庫進行的變更。

* 重設值表示轉出重設模式。

您可以透過這些物件取得 `LiveCopy`. 您還可以使用 `Resource` 物件獲取 `ResourceResolver`、`Session` 和 `Node` 物件。這些物件對於操作存放庫內容非常有用：

在以下程式碼的第一行中，來源是指來源頁面的 `Resource` 物件：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>`Resource` 引數可能是 `null` 或者 `Resources` 物件 (不適應於 `Node` 物件，例如 [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/NonExistingResource.html) 物件)。

## 建立新的推出設定 {#creating-a-new-rollout-configuration}

當安裝的轉出設定不符合您的應用程式需求時，建立轉出設定：

* [建立推出設定](#create-the-rollout-configuration)。
* [將同步動作新增到推出設定中](#add-synchronization-actions-to-the-rollout-configuration).

然後，在藍圖或 Live Copy 頁面上設定推出設定時，您即可使用新的推出設定。

>[!NOTE]
>
>另請參閱「[自訂推出的最佳做法](/help/sites-administering/msm-best-practices.md#customizing-rollouts)」。

### 建立「推出設定」 {#create-the-rollout-configuration}

1. 開啟CRXDE Lite；例如：
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 瀏覽到 :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >這是您專案的自訂版本：
   >`/libs/msm/wcm/rolloutconfigs`
   >如果這是您的第一個設定，則必須將此 `/libs` 分支用為範本，以便在 `/apps` 下面建立新分支。

   >[!NOTE]
   >
   >您不得變更 `/libs` 路徑。
   >這是因為 `/libs` 下次升級執行個體時會被覆寫（當您套用hotfix或feature pack時，很可能會被覆寫）。
   >設定和其他變更的建議方法是：
   >
   >* 重新建立所需專案（即存在於中的專案） `/libs`)下 `/apps`
   >* 進行任何變更 `/apps`

1. 在此底下 **建立** 具有下列屬性的節點：

   * **名稱**：轉出設定的節點名稱。 md#installed-synchronization-actions)，例如： `contentCopy` 或 `workflow`.
   * **類型**：`cq:RolloutConfig`

1. 將以下屬性新增至此節點：
   * **名稱**：`jcr:title`
     **類型**：`String`
     **值**：將顯示在UI中的識別標題。
   * **名稱**：`jcr:description`
     **類型**：`String`
     **值**：選用的說明。
   * **名稱**：`cq:trigger`
     **類型**：`String`
     **值**：所要使用的[推出觸發器. ](/help/sites-administering/msm-sync.md#rollout-triggers)選取自：
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 按一下&#x200B;**「儲存全部」**。

### 將「同步動作」新增到「推出設定」中 {#add-synchronization-actions-to-the-rollout-configuration}

轉出設定儲存在 [轉出設定節點](#create-the-rollout-configuration) 您已在「 」下建立的 `/apps/msm/<your-project>/rolloutconfigs` 節點。

新增類型 `cq:LiveSyncAction` 的子節點，以將同步動作新增到推出設定中。同步動作節點的順序會決定動作發生的順序。

1. 仍然在CRXDE Lite中，選擇您的 [轉出設定](#create-the-rollout-configuration) 節點。

   例如：
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **建立具有下列節點屬性的節點：**

   * **名稱**：同步動作的節點名稱.
名稱必須與 **動作名稱** 在表格中的 [同步化動作](/help/sites-administering/msm-sync.md#installed-synchronization-actions)例如， `contentCopy` 或 `workflow`.
   * **類型**：`cq:LiveSyncAction`

1. 依您需要的數量新增並設定同步動作節點。重新排列動作節點，使其顯示的順序和您希望它們出現的順序相符。最頂端的動作節點會先出現。

## 建立並使用簡單的 LiveActionFactory 類別 {#creating-and-using-a-simple-liveactionfactory-class}

依照本節中說明的程序開發一個 `LiveActionFactory` 並用於推出設定中。此程序會使用 Maven 和 Eclipse 來開發和部署 `LiveActionFactory`：

1. [建立 maven 專案](#create-the-maven-project)並將其匯入到 Eclipse 中。
1. [新增相依性](#add-dependencies-to-the-pom-file)到 POM 檔案。
1. [實作 `LiveActionFactory` 介面](#implement-liveactionfactory) 並部署OSGi套件組合。
1. [建立推出設定](#create-the-example-rollout-configuration)。
1. [建立 Live Copy](#create-the-live-copy)。

Maven 專案和 Java 類別的原始碼可在公用 Git 存放庫中取得。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟experiencemanager-java-msmrollout專案](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### 建立 Maven 專案 {#create-the-maven-project}

下列程式要求您已將adobe-public設定檔新增到Maven設定檔。

* 如需 adobe-public 設定檔的資訊，請參閱[獲取內容套件 Maven 外掛程式](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* 如需 Maven 設定檔案的資訊，請參閱 Maven [設定參考](https://maven.apache.org/settings.html)。

1. 開啟終端機或命令列工作階段，並將目錄變更為指向建立專案的位置。
1. 輸入以下命令：

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在互動式提示處指定下列值：

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`: `MyLiveActionFactory`
   * `version`: `1.0-SNAPSHOT`
   * `package`: `MyPackage`
   * `appsFolderName`: `myapp`
   * `artifactName`: `MyLiveActionFactory package`
   * `packageGroup`: `myPackages`

1. 啟動Eclipse和 [匯入Maven專案](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse).

### 新增相依性到 POM 檔案 {#add-dependencies-to-the-pom-file}

新增相依性，以便 Eclipse 編譯器可以參照在 `LiveActionFactory` 程式碼中使用的類別。

1. 從Eclipse專案總管中，開啟檔案：

   `MyLiveActionFactory/pom.xml`

1. 在編輯器中，按一下 `pom.xml` 索引標籤並找到 `project/dependencyManagement/dependencies` 區段。
1. 在 `dependencyManagement` 元素裡面新增以下 XML，然後儲存檔案。

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

1. 從&#x200B;**專案總管** (在 `MyLiveActionFactory-bundle/pom.xml`) 開啟套件組合的 POM 檔案。
1. 在編輯器中，按一下 `pom.xml` 索引標籤並找到「專案/相依性」區段。在相依性元素裡面新增以下 XML，然後儲存檔案：

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

### 實作 LiveActionFactory {#implement-liveactionfactory}

以下 `LiveActionFactory` 類別會實作一項 `LiveAction`，這會記錄來源和目標頁面的訊息，並將 `cq:lastModifiedBy` 屬性從來源節點複製到目標節點。即時動作的名稱為 `exampleLiveAction`。

1. 在Eclipse專案總管中，以滑鼠右鍵按一下 `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` 封裝並按一下 **新增** > **類別**. 對於&#x200B;**名稱**，請輸入 `ExampleLiveActionFactory` 然後按一下「**完成**」。
1. 開啟 `ExampleLiveActionFactory.java` 檔案，將內容更換為以下程式碼，然後儲存檔案。

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

1. 使用終端機或命令工作階段，將目錄變更為 `MyLiveActionFactory` 目錄 (Maven 專案目錄)。然後，輸入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   AEM `error.log` 檔案應指示該套件組合已啟動。

   例如， [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs).

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### 建立推出設定範例 {#create-the-example-rollout-configuration}

建立使用您所建立 `LiveActionFactory` 的 MSM 推出設定：

1. 建立和設定 [使用標準程式轉出組態](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)  — 並使用屬性：

   * **標題**：推出設定範例
   * **名稱**：examplerolloutconfig
   * **cq：trigger**：`publish`

### 將即時動作新增到推出設定範例中 {#add-the-live-action-to-the-example-rollout-configuration}

設定您在前一個程序中建立的推出設定，以便該設定使用 `ExampleLiveActionFactory` 類別。

1. 開啟CRXDE Lite；例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de).
1. 在 `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content` 下面建立以下節點：

   * **名稱**：`exampleLiveAction`
   * **類型**：`cq:LiveSyncAction`

1. 按一下&#x200B;**「儲存全部」**。
1. 選取 `exampleLiveAction` 節點並新增下列屬性：

   * **名稱**：`repLastModBy`
   * **類型**：`Boolean`
   * **值**：`true`

   此屬性會指示 `ExampleLiveAction` 類別 `cq:LastModifiedBy` 屬性應該從來源復寫到目標節點。

1. 按一下&#x200B;**「儲存全部」**。

### 建立 Live Copy {#create-the-live-copy}

[建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) ，位於We.Retail參考網站的英文/產品分支，使用您的轉出設定：

* **來源**：`/content/we-retail/language-masters/en/products`

* **推出設定**：推出設定範例

啟動來源分支的&#x200B;**產品** (英文) 頁面並觀察 `LiveAction` 類別所產生的紀錄訊息：

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

<!--
## Removing the Chapters Step in the Create Site Wizard {#removing-the-chapters-step-in-the-create-site-wizard}

In some cases, the **Chapters** selection is not required in the create site wizard (only the **Languages** selection is required). To remove this step in the default We.Retail English blueprint:

1. In CRX Explorer, remove the node:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigate to `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` and create a node:

    1. **Name** = `chapters`; **Type** = `cq:Widget`.

1. Add following properties to the new node:

    1. **Name** = `name`; **Type** = `String`; **Value** = `msm:chapterPages`

    1. **Name** = `value`; **Type** = `String`; **Value** = `all`

    1. **Name** = `xtype`; **Type** = `String`; **Value** = `hidden`
-->

## 變更語言名稱和預設國家/地區 {#changing-language-names-and-default-countries}

AEM 會使用一組預設的語言和國家/地區代碼。

* 預設的語言代碼根據 ISO-639-1 定義的兩個字母小寫代碼。
* 預設的國家/地區代碼是根據 ISO 3166 定義的兩個字母小寫或大寫代碼。

MSM 會使用儲存的語言和國家/地區代碼清單來確定和頁面語言版本名稱相關聯的國家/地區名稱。如有需要，您可以變更清單的以下部分：

* 語言標題
* 國家/地區名稱
* 語言預設國家/地區（適用於下列程式碼） `en`， `de`，等等)

語言清單會儲存在 `/libs/wcm/core/resources/languages` 節點下方。每個子節點即代表一種語言或一種語言國家：

* 節點的名稱是語言代碼(例如 `en` 或 `de`)或language_country程式碼(例如 `en_us` 或 `de_ch`)。

* 節點的 `language` 屬性會儲存代碼語言的完整名稱。
* 節點的 `country` 屬性會儲存代碼國家/地區的完整名稱。
* 當節點名稱僅包含語言代碼時 (例如 `en`)，國家/地區屬性為 `*`，會有額外的 `defaultCountry` 屬性儲存語言-國家/地區的代碼，以顯示要使用的國家/地區。

![語言定義](assets/chlimage_1-76.png)

若要修改語言：

1. 在網頁瀏覽器中開啟CRXDE Lite；例如， [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. 選取 `/apps` 資料夾並按一下&#x200B;**「建立」**，然後再按一下&#x200B;**「建立資料夾」。**

   命名新資料夾`wcm`。

1. 重複上一個步驟以建立 `/apps/wcm/core` 資料夾樹狀結構。在稱之為 `sling:Folder` 的 `core` 中建立類型 `resources` 的節點。 <!-- ![Resources](assets/chlimage_1-77.png) -->

1. 在 `/libs/wcm/core/resources/languages` 節點上按一下右鍵，然後按一下「**複製**」。
1. 在 `/apps/wcm/core/resources` 資料夾上按一下右鍵，然後按一下「**貼上**」。根據需要修改子節點。
1. 按一下&#x200B;**「儲存全部」**。
1. 按一下「**工具**」、「**操作**」，然後再按一下「**Web 主控台**」。在此主控台上，按一下 **OSGi**，然後按一下「**設定**」。
1. 找到並按一下 **Day CQ WCM 語言管理員**，然後將&#x200B;**語言清單**&#x200B;的值變更為 `/apps/wcm/core/resources/languages`，然後再按一下「**儲存**」。

   ![Day CQ WCM 語言管理員](assets/chlimage_1-78.png)

## 在頁面屬性上設定 MSM 鎖 （觸控式UI） {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

建立自訂頁面屬性時，您可能需要考慮新屬性是否適合推出到任何 Live Copy。

例如，如果正要新增兩個新的頁面屬性：

* 連絡人電子郵件：

   * 此屬性不需要推出，因為每個國家/地區（或品牌等）都有不同。

* 索引鍵視覺樣式：

   * 專案要求是推出此屬性，因為此屬性（通常）對所有國家/地區（或品牌等）都是通用的。

那麼您需要確保：

* 連絡人電子郵件：

* 會從轉出屬性中排除；請參閱 [從同步處理排除屬性和節點型別](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization).

* 索引鍵視覺樣式：

* 請確定除非取消繼承，否則不允許您在觸控式UI中編輯此屬性，您也可以恢復繼承；若要控制繼承，請按一下用來切換以指出連線狀態的鏈/斷鏈連結。

頁面屬性是否需要推出，以及因此在編輯時是否需要取消/恢復繼承，會由對話框屬性控制：

* `cq-msm-lockable`

   * 適用於觸控式UI對話方塊中的專案
   * 會在對話方塊中建立鏈結符號
   * 只有在取消繼承時（鏈結已中斷）才允許編輯
   * 僅適用於資源的第一個子層級
      * **類型**：`String`

      * **值**：保留考量中屬性的名稱(且可比較屬性的值 `name`；例如，請參閱
        `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

若已定義 `cq-msm-lockable`，則毀損/關閉鏈會以下列方式和 MSM 互動：

* 如果值 `cq-msm-lockable` 為：

   * **相對值** (例如，`myProperty` 或是 `./myProperty`)

      * 它會從新增和移除屬性 `cq:propertyInheritanceCancelled`.

   * **絕對值** (例如，`/image`)

      * 中斷鏈結將會透過新增 `cq:LiveSyncCancelled` mixin至 `./image` 和設定 `cq:isCancelledForChildren` 至 `true`.

      * 關閉鏈結將會回覆繼承。

>[!NOTE]
>
>`cq-msm-lockable` 適用於要編輯的資源的第一個子層級，並且無論將該值定義為絕對值或是相對值，它在任何更深入的上階層級上都不起作用。

>[!NOTE]
>
>重新啟用繼承時，Live Copy 頁面屬性不會和來源屬性自動同步。如有需要，您可以手動要求同步。
