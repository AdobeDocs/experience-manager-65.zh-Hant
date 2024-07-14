---
title: 伺服器端自訂
description: 瞭解Adobe Experience Manager Communities中伺服器端自訂的方式。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# 伺服器端自訂 {#server-side-customization}

| **[⇐ Feature Essentials](essentials.md)** | **[使用者端自訂⇒](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars協助程式⇒](handlebars-helpers.md)** |

## Java™ API {#java-apis}

>[!NOTE]
>
>從一個主要版本升級至下一個主要版本時，Communities API的套件位置可能會有所變更。

### SocialComponent介面 {#socialcomponent-interface}

SocialComponents是POJO，代表AEM Communities功能的資源。 理想情況下，每個SocialComponent代表特定的resourceType，其中包含公開的GETters，可提供資料給使用者端，以便準確表示資源。 所有業務和檢視邏輯都會封裝在SocialComponent中，包括網站訪客的工作階段資訊（如有必要）。

介面定義了一組代表資源所需的基本GETter。 重要的是，介面會規定Map&lt;String， Object> getAsMap()和String toJSONString()方法，這些方法對於呈現Handlebars範本及公開資源的GETJSON端點很有必要。

所有SocialComponent類別都必須實作介面`com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent介面 {#socialcollectioncomponent-interface}

SocialCollectionComponent介面可擴充SocialComponent介面，以便更妥善地表示屬於其他資源集合的資源。

所有SocialCollectionComponent類別都必須實作介面com.adobe.cq.social.scf.SocialCollectionComponent

### SocialComponentFactory介面 {#socialcomponentfactory-interface}

SocialComponentFactory （工廠）會向架構註冊SocialComponent。 工廠提供一種方法，讓架構知道指定的resourceType有哪些SocialComponents可用，以及識別多個SocialComponents時它們的優先順序排名。

SocialComponentFactory負責建立所選SocialComponent的執行個體，以便使用DI實務從工廠插入SocialComponent所需的所有相依性。

SocialComponentFactory是OSGi服務，可存取其他OSGi服務，這些服務可透過建構函式傳遞給SocialComponent。

所有SocialComponentFactory類別都必須實作介面`com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority()方法的實作應傳回getResourceType()傳回之指定resourceType所用工廠的最高值。

### SocialComponentFactoryManager介面 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager （管理員）會管理在架構中註冊的所有SocialComponents，並負責選取要用於指定資源(resourceType)的SocialComponentFactory。 如果沒有為特定resourceType登入工廠，則管理員會傳回指定資源具有最接近超級型別的工廠。

SocialComponentFactoryManager是一項OSGi服務，可存取其他OSGi服務，這些服務可透過建構函式傳遞給SocialComponent。

透過叫用`com.adobe.cq.social.scf.SocialComponentFactoryManager`取得OSGi服務的控制代碼

### HTTP API -POST要求 {#http-api-post-requests}

#### PostOperation類別 {#postoperation-class}

HTTP APIPOST端點是由實作`SlingPostOperation`介面（封裝`org.apache.sling.servlets.post`）定義的PostOperation類別。

`PostOperation`端點實作將`sling.post.operation`設定為作業回應的值。 所有POST請求的：operation引數都設為該值，這些請求都會委派給此實作類別。

`PostOperation`會叫用`SocialOperation`，以執行作業所需的動作。

`PostOperation`從`SocialOperation`接收結果，並傳回適當的回應給使用者端。

#### SocialOperation類別 {#socialoperation-class}

每個`SocialOperation`端點都會擴充AbstractSocialOperation類別並覆寫方法`performOperation()`。 此方法會執行完成作業所需的所有動作，並傳回`SocialOperationResult`或擲回`OperationException`。 在這種情況下，會傳回包含訊息的HTTP錯誤狀態（如果可用），以取代一般JSON回應或成功HTTP狀態代碼。

延伸`AbstractSocialOperation`可重複使用`SocialComponents`來傳送JSON回應。

#### SocialOperationResult類別 {#socialoperationresult-class}

`SocialOperationResult`類別是以`SocialOperation`的結果傳回，並由`SocialComponent`、HTTP狀態碼和HTTP狀態訊息組成。

`SocialComponent`代表受作業影響的資源。

對於Create作業，`SocialOperationResult`中包含的`SocialComponent`代表已建立的資源，而對於Update作業，它代表作業變更的資源。 刪除作業未傳回任何`SocialComponent`。

使用的成功HTTP狀態代碼為：

* 201用於建立操作
* 200表示更新作業
* 204 （刪除作業）

#### OperationException類別 {#operationexception-class}

如果要求無效或發生其他錯誤，執行作業時會擲回`OperationExcepton`。 例如，內部錯誤、引數值錯誤或不適當的許可權。 `OperationException`由HTTP狀態碼和錯誤訊息組成，這些會作為對`PostOperatoin`的回應傳回給使用者端。

#### OperationService類別 {#operationservice-class}

社交元件架構建議不要在`SocialOperation`類別內實作負責執行作業的商業邏輯，而是委派給OSGi服務。 將OSGi服務用於商業邏輯可讓`SocialOperation`端點執行的`SocialComponent`與其他程式碼整合，並套用不同的商業邏輯。

所有`OperationService`類別都會延伸`AbstractOperationService`，允許可連結至正在執行之作業的其他延伸。 服務中的每個作業都由`SocialOperation`類別表示。 可在作業執行期間呼叫方法，以叫用`OperationExtensions`類別

* `performBeforeActions()`

  允許預先檢查/前置處理和驗證
* `performAfterActions()`

  允許進一步編輯資源或叫用自訂事件、工作流程等。

#### OperationExtension類別 {#operationextension-class}

`OperationExtension`類別是可插入作業的自訂程式碼片段，允許自訂作業以符合業務需求。 元件的取用者可以動態地並遞增方式為元件新增功能。 擴充功能/掛接模式可讓開發人員專注於擴充功能本身，且無須複製及覆寫整個作業和元件。

## 程式碼範例 {#sample-code}

範常式式碼可在[Adobe Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud)存放庫中取得。 搜尋帶有`aem-communities`或`aem-scf`首碼的專案。

## 最佳做法 {#best-practices}

檢視[編碼准則](code-guide.md)區段，瞭解AEM Communities開發人員的各種編碼准則與最佳作法。

另請參閱UGC](srp.md)的[儲存資源提供者(SRP)，瞭解如何存取使用者產生的內容。

| **[⇐ Feature Essentials](essentials.md)** | **[使用者端自訂⇒](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars協助程式⇒](handlebars-helpers.md)** |
