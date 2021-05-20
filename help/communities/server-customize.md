---
title: 伺服器端自訂
seo-title: 伺服器端自訂
description: 在AEM Communities中自訂伺服器端
seo-description: 在AEM Communities中自訂伺服器端
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# 伺服器端自訂{#server-side-customization}

| **[⇐功能要點](essentials.md)** | **[用戶端自訂⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>從一個主要版本升級至下一個主要版本時，Communities API的套件位置可能會有所變更。

### SocialComponent介面{#socialcomponent-interface}

SocialComponents是POJO，代表AEM Communities功能的資源。 理想情況下，每個SocialComponent都表示特定的resourceType，它具有向客戶端提供資料的公開的GETter，以便準確表示資源。 所有業務邏輯和檢視邏輯都封裝在SocialComponent中，包括網站訪客的工作階段資訊（如有必要）。

該介面定義了表示資源所需的基本GETter集。 重要的是，介面規定了Map&lt;String, Object> getAsMap()和String toJSONString()方法，這些方法是呈現Handlebars範本並公開資源的GETJSON端點所必需的。

所有SocialComponent類別都必須實作介面`com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent介面{#socialcollectioncomponent-interface}

SocialCollectionComponent介面可擴充SocialComponent介面，以更妥善地呈現其他資源的集合。

所有SocialCollectionComponent類別都必須實作介面com.adobe.cq.social.scf.SocialCollectionComponent

### SocialComponentFactory介面{#socialcomponentfactory-interface}

SocialComponentFactory(factory)會將SocialComponent註冊到框架中。 工廠提供一種方法，讓架構知道在識別多個SocialComponents時，指定resourceType可使用哪些SocialComponents及其優先順序排名。

SocialComponentFactory負責建立所選SocialComponent的例項，以便能夠使用DI實務從工廠插入SocialComponent所需的所有相依性。

SocialComponentFactory是OSGi服務，可存取其他OSGi服務，這些服務可透過建構函式傳遞至SocialComponent。

所有SocialComponentFactory類都必須實作介面`com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的實作應傳回最高值，以便工廠用於getResourceType()傳回的指定resourceType。

### SocialComponentFactoryManager介面{#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（管理員）管理在框架中註冊的所有SocialComponents，並負責選擇用於指定資源(resourceType)的SocialComponentFactory。 如果沒有為特定資源類型註冊工廠，則經理將返回具有給定資源的最接近超級類型的工廠。

SocialComponentFactoryManager是OSGi服務，可存取其他OSGi服務，這些服務可透過建構函式傳遞至SocialComponent。

調用`com.adobe.cq.social.scf.SocialComponentFactoryManager`可獲得對OSGi服務的句柄

### HTTP API -POST要求{#http-api-post-requests}

#### 後操作類{#postoperation-class}

HTTP APIPOST端點是透過實作`SlingPostOperation`介面（套件`org.apache.sling.servlets.post`）所定義的PostOperation類。

`PostOperation`端點實施會將`sling.post.operation`設定為操作將回應的值。 所有將a:operation參數設為該值的POST請求將委派給此實施類別。

`PostOperation`調用`SocialOperation`，該執行操作所需的操作。

`PostOperation`從`SocialOperation`接收結果，並將相應的響應返回給客戶端。

#### SocialOperation類{#socialoperation-class}

每個`SocialOperation`端點都擴展了AbstractSocialOperation類，並覆蓋方法`performOperation()`。 此方法會執行完成操作並傳回`SocialOperationResult`或擲回`OperationException`所需的所有動作，在此情況下，會傳回含有訊息的HTTP錯誤狀態（如果有），取代一般JSON回應或成功的HTTP狀態代碼。

延伸`AbstractSocialOperation`可重複使用`SocialComponents`以傳送JSON回應。

#### SocialOperationResult類{#socialoperationresult-class}

`SocialOperationResult`類由`SocialComponent`、HTTP狀態代碼和HTTP狀態消息組成，由`SocialOperation`的結果返回。

`SocialComponent`表示受操作影響的資源。

對於建立操作，`SocialOperationResult`中包含的`SocialComponent`表示剛建立的資源，對於更新操作，它表示操作更改的資源。 沒有為刪除操作返回`SocialComponent`。

使用的成功HTTP狀態代碼為：

* 201：建立操作
* 更新操作200
* 204：刪除操作

#### OperationException類{#operationexception-class}

如果請求無效或發生其他錯誤（如內部錯誤、錯誤的參數值、不正確的權限等），則執行操作時可能會擲回`OperationExcepton`。 `OperationException`由HTTP狀態代碼和錯誤消息組成，這些消息作為對`PostOperatoin`的響應返回給客戶端。

#### 操作服務類{#operationservice-class}

社會元件框架建議不在`SocialOperation`類內實施負責執行操作的業務邏輯，而是將其委託給OSGi服務。 將OSGi服務用於業務邏輯允許由`SocialOperation`端點作用的`SocialComponent`與其他代碼整合併應用不同的業務邏輯。

所有`OperationService`類都擴展`AbstractOperationService`，允許與正在執行的操作掛接的其他擴展。 服務中的每個操作都由`SocialOperation`類表示。 可通過調用方法在操作執行期間調用`OperationExtensions`類

* `performBeforeActions()`

   允許預檢查/預處理和驗證
* `performAfterActions()`

   允許進一步修改資源或叫用自訂事件、工作流程等

#### 操作擴展類{#operationextension-class}

`OperationExtension` 類別是可插入到操作中的自定義代碼片段，允許定制操作以滿足業務需要。元件的使用者可以動態且逐步地新增功能至元件。 擴充功能/連結模式可讓開發人員專注在擴充功能本身，而無須複製和覆寫整個作業和元件。

## 程式碼範例{#sample-code}

范常式式碼可在[Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud)存放庫中使用。 搜尋首碼為`aem-communities`或`aem-scf`的專案。

## 最佳作法 {#best-practices}

檢視[編碼准則](code-guide.md)區段，了解AEM Communities開發人員的各種編碼准則和最佳實務。

另請參閱UGC](srp.md)的[儲存資源提供者(SRP)，以了解如何存取使用者產生的內容。

| **[⇐功能要點](essentials.md)** | **[用戶端自訂⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
