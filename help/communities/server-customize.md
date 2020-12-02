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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---


# 伺服器端自訂{#server-side-customization}

| **[‹功能基本工具](essentials.md)** | **[用戶端自訂的‹](client-customize.md)** |
|---|---|
|  | **[SCF Handlepers ‡](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>當從一個主要版本升級至下一個版本時，Communities API的封裝位置可能會有所變更。

### SocialComponent介面{#socialcomponent-interface}

SocialComponents是POJO，代表AEM Communities功能的資源。 理想情況下，每個SocialComponent都代表特定的resourceType，並有公開的GETters，可提供資料給用戶端，以精確呈現資源。 所有商業邏輯和檢視邏輯都封裝在Social元件中，包括網站訪客的作業資訊（如有需要）。

該介面定義了表示資源所需的基本GETter集。 重要的是，介面規定了Map&lt;String, Object> getAsMap()和String toJSONString()方法，這些方法是轉譯Handlebars範本和公開GET JSON端點資源的必要方式。

所有SocialComponent類別都必須實作介面`com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent介面{#socialcollectioncomponent-interface}

SocialCollectionComponent介面可擴充SocialComponent介面，以更好地呈現其他資源的集合。

所有SocialCollectionComponent類別都必須實作介面com.adobe.cq.sosical.scf.SocialCollectionComponent

### SocialComponentFactory介面{#socialcomponentfactory-interface}

SocialComponentFactory(factory)會將SocialComponent註冊為架構。 工廠提供一種方法，讓框架知道指定resourceType的SocialComponents可用項目，以及在識別多個SocialComponents時的優先順序排名。

SocialComponentFactory負責建立所選SocialComponent的例項，以便能夠使用DI實務從工廠中注入SocialComponent所需的所有相依性。

SocialComponentFactory是OSGi服務，可存取其他OSGi服務，這些服務可透過建構函式傳遞至SocialComponent。

所有SocialComponentFactory類都必須實作介面`com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的實作應傳回最高值，以便工廠用於getResourceType()傳回的指定resourceType。

### SocialComponentFactoryManager介面{#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（管理員）會管理在架構中註冊的所有SocialComponents，並負責選擇SocialComponentFactory以用於指定的資源(resourceType)。 如果沒有為特定資源類型註冊工廠，則經理將返回具有給定資源最接近超類型的工廠。

SocialComponentFactoryManager是OSGi服務，可存取其他OSGi服務，這些服務可透過建構函式傳遞至SocialComponent。

通過調用`com.adobe.cq.social.scf.SocialComponentFactoryManager`獲得OSGi服務的句柄

### HTTP API - POST請求{#http-api-post-requests}

#### 後操作類{#postoperation-class}

HTTP API POST端點是通過實施`SlingPostOperation`介面（包`org.apache.sling.servlets.post`）定義的PostOperation類。

`PostOperation`端點實施將`sling.post.operation`設定為操作將響應的值。 設為該值的：operation參數的所有POST請求都將委託給此實施類。

`PostOperation`調用`SocialOperation` ，該&lt;a1/>執行操作所需的操作。

`PostOperation`從`SocialOperation`接收結果，並將相應的響應返回給客戶端。

#### SocialOperation類{#socialoperation-class}

每個`SocialOperation`端點都擴展了AbstractSocialOperation類並覆蓋方法`performOperation()`。 此方法會執行完成操作並傳回`SocialOperationResult`或擲回`OperationException`所需的所有動作，在此情況下，會傳回含訊息的HTTP錯誤狀態（如果有的話），以取代一般的JSON回應或成功的HTTP狀態碼。

延伸`AbstractSocialOperation`可重複使用`SocialComponents`來傳送JSON回應。

#### SocialOperationResult類{#socialoperationresult-class}

`SocialOperationResult`類作為`SocialOperation`的結果返回，並由`SocialComponent`、HTTP狀態代碼和HTTP狀態消息組成。

`SocialComponent`表示受操作影響的資源。

對於建立操作，`SocialOperationResult`中包含的`SocialComponent`表示剛建立的資源，對於更新操作，它表示由操作更改的資源。 刪除操作不會返回`SocialComponent`。

使用的成功HTTP狀態代碼為：

* 2010年建立操作
* 200 for Update operations
* 204 for Delete operations

#### OperationException類{#operationexception-class}

如果請求無效或發生其他錯誤，例如內部錯誤、參數值錯誤、權限不當等，在執行操作時可拋出`OperationExcepton`。 `OperationException`由HTTP狀態代碼和錯誤消息組成，這些消息作為對`PostOperatoin`的響應返回給客戶端。

#### OperationService Class {#operationservice-class}

社交元件架構建議負責執行操作的商業邏輯不在`SocialOperation`類別中實作，而是委託給OSGi服務。 使用OSGi業務邏輯服務允許由`SocialOperation`端點所作的`SocialComponent`與其它代碼整合併應用不同的業務邏輯。

所有`OperationService`類都擴展`AbstractOperationService` ，允許附加擴展，這些擴展可連接到正在執行的操作中。 服務中的每個操作都由`SocialOperation`類表示。 通過調用方法，可在操作執行期間調用`OperationExtensions`類

* `performBeforeActions()`

   允許預檢／預處理和驗證
* `performAfterActions()`

   允許進一步修改資源或調用自定義事件、工作流等

#### OperationExtension類{#operationextension-class}

`OperationExtension` 類是可插入操作的自定義代碼片段，允許定制操作以滿足業務需要。元件的使用者可動態且遞增地新增功能至元件。 擴充／掛接模式可讓開發人員專注於擴充功能本身，而不需複製和覆寫整個作業和元件。

## 范常式式碼{#sample-code}

范常式式碼可在[Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud)儲存庫中使用。 搜尋前置詞為`aem-communities`或`aem-scf`的專案。

## 最佳作法 {#best-practices}

檢視[編碼准則](code-guide.md)一節，以取得AEM Communities開發人員的各種編碼准則和最佳實務。

如需有關訪問用戶生成內容的資訊，請參閱[UGC](srp.md)的儲存資源提供程式(SRP)。

| **[‹功能基本工具](essentials.md)** | **[用戶端自訂的‹](client-customize.md)** |
|---|---|
|  | **[SCF Handlepers ‡](handlebars-helpers.md)** |

