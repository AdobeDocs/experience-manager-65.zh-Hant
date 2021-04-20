---
title: 服務使用AEM者
seo-title: 服務使用AEM者
description: 在中瞭解服務用戶AEM。
seo-description: 在中瞭解服務用戶AEM。
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1789'
ht-degree: 0%

---

# &lt;a0/AEM>中的服務用戶{#service-users-in-aem}

## 概覽 {#overview}

取得管理工作階段或資源解析程式的主要AEM方式是使用Sling提供的`SlingRepository.loginAdministrative()`和`ResourceResolverFactory.getAdministrativeResourceResolver()`方法。

但是，這兩種方法都沒有圍繞[最少權限原則設計，而且讓開發人員過於容易，無法為其內容早期規劃適當的結構和相應的訪問控制級別(ACL)。 ](https://en.wikipedia.org/wiki/Principle_of_least_privilege)如果此類服務中存在漏洞，則通常會導致向`admin`用戶提供權限升級，即使代碼本身不需要管理權限也能正常工作。

## 如何逐步淘汰管理會話{#how-to-phase-out-admin-sessions}

### 優先順序0:此功能是否為活動／需要／廢棄？{#priority-is-the-feature-active-needed-derelict}

有時可能未使用管理工作階段，或完全停用功能。 如果您的實作就是這樣，請確定您完全移除功能，或將它與[NOP程式碼](https://en.wikipedia.org/wiki/NOP)搭配使用。

### 優先順序1:使用請求會話{#priority-use-the-request-session}

在可能的情況下重新調整您的功能，讓指定的已驗證要求工作階段可用來讀取或寫入內容。 如果這不可行，則通常可以採用下列優先事項。

### 優先順序2:重構內容{#priority-restructure-content}

許多問題都可以透過重組內容來解決。 進行重組時，請牢記以下簡單規則：

* **更改訪問控制**

   * 請確定真正需要存取權的使用者或群組實際擁有存取權；

* **調整內容結構**

   * 將它移至其他位置，例如存取控制符合可用的要求工作階段；
   * 變更內容粒度；

* **將程式碼重新調整為適當的服務**

   * 將商業邏輯從JSP程式碼移至服務。 這可讓不同的內容建模。

此外，請確定您開發的任何新功能都遵循下列原則：

* **安全性需求應推動內容結構**

   * 管理存取控制應該感覺自然
   * 訪問控制必須由儲存庫而不是應用程式強制執行

* **使用節點類型**

   * 限制可設定的屬性集

* **尊重隱私權設定**

   * 對於私有配置檔案，一個示例是不公開在專用`/profile`節點上找到的配置檔案圖片、電子郵件或全名。

## 嚴格訪問控制{#strict-access-control}

無論您是在重組內容時應用訪問控制還是為新服務用戶應用訪問控制，都必須盡可能應用最嚴格的ACL。 使用所有可能的訪問控制設施：

* 例如，不應在`/apps`上套用`jcr:read`，而只將它套用至`/apps/*/components/*/analytics`

* 使用[restrictions](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 為節點類型應用ACL
* 限制權限

   * 例如，只需編寫屬性時，請勿授予`jcr:write`權限；請改用`jcr:modifyProperties`

## 服務用戶和映射{#service-users-and-mappings}

如果上述失敗，Sling 7提供Service User Mapping服務，可設定Bundle-to-user對應和兩種對應的API方法：` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)`和` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)`，它們僅返回具有已配置用戶權限的會話／資源解析器。 這些方法具有以下特點：

* 它們允許將服務對應給用戶
* 他們使子服務用戶定義更容易
* 中心配置點是：`org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` =  `service-name` [ &quot;:&quot;子服務名稱  ] 

* `service-id` 映射到資源解析器和／或JCR儲存庫用戶ID以進行驗證
* `service-name` 是提供服務的包的符號名稱

## 其他Recommendations{#other-recommendations}

### 以service-user {#replacing-the-admin-session-with-a-service-user}取代admin-session

服務用戶是JCR用戶，沒有設定口令和執行特定任務所需的最少權限集。 沒有設定密碼表示無法與服務使用者登入。

取代管理作業的方法，是以服務使用者作業取代。 如有需要，也可以由多個子服務使用者取代。

若要以服務使用者取代管理工作階段，您應執行下列步驟：

1. 確定您服務的必要權限，並牢記最低權限的原則。
1. 檢查是否已有使用者具備您所需的權限設定。 如果沒有符合您需求的現有使用者，請建立新的系統服務使用者。 需要RTC才能建立新的服務用戶。 有時，建立多個子服務用戶（例如，一個用於寫作，一個用於閱讀）來劃分更多訪問是明智的。
1. 為您的用戶設定和測試ACE。
1. 為服務和`user/sub-users`添加`service-user`映射

1. 將服務使用者sling功能提供給您的搭售：更新至`org.apache.sling.api`的最新版本。

1. 將程式碼中的`admin-session`取代為`loginService`或`getServiceResourceResolver` API。

## 建立新服務用戶{#creating-a-new-service-user}

在您確認服務用戶清單中沒有用戶適用於您的使用案例AEM，且相應的RTC問題已獲得批准後，您可以繼續將新用戶添加到預設內容中。

建議的方法是建立服務用戶，以使用位於&#x200B;*https://&lt;server>:&lt;port>/crx/explorer/index.jsp*&#x200B;的儲存庫瀏覽器

其目標是取得有效的`jcr:uuid`屬性，這是透過內容封裝安裝來建立使用者的必要屬性。

您可以通過以下方式建立服務用戶：

1. 前往位於&#x200B;*https://&lt;server>:&lt;port>/crx/explorer/index.jsp*&#x200B;的儲存庫瀏覽器
1. 按螢幕左上角的&#x200B;**登錄**&#x200B;連結以管理員身份登錄。
1. 接著，建立並命名您的系統使用者。 要將用戶建立為系統用戶，請將中間路徑設定為`system` ，並根據您的需要添加可選子資料夾：

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 驗證您的系統用戶節點的外觀如下：

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >請注意，沒有與服務使用者相關聯的混音類型。 這表示系統使用者將沒有存取控制原則。

將對應的。content.xml新增至套件內容時，請確定您已設定`rep:authorizableId`，且主要類型為`rep:SystemUser`。 應該是這樣的：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## 向ServiceUserMapper配置{#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}添加配置修改

要從服務向相應的系統用戶添加映射，您需要為` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)`服務建立工廠配置。 為了保持這種模組，可使用[Sling amend mechanism](https://issues.apache.org/jira/browse/SLING-3578)提供這種配置。 建議使用[Sling Initial Content Loading](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html)來安裝搭售的這類組態：

1. 在您搭售的src/main/resources資料夾下建立子資料夾SLING-INF/content
1. 在此資料夾中，建立名為org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.refined-&lt;您工廠組態的某個唯一名稱>.xml，並包含您工廠組態的內容（包括所有子服務使用者映射）。 範例:

1. 在您套裝的`src/main/resources`資料夾下方建立`SLING-INF/content`資料夾；
1. 在此資料夾中建立一個檔案`named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml`，其中包含出廠配置的內容，包括所有子服務用戶映射。

   為了便於說明，請使用名為`org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`的檔案：

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

1. 在您搭售的`pom.xml`中的`maven-bundle-plugin`組態中參考Sling初始內容。 範例:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 安裝您的套件，並確定已安裝工廠配置。 您可以透過下列方式執行此動作：

   * 前往Web控制台，網址為&#x200B;*https://serverhost:serveraddress/system/console/configMgr*
   * 搜尋&#x200B;**Apache Sling Service User Mapper Service Andition**
   * 按一下連結，查看是否有正確的設定。

## 處理服務{#dealing-with-shared-sessions-in-services}中的共用會話

對`loginAdministrative()`的呼叫通常會與共用作業一起顯示。 這些會話是在服務啟動時獲得的，並且僅在服務停止後才註銷。 雖然這是常見的做法，但它導致了兩個問題：

* **安全性：** 此類管理會話用於快取並返回綁定到共用會話的資源或其他對象。在調用堆棧的稍後部分，這些對象可以適應具有提升權限的會話或資源解析器，而且呼叫者通常不清楚它是他們正在操作的管理會話。
* **效能：在** Oak共用工作階段中，可能會造成效能問題，目前不建議使用。

最顯而易見的安全風險解決方案是，只需將`loginAdministrative()`呼叫替換為`loginService()`呼叫，以限制權限讓使用者接受。 但是，這不會對任何潛在的效能降級產生任何影響。 可能的緩解措施是，將所有請求的資訊包在與會話無關聯的對象中。 然後，視需要建立（或銷毀）工作階段。

建議的方法是重新調整服務的API，讓呼叫者控制建立／銷毀工作階段。

## JSP中的管理會話{#administrative-sessions-in-jsps}

JSP無法使用`loginService()`，因為沒有相關服務。 不過，JSP中的管理會話通常是違反MVC模式的信號。

這可以用兩種方式來修正：

1. 以允許與使用者作業一起操縱內容的方式重組內容；
1. 將邏輯擷取至提供API的服務，然後供JSP使用。

第一種方法是優選的方法。

## 處理事件、複製預處理器和作業{#processing-events-replication-preprocessors-and-jobs}

處理事件或工作時（在某些情況下），觸發事件的對應作業通常會遺失。 這會導致事件處理常常使用管理作業來處理其工作。 要解決這個問題，可以想見的方法各不相同，各有其優點和缺點：

1. 在事件裝載中傳遞`user-id`並使用模擬。

   **優點：** 易於使用。

   **缺點：** 仍使用 `loginAdministrative()`。它會重新驗證已經驗證的請求。

1. 建立或重複使用可存取資料的服務使用者。

   **優點：** 符合目前的設計。需要最少的變更。

   **缺點：需** 要非常強大的服務用戶才能靈活，這很容易導致權限升級。避開安全模型。

1. 在事件裝載中傳遞`Subject`的序列化，並根據該主題建立`ResourceResolver`。 例如，在`ResourceResolverFactory`中使用JAAS `doAsPrivileged`。

   **優點：從** 安全性的角度進行簡潔的實作。它避免了重認證，並且以原始權限操作。 安全相關程式碼對事件的使用者是透明的。

   **缺點：需** 要重構。安全相關程式碼對事件的使用者透明，這個事實也可能導致問題。

第三種方法目前是首選的處理技術。

## 工作流進程{#workflow-processes}

在工作流進程實現中，觸發工作流的相應用戶會話通常丟失。 這會導致工作流程程式通常使用管理工作階段來執行其工作。

為瞭解決這些問題，建議使用[處理事件、複製預處理器和作業](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs)中提及的相同方法。

## SlingPOST處理器和已刪除頁面{#sling-post-processors-and-deleted-pages}

在吊索POST處理器實施中使用了幾個管理會話。 通常，管理會話用於訪問正在處理的POST中待刪除的節點。 因此，它們不再透過請求作業階段提供。 可以訪問一個節點待刪除，以揭露其他情況下不可訪問的元資料。
