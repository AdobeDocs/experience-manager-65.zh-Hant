---
title: 永續升級
description: 瞭解Adobe Experience Manager 6.4中的可持續升級。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# 永續升級{#sustainable-upgrades}

## Customization Framework {#customization-framework}

### 架構（功能/基礎架構/內容/應用程式）  {#architecture-functional-infrastructure-content-application}

自訂架構功能的設計目的，是為了協助減少程式碼（如API）或內容（如覆蓋圖）不可擴充區域中不利於升級時的違規。

自訂架構有兩個元件： **API表面**&#x200B;和&#x200B;**內容分類**。

#### API表面 {#api-surface}

在舊版Adobe Experience Manager (AEM)中，許多API是透過Uber Jar公開。 其中部分API並非打算供客戶使用，而是公開支援跨套件組合的AEM功能。 日後，Java™ API會標示為「公用」或「私用」，以向客戶指出哪些API可在升級環境中安全使用。 其他細節包括：

* 標示為`Public`的Java™ API可供自訂實作套件組合使用和參考。

* 公用API會回溯相容性套件的安裝。
* 相容性套件包含相容性Uber JAR，以確保回溯相容性
* 標示為`Private`的Java™ API僅供AEM內部套件組合使用，而非自訂套件組合。

>[!NOTE]
>
>在此內容中，`Private`和`Public`的概念不應與公用和私用類別的Java™概念混淆。

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### 內容分類 {#content-classifications}

AEM一直使用覆蓋和Sling Resource Merger的原則來允許客戶擴充和自訂AEM功能。 支援AEM主控台和UI的預先定義功能儲存在&#x200B;**/libs**&#x200B;中。 客戶永遠無法修改&#x200B;**/libs**&#x200B;下的任何專案，但可以在&#x200B;**/apps**&#x200B;下新增其他內容，以覆蓋及擴充&#x200B;**/libs**&#x200B;中定義的功能（如需詳細資訊，請參閱使用覆蓋開發）。 升級AEM時，這仍會造成許多問題，因為&#x200B;**/libs**&#x200B;中的內容可能會變更，導致覆蓋功能以非預期的方式中斷。 客戶也可以透過`sling:resourceSuperType`的繼承擴充AEM元件，或直接透過sling：resourceType參考&#x200B;**/libs**&#x200B;中的元件。 在參考和覆寫使用案例時可能會發生類似的升級問題。

為了讓客戶更安全輕鬆地瞭解&#x200B;**/libs**&#x200B;的哪些區域可安全使用和覆蓋，**/libs**&#x200B;中的內容已使用下列mixin進行分類：

* **公用(granite：PublicArea)** — 將節點定義為公用，以便可以重疊、繼承(`sling:resourceSuperType`)或直接使用(`sling:resourceType`)。 標示為Public的/libs底下的節點可以安全升級，並加入相容性套件。 一般而言，客戶應僅使用標示為「公用」的節點。

* **抽象(granite：AbstractArea)** — 將節點定義為抽象。 節點可以覆蓋或繼承( `sling:resourceSupertype`)，但不能直接使用( `sling:resourceType`)。

* **最終(granite：FinalArea)** — 將節點定義為最終。 最好是分類為最終節點的節點不應覆蓋或繼承。 可透過`sling:resourceType`直接使用最終節點。 依預設，最終節點下的子節點會視為內部。

* ***內部(granite：InternalArea)*** *- *將節點定義為內部。 最好是分類為內部的節點不應重疊、繼承或直接使用。 這些節點僅適用於AEM的內部功能

* **沒有附註** — 節點會根據樹狀結構階層繼承分類。 /根預設為「公用」。 **父項分類為Internal或Final的節點也會被視為內部。**

>[!NOTE]
>
>這些政策僅針對Sling搜尋路徑型機制強制執行。 **/libs**&#x200B;的其他區域（例如使用者端資料庫）可能會標示為`Internal`，但仍可搭配標準clientlib包含專案使用。 在這些情況下，客戶必須繼續遵守內部分類。

#### CRXDE Lite內容型別指標 {#crxde-lite-content-type-indicators}

在CRXDE Lite中套用的Mixin會顯示標示為`INTERNAL`的內容節點和樹狀結構為灰色（灰色）。 對於`FINAL`，只有圖示是灰色。 這些節點的子項也會呈現暗灰色。 在這兩種情況下，覆蓋節點功能都會停用。

**公用**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**最終**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**內部**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**內容健康狀態檢查**

>[!NOTE]
>
>自AEM 6.5起，Adobe建議使用模式偵測器來偵測內容存取違規。 模式偵測器報告更詳細，可偵測更多問題，並降低誤報的可能性。
>
>如需詳細資訊，請參閱[使用模式偵測器評估升級複雜性](/help/sites-deploying/pattern-detector.md)。

AEM 6.5隨附健康情況檢查，如果以與內容分類不一致的方式使用覆蓋或參考的內容，則會提醒客戶。

** Sling/Granite Content Access Check**是新的健康狀態檢查，可監視存放庫，以檢視客戶程式碼是否不適當地存取AEM中受保護的節點。

這會掃描&#x200B;**/應用程式**，通常需要幾秒鐘才能完成。

若要存取這項新的健康情況檢查，請執行下列動作：

1. 從AEM首頁畫面，瀏覽至&#x200B;**工具>作業>健康狀態報告**
1. 按一下&#x200B;**Sling/Granite內容存取檢查**。

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

掃描完成後，會顯示警告清單，通知一般使用者受保護節點被不當參考：

![熒幕擷圖–2018-2-5healthreports](assets/screenshot-2018-2-5healthreports.png)

修正違規後，它會回到綠色狀態：

![熒幕擷圖–2018-2-5healthreports-violations](assets/screenshot-2018-2-5healthreports-violations.png)

健康狀態檢查會顯示背景服務收集的資訊，這些資訊會在所有Sling搜尋路徑上使用覆蓋或資源型別時進行非同步檢查。 如果內容Mixin使用不正確，它會報告違規。
