---
title: 服務用AEM戶
seo-title: Service Users in AEM
description: 瞭解中的服務用AEM戶。
seo-description: Learn about Service Users in AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 0%

---

# 服務用AEM戶{#service-users-in-aem}

## 概觀 {#overview}

獲取中的管理會話或資源解析程式的主AEM要方法是 `SlingRepository.loginAdministrative()` 和 `ResourceResolverFactory.getAdministrativeResourceResolver()` 方法。

但是，這兩種方法都不是圍繞 [最小特權原則](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 讓開發人員很容易就無法及早為其內容規劃適當的結構和相應的訪問控制級別(ACL)。 如果此類服務中存在漏洞，則通常會導致權限提升到 `admin` 用戶，即使代碼本身不需要管理權限即可工作。

## 如何逐步淘汰管理會話 {#how-to-phase-out-admin-sessions}

### 優先順序0:該功能是否處於活動狀態/需要/廢棄？ {#priority-is-the-feature-active-needed-derelict}

可能未使用管理會話，或功能完全禁用。 如果實施中存在這種情況，請確保完全刪除該功能或將其與 [NOP代碼](https://en.wikipedia.org/wiki/NOP)。

### 優先順序1:使用請求會話 {#priority-use-the-request-session}

只要可能，重新構建功能，使給定的經過驗證的請求會話可用於讀取或寫入內容。 如果這不可行，則通常可以採用下列優先事項。

### 優先順序2:重構內容 {#priority-restructure-content}

許多問題可以通過重組內容來解決。 在進行重組時，請牢記以下簡單規則：

* **更改訪問控制**

   * 確保真正需要訪問的用戶或組實際具有訪問權限；

* **細化內容結構**

   * 將其移動到其他位置，例如，在訪問控制與可用的請求會話匹配的位置；
   * 更改內容粒度；

* **將代碼重構為適當的服務**

   * 將業務邏輯從JSP代碼移至服務。 這允許進行不同的內容建模。

另外，確保您開發的任何新功能都遵循以下原則：

* **安全要求應推動內容結構**

   * 管理訪問控制應讓您感到自然
   * 訪問控制必須由儲存庫而非應用程式強制實施

* **使用節點類型**

   * 限制可設定的屬性集

* **尊重隱私設定**

   * 在私有配置式中，一個示例是不公開在私有配置式上找到的配置檔案圖片、電子郵件或全名 `/profile` 的下界。

## 嚴格訪問控制 {#strict-access-control}

無論您是在重構內容時應用訪問控制，還是在為新服務用戶應用訪問控制時，都必須應用盡可能嚴格的ACL。 使用所有可能的訪問控制設施：

* 例如，不應應用 `jcr:read` 上 `/apps`，僅將其應用於 `/apps/*/components/*/analytics`

* 使用 [限制](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 為節點類型應用ACL
* 限制權限

   * 例如，當僅需要寫入屬性時，不要 `jcr:write` 許可；使用 `jcr:modifyProperties` 改

## 服務用戶和映射 {#service-users-and-mappings}

如果上述方法失敗，Sling 7將提供服務用戶映射服務，該服務允許配置捆綁到用戶的映射和兩種相應的API方法： ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` 和 ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` 返回僅具有已配置用戶權限的會話/資源解析程式。 這些方法具有以下特點：

* 它們允許將服務映射到用戶
* 它們使定義子服務用戶成為一種義務
* 中心配置點是： `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [ &quot;:&quot;子服務名 ] 

* `service-id` 映射到資源解析程式和/或JCR儲存庫用戶ID以進行身份驗證
* `service-name` 是提供服務的捆綁包的符號名稱

## 其他Recommendations {#other-recommendations}

### 用服務用戶替換管理會話 {#replacing-the-admin-session-with-a-service-user}

服務用戶是JCR用戶，沒有密碼集和執行特定任務所需的最小權限集。 未設定密碼意味著無法與服務用戶登錄。

取消管理會話的一種方法是將其替換為服務用戶會話。 如果需要，也可以用多個子服務用戶替換。

要用服務用戶替換管理會話，應執行以下步驟：

1. 確定服務所需的權限，同時牢記最少權限的原則。
1. 檢查是否已有用戶具有您所需的權限設定。 如果現有用戶與您的需求不匹配，則建立新的系統服務用戶。 需要RTC來建立新服務用戶。 有時，建立多個子服務用戶（例如，一個用於寫入，一個用於閱讀）來劃分更多訪問是有意義的。
1. 為用戶設定和testACE。
1. 添加 `service-user` 為您的服務和 `user/sub-users`

1. 使服務用戶吊帶功能可用於您的捆綁包：更新到 `org.apache.sling.api`。

1. 替換 `admin-session` 你的密碼里 `loginService` 或 `getServiceResourceResolver` API。

## 建立新服務用戶 {#creating-a-new-service-user}

在您驗證服務用戶清單中的用戶AEM不適用於您的使用案例且相應的RTC問題已獲批准後，您可以繼續將新用戶添加到預設內容。

建議的方法是建立服務用戶，以在 *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

目標是獲得一個 `jcr:uuid` 屬性，該屬性是通過內容包安裝建立用戶所必需的。

您可以通過以下方式建立服務用戶：

1. 正在轉到儲存庫資源管理器(位於 *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. 通過按 **登錄** 連結。
1. 接下來，建立並命名系統用戶。 要將用戶建立為系統，請將中間路徑設定為 `system` 並根據需要添加可選子資料夾：

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 驗證系統用戶節點的外觀如下：

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >請注意，沒有與服務用戶關聯的混合類型。 這意味著系統用戶將沒有訪問控制策略。

將相應的.content.xml添加到捆綁包的內容時，請確保已設定 `rep:authorizableId` 主要類型是 `rep:SystemUser`。 它應該是這樣的：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## 向ServiceUserMapper配置添加配置修正 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

要將映射從您的服務添加到相應的系統用戶，您需要為 ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)` 服務。 為保持此模組化，可以使用 [吊具修正機構](https://issues.apache.org/jira/browse/SLING-3578)。 建議將此類配置與捆綁包一起安裝的方法是： [吊索初始內容載入](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. 在捆綁包的src/main/resources資料夾下建立子資料夾SLING-INF/內容
1. 在此資料夾中建立名為org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.refinded-&lt;some unique=&quot;&quot; name=&quot;&quot; for=&quot;&quot; your=&quot;&quot; factory=&quot;&quot; configuration=&quot;&quot;>.xml，包含出廠配置的內容（包括所有子服務用戶映射）。 範例:

1. 建立 `SLING-INF/content` 資料夾 `src/main/resources` 資料夾；
1. 在此資料夾中建立檔案 `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` 包括所有子服務用戶映射。

   為了進行說明，請取一個名為 `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. 在配置中引用Sling初始內容 `maven-bundle-plugin` 的 `pom.xml` 你的包。 範例:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 安裝捆綁包並確保已安裝出廠配置。 您可以透過以下方式進行：

   * 轉到Web控制台 *https://serverhost:serveraddress/system/console/configMgr*
   * 搜索 **《 Apache Sling服務用戶映射器服務修正》**
   * 按一下連結查看是否有正確的配置。

## 處理服務中的共用會話 {#dealing-with-shared-sessions-in-services}

呼叫 `loginAdministrative()` 通常與共用會話一起顯示。 這些會話在服務激活時獲得，並且僅在服務停止後註銷。 儘管這是常見的做法，但它導致了兩個問題：

* **安全性：** 此類管理會話用於快取和返回綁定到共用會話的資源或其他對象。 稍後在調用堆棧中，這些對象可以適應具有提升權限的會話或資源解析器，並且調用者通常不清楚它是他們正在操作的管理會話。
* **效能：** 在Oak共用會話中，可能會導致效能問題，目前不建議使用它們。

對於安全風險，最顯而易見的解決方案是 `loginAdministrative()` 打電話 `loginService()` 一個給具有受限權限的用戶。 但是，這不會對任何潛在的效能降級產生任何影響。 緩解這種情況的一種可能方式是將所有請求的資訊包裝在與會話沒有關聯的對象中。 然後，根據需要建立（或銷毀）會話。

建議的方法是重構服務的API，使調用方能夠控制會話的建立/銷毀。

## JSP中的管理會話 {#administrative-sessions-in-jsps}

JSP無法使用 `loginService()`，因為沒有關聯的服務。 但是，JSP中的管理會話通常是違反MVC範例的標誌。

這可以通過兩種方式來解決：

1. 以允許通過用戶會話來操縱內容的方式重組內容；
1. 將邏輯解壓到提供API的服務，該API隨後可供JSP使用。

第一種方法是優選的。

## 處理事件、複製預處理器和作業 {#processing-events-replication-preprocessors-and-jobs}

在處理事件或作業（在某些情況下）時，觸發事件的相應會話通常會丟失。 這會導致事件處理程式和作業處理器經常使用管理會話來執行其工作。 解決這個問題有不同的可想而知的方法，每一種方法都有其優勢和劣勢：

1. 通過 `user-id` 在事件負載中使用模擬。

   **優點：** 易用。

   **缺點：** 仍使用 `loginAdministrative()`。 它重新驗證已經過身份驗證的請求。

1. 建立或重用有權訪問資料的服務用戶。

   **優點：** 與當前設計一致。 需要最小的更改。

   **缺點：** 需要非常強大的服務用戶靈活，這很容易導致權限升級。 繞過安全模型。

1. 通過序列化 `Subject` 在事件負載中，並建立 `ResourceResolver` 基於這個主題。 一個示例是使用JAAS `doAsPrivileged` 的 `ResourceResolverFactory`。

   **優點：** 從安全形度清理實施。 它避免了重認證，並且以原始權限運行。 安全相關代碼對事件的消費者是透明的。

   **缺點：** 需要重構。 安全相關代碼對事件的消費者透明這一事實也可能導致問題。

第三種方法是目前優選的處理技術。

## 工作流進程 {#workflow-processes}

在工作流進程實現中，觸發工作流的相應用戶會話通常會丟失。 這會導致工作流進程經常使用管理會話來執行其工作。

為瞭解決這些問題，建議採取《公約》第13條中提及的相同辦法 [處理事件、複製預處理器和作業](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) 。

## SlingPOST處理器和已刪除頁 {#sling-post-processors-and-deleted-pages}

在吊具POST處理器實施中使用了幾個管理會話。 通常，管理會話用於訪問正在處理的POST中等待刪除的節點。 因此，它們不再通過請求會話可用。 可以訪問待刪除的節點以披露除此之外不應訪問的元。
