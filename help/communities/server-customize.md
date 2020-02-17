---
title: 伺服器端自訂
seo-title: 伺服器端自訂
description: 自訂AEM Communities中的伺服器端
seo-description: 自訂AEM Communities中的伺服器端
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 伺服器端自訂 {#server-side-customization}

| **[‹功能基本工具](essentials.md)** | **[用戶端自訂的‹](client-customize.md)** |
|---|---|
|  | **[SCF Handlepers ‡](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>當從一個主要版本升級至下一個版本時，Communities API的封裝位置可能會有所變更。

### SocialComponent介面 {#socialcomponent-interface}

SocialComponents是POJO，代表AEM Communities功能的資源。 理想情況下，每個SocialComponent都代表特定的resourceType，並有公開的GETters，可提供資料給用戶端，以精確呈現資源。 所有商業邏輯和檢視邏輯都封裝在Social元件中，包括網站訪客的作業資訊（如有需要）。

該介面定義了表示資源所需的基本GETter集。 重要的是，介面規定了Map&lt;String, Object> getAsMap()和String toJSONString()方法，這些方法是轉譯Handlebars範本和公開GET JSON端點資源的必要方式。

所有SocialComponent類別都必須實作介面 `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent介面 {#socialcollectioncomponent-interface}

SocialCollectionComponent介面可擴充SocialComponent介面，以更好地呈現其他資源的集合。

所有SocialCollectionComponent類別都必須實作介面com.adobe.cq.sosical.scf.SocialCollectionComponent

### SocialComponentFactory介面 {#socialcomponentfactory-interface}

SocialComponentFactory(factory)會將SocialComponent註冊為架構。 該工廠提供一種方法，讓框架知道什麼SocialComponents可用於給定的resourceType及其優先順序ranking&amp;ast;識別多個Social元件時。

SocialComponentFactory負責建立所選SocialComponent的例項，以便能夠使用DI實務從工廠中注入SocialComponent所需的所有相依性。

SocialComponentFactory是OSGi服務，可存取其他OSGi服務，這些服務可透過建構函式傳遞至SocialComponent。

所有SocialComponentFactory類都必須實作介面 `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的實作應傳回最高值，以便工廠用於getResourceType()傳回的指定resourceType。

### SocialComponentFactoryManager介面 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（管理員）會管理在架構中註冊的所有SocialComponents，並負責選擇SocialComponentFactory以用於指定的資源(resourceType)。 如果沒有為特定資源類型註冊工廠，則經理將返回具有給定資源最接近超類型的工廠。

SocialComponentFactoryManager是OSGi服務，可存取其他OSGi服務，這些服務可透過建構函式傳遞至SocialComponent。

通過調用OSGi服務獲得對OSGi服務的句柄 `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API —— 貼文要求 {#http-api-post-requests}

#### 後工序類 {#postoperation-class}

HTTP API POST端點是PostOperation類，通過實施介面（包） `SlingPostOperation`定義 `org.apache.sling.servlets.post`這些類。

端 `PostOperation`點實施設 `sling.post.operation`置為操作將響應的值。 設為該值的：operation參數的所有POST請求都將委託給此實施類。

調用 `PostOperation`執行操 `SocialOperation`作所需操作的操作。

接 `PostOperation`收結果，並 `SocialOperation`傳回適當的回應給用戶端。

#### SocialOperation類 {#socialoperation-class}

每個 `SocialOperation`端點都會擴充AbstractSocialOperation類別並覆寫方法。 `performOperation().`This method會執行完成作業並傳回 `SocialOperationResult``OperationException`或擲回的所有必要動作，在此情況下，會傳回含訊息的HTTP錯誤狀態（如果有），以取代一般JSON回應或成功的HTTP狀態碼。

擴充 `AbstractSocialOperation`功能可重複使用傳 `SocialComponents`送JSON回應。

#### SocialOperationResult類 {#socialoperationresult-class}

類 `SocialOperationResult`作為返回的結果返回， `SocialOperation`並由 `SocialComponent`HTTP狀態代碼和HTTP狀態消息組成。

表 `SocialComponent`示受工序影響的資源。

對於建立工序， `SocialComponent`中包 `SocialOperationResult`括的代表剛建立的資源，並代表由工序更改的資源。 不 `SocialComponent`會傳回刪除作業。

使用的成功HTTP狀態代碼為

* 2010年建立操作
* 200 for Update operations
* 204 for Delete operations

#### OperationException類 {#operationexception-class}

如果 `OperationExcepton`請求無效或發生其他錯誤，例如內部錯誤、參數值錯誤、權限不當等，則在執行操作時可能會拋出。 由 `OperationException`HTTP狀態代碼和錯誤消息組成，這些消息作為對的響應返回給客戶 `PostOperatoin`。

#### OperationService類 {#operationservice-class}

社交元件架構建議負責執行操作的商業邏輯不在類別中實作， `SocialOperation`而是委派給OSGi服務。 使用OSGi服務用於業務邏輯 `SocialComponent`允許端點所作 `SocialOperation`用的與其它代碼整合併應用不同的業務邏輯。

所有 `OperationService`類都可 `AbstractOperationService`以擴展，允許附加擴展，這些擴展可以連接到正在執行的操作。 服務中的每個操作都由類表 `SocialOperation`示。 通過 `OperationExtensions`調用這些方法，可以在操作執行期間調用類

* `performBeforeActions()`
允許預檢／預處理和驗證
* `performAfterActions()`
允許進一步修改資源或調用自定義事件、工作流等

#### OperationExtension類 {#operationextension-class}

`OperationExtension`類是可插入操作的自定義代碼片段，允許定制操作以滿足業務需要。 元件的使用者可動態且遞增地新增功能至元件。 擴充／掛接模式可讓開發人員專注於擴充功能本身，而不需複製和覆寫整個作業和元件。

## 范常式式碼 {#sample-code}

范常式式碼可在 [Adobe Marketing Cloud GitHub儲存庫中取得](https://github.com/Adobe-Marketing-Cloud) 。 搜尋前置詞為或的 `aem-communities` 專案 `aem-scf`。

## Best Practices {#best-practices}

檢視「 [編碼准則](code-guide.md) 」區段，以取得AEM Communities開發人員的各種編碼准則和最佳實務。

另請參 [閱UGC的儲存資源提供商(SRP)](srp.md) ，瞭解如何訪問用戶生成的內容。

| **[‹功能基本工具](essentials.md)** | **[用戶端自訂的‹](client-customize.md)** |
|---|---|
|  | **[SCF Handlepers ‡](handlebars-helpers.md)** |

