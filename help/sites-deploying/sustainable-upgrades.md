---
title: 可持續升級
seo-title: 可持續升級
description: 瞭解AEM 6.4的可持續升級。
seo-description: 瞭解AEM 6.4的可持續升級。
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# 可持續升級{#sustainable-upgrades}

## 自訂框架{#customization-framework}

### 體系結構（功能／基礎結構／內容／應用程式）{#architecture-functional-infrastructure-content-application}

「自訂架構」功能可協助減少不方便升級的程式碼（例如APIS）或內容（例如覆蓋）不可擴充區域的違規。

定制框架有兩個元件：**API Surface**&#x200B;和&#x200B;**內容分類**。

#### API Surface {#api-surface}

在舊版AEM中，許多API都是透過Uber Jar公開的。 其中有些API並非客戶所要使用，但是會跨套件提供支援AEM功能。 未來，Java API將標示為「公開」或「私用」，以向客戶指出哪些API在升級中可安全使用。 其他具體內容包括：

* 標示為`Public`的Java API可供自訂實作組合使用和參考。

* Public API將向後相容相容軟體包的安裝。
* 相容性軟體包將包含相容性Uber JAR以確保向後相容性
* 標示為`Private`的Java API僅供AEM內部組合使用，不應供自訂組合使用。

>[!NOTE]
>
>`Private`和`Public`的概念不應與Java的公共和私有類概念混淆。

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### 內容分類{#content-classifications}

AEM長期以來都採用覆蓋和Sling Resource Merger的原則，讓客戶可擴充和自訂AEM功能。 為AEM主控台和UI提供動力的預先定義功能會儲存在&#x200B;**/libs**&#x200B;中。 客戶絕不得修改&#x200B;**/libs**&#x200B;下方的任何內容，但可在&#x200B;**/apps**&#x200B;下方新增其他內容，以覆蓋並延伸&#x200B;**/libs**&#x200B;中定義的功能（如需詳細資訊，請參閱使用覆蓋進行開發）。 當將AEM升級為&#x200B;**/libs**&#x200B;中的內容時，仍然會造成許多問題，這些問題可能會變更，導致覆蓋函式以非預期的方式中斷。 客戶也可以透過`sling:resourceSuperType`的繼承來擴充AEM元件，或直接透過sling:resourceType參考&#x200B;**/libs**&#x200B;中的元件。 類似的升級問題可能與參考和覆寫使用案例有關。

為了讓客戶更安全、更輕鬆地瞭解&#x200B;**/libs**&#x200B;的哪些區域安全使用並覆蓋&#x200B;**/libs**&#x200B;中的內容，已使用下列混音分類：

* **公用(granite:PublicArea)** -將節點定義為公用，以便其可以覆蓋、繼承( `sling:resourceSuperType`)或直接使用( `sling:resourceType`)。在/libs下標示為Public的節點可以通過添加相容性包進行安全升級。 一般而言，客戶只應使用標示為「公用」的節點。

* **摘要(granite:AbstractArea)** -將節點定義為抽象。節點可以覆蓋或繼承(`sling:resourceSupertype`)，但不能直接使用(`sling:resourceType`)。

* **Final(granite:FinalArea)** -將節點定義為final。分類為最終的理想節點不應重疊或繼承。 最終節點可以直接通過`sling:resourceType`使用。 預設情況下，最終節點下的子節點被視為內部節點。

* ***內部(granite:InternalArea)*** *- *將節點定義為內部。理想情況下，分類為內部的節點不應重疊、繼承或直接使用。 這些節點僅適用於AEM的內部功能

* **無注釋** -節點根據樹層次繼承分類。預設情況下， / root為Public。 **父節點被分類為「內部」或「最終」，節點也被視為「內部」。**

>[!NOTE]
>
>這些原則僅會針對Sling搜尋路徑架構強制執行。 **/libs**&#x200B;的其他區域（如用戶端程式庫）可標示為`Internal`，但仍可與標準clientlib內含項目搭配使用。 在這些情況下，客戶必須繼續遵守內部分類。

#### CRXDE Lite內容類型指示器{#crxde-lite-content-type-indicators}

在CRXDE Lite中套用的Mixin會顯示標示為`INTERNAL`的內容節點和樹狀結構變灰。 對於`FINAL`，只有圖示會變灰。 這些節點的子節點也將顯示為灰色。 這兩種情況下都會停用「覆蓋節點」功能。

**公共**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**最終**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**內部**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Content Health Check**

>[!NOTE]
>
>自AEM 6.5起，Adobe建議使用Pattern Detector來偵測內容存取違規。 模式檢測器報告更加詳細，檢測問題更多，降低誤報率。
>
>如需詳細資訊，請參閱[使用模式偵測器評估升級複雜性](/help/sites-deploying/pattern-detector.md)。

AEM 6.5將隨附健康狀況檢查，以警告客戶重疊或參考的內容使用方式與內容分類不符。

The** Sling/Granite Content Access Check**是新的健康狀態檢查，可監控儲存庫，以檢視客戶程式碼是否正在不當存取AEM中的受保護節點。

這會掃描&#x200B;**/apps**，通常需要數秒才能完成。

要訪問此新的運行狀況檢查，您需要執行以下操作：

1. 從「AEM首頁畫面」，導覽至「**工具>作業>健康報表」**
1. 按一下&#x200B;**Sling/Granite Content Access Check**，如下所示：

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

掃描完成後，將顯示警告清單，通知正被不當引用的受保護節點的最終用戶：

![screenshot-2018-2-5healthreports](assets/screenshot-2018-2-5healthreports.png)

修正違規後，將返回綠色狀態：

![screenshot-2018-2-5healthreports-violations](assets/screenshot-2018-2-5healthreports-violations.png)

The health check displays information by a background services collected that hat an an overlay or resource type is used or all Sling search paths. 如果內容混音使用不當，則會報告違規。
