---
title: 伺服器端定制
seo-title: Server-side Customization
description: 在AEM Communities自定義伺服器端
seo-description: Customizing server-side in AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# 伺服器端定制 {#server-side-customization}

| **[⇐功能要點](essentials.md)** | **[客戶端定制⇒](client-customize.md)** |
|---|---|
|  | **[SCF把手幫⇒](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>從一個主發行版升級到下一個主發行版時，社區API的包位置可能會發生更改。

### SocialComponent介面 {#socialcomponent-interface}

SocialComponents是代表AEM Communities功能資源的POJO。 理想情況下，每個SocialComponent都表示具有外露GETter的特定resourceType，這些GETter向客戶端提供資料，以便準確表示資源。 所有業務邏輯和視圖邏輯都封裝在SocialComponent中，包括站點訪問者的會話資訊（如果需要）。

該介面定義了表示資源所需的基本GETter集。 重要的是，介面規定了&lt;string object=&quot;&quot;> getAsMap()和String toJSONString()方法，這是呈現Handlebar模板和公開資源的GETJSON終結點所必需的方法。

所有SocialComponent類必須實現介面 `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent介面 {#socialcollectioncomponent-interface}

SocialCollectionComponent介面擴展了SocialComponent介面，以更好地表示其他資源的集合。

所有SocialCollectionComponent類必須實現介面com.adobe.cq.social.scf.SocialCollectionComponent

### SocialComponentFactory介面 {#socialcomponentfactory-interface}

SocialComponentFactory（工廠）在框架中註冊SocialComponent。 工廠提供了一種方法，使框架知道指定resourceType可用的SocialComponents以及在識別多個SocialComponents時它們的優先順序。

SocialComponentFactory負責建立所選SocialComponent的實例，以便能夠使用DI慣例從工廠中注入SocialComponent所需的所有依賴項。

SocialComponentFactory是OSGi服務，可以訪問其他OSGi服務，這些服務可以通過建構子傳遞到SocialComponent。

所有SocialComponentFactory類必須實現介面 `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的實現應返回最高值，以便工廠用於getResourceType()返回的給定resourceType。

### SocialComponentFactoryManager介面 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（經理）管理在框架中註冊的所有SocialComponents，並負責選擇要用於給定資源(resourceType)的SocialComponentsFactory。 如果沒有為特定資源類型註冊工廠，則經理將返回具有給定資源的最近超級類型的工廠。

SocialComponentFactoryManager是OSGi服務，可以訪問其他OSGi服務，這些服務可以通過建構子傳遞到SocialComponent。

通過調用獲得對OSGi服務的句柄 `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API -POST請求 {#http-api-post-requests}

#### 後工序類 {#postoperation-class}

HTTP APIPOST終結點是通過實現 `SlingPostOperation` 介面（包） `org.apache.sling.servlets.post`)。

的 `PostOperation` 端點實施集 `sling.post.operation` 到操作將響應的值。 將a:operation參數設定為該值的所有POST請求都將委託給此實現類。

的 `PostOperation` 調用 `SocialOperation` 執行操作所需的操作。

的 `PostOperation` 從 `SocialOperation` 並返回對客戶端的相應響應。

#### SocialOperation類 {#socialoperation-class}

每個 `SocialOperation` 終結點擴展了AbstractSocialOperation類並重寫方法 `performOperation()`。 此方法執行完成操作並返回 `SocialOperationResult` 否則扔 `OperationException`，在這種情況下，返回帶有消息的HTTP錯誤狀態（如果可用），而不是正常JSON響應或成功的HTTP狀態代碼。

擴展 `AbstractSocialOperation` 使得 `SocialComponents` 發送JSON響應。

#### SocialOperationResult類 {#socialoperationresult-class}

的 `SocialOperationResult` 類作為 `SocialOperation` 由 `SocialComponent`、HTTP狀態代碼和HTTP狀態消息。

的 `SocialComponent` 表示受操作影響的資源。

對於「建立」操作， `SocialComponent` 包含於 `SocialOperationResult` 表示剛建立的資源，並為更新操作表示由操作更改的資源。 否 `SocialComponent` 為刪除操作返回。

使用的成功HTTP狀態代碼包括：

* 201用於建立操作
* 200用於更新操作
* 204用於刪除操作

#### OperationException類 {#operationexception-class}

安 `OperationExcepton` 如果請求無效或出現其他錯誤，例如內部錯誤、參數值錯誤、權限不正確等，則在執行操作時可能會拋出。 安 `OperationException` 由HTTP狀態代碼和錯誤消息組成，這些消息將作為對 `PostOperatoin`。

#### OperationService類 {#operationservice-class}

該社會構成框架建議，不在 `SocialOperation` 而是委託給OSGi服務。 使用OSGi服務用於業務邏輯允許 `SocialComponent`，由 `SocialOperation` 端點，與其他代碼整合，應用不同的業務邏輯。

全部 `OperationService` 類擴展 `AbstractOperationService`，允許附加可掛接到正在執行的操作的擴展。 服務中的每個操作由 `SocialOperation` 類。 的 `OperationExtensions` 可通過調用方法在操作執行期間調用類

* `performBeforeActions()`

   允許預檢查/預處理和驗證
* `performAfterActions()`

   允許進一步修改資源或調用自定義事件、工作流等

#### OperationExtension類 {#operationextension-class}

`OperationExtension` 類是可以注入到操作中的定製代碼段，允許根據業務需求定制操作。 元件的使用者可以動態和增量地向元件添加功能。 擴展/掛接模式允許開發人員專門關注擴展本身，並消除複製和覆蓋整個操作和元件的需要。

## 示例代碼 {#sample-code}

示例代碼在 [Adobe Marketing CloudGitHub](https://github.com/Adobe-Marketing-Cloud) 儲存庫。 搜索以前置詞的項目 `aem-communities` 或 `aem-scf`。

## 最佳做法 {#best-practices}

查看 [編碼准則](code-guide.md) 編碼指南和最佳實踐的章節。

另請參閱 [UGC的儲存資源提供程式(SRP)](srp.md) 瞭解如何訪問用戶生成的內容。

| **[⇐功能要點](essentials.md)** | **[客戶端定制⇒](client-customize.md)** |
|---|---|
|  | **[SCF把手幫⇒](handlebars-helpers.md)** |
