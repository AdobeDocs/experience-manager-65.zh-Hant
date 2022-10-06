---
title: 永續升級
seo-title: Sustainable Upgrades
description: 了解AEM 6.4中的可持續升級。
seo-description: Learn about sustainable upgrades in AEM 6.4.
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# 永續升級{#sustainable-upgrades}

## 定制框架 {#customization-framework}

### 架構（功能/基礎架構/內容/應用程式）  {#architecture-functional-infrastructure-content-application}

自訂架構功能的設計目的，是協助減少升級不方便的程式碼（例如API）或內容（例如覆蓋）中不可擴充區域的違規情形。

自訂架構有兩個元件：the **API Surface** 和 **內容分類**.

#### API Surface {#api-surface}

在舊版AEM中，許多API是透過Uber Jar公開。 其中有些API並非打算供客戶使用，但是會接觸到不同套件的支援AEM功能。 日後，Java API將標示為「公用」或「私人」，以向客戶指出哪些API在升級時可安全使用。 其他具體內容包括：

* 標示為的Java API `Public` 可供自訂實作套件使用和參考。

* 公用API可回溯相容於相容性套件的安裝。
* 相容性套件將包含相容性Uber JAR，以確保回溯相容性
* 標示為的Java API `Private` 僅供AEM內部套件組合使用，不應供自訂套件組合使用。

>[!NOTE]
>
>概念 `Private` 和 `Public` 在這方面，不應將Java概念與公共和私有類混淆。

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### 內容分類 {#content-classifications}

AEM長期以來都採用覆蓋和Sling Resource Merger的原則，讓客戶可擴充及自訂AEM功能。 為AEM主控台和UI提供支援的預先定義功能會儲存在 **/libs**. 客戶絕不可修改下面的任何內容 **/libs** 但可以在 **/apps** 覆蓋並擴充中定義的功能 **/libs** （如需詳細資訊，請參閱使用覆蓋開發）。 這仍會在將AEM升級為 **/libs** 可能會變更，導致覆蓋圖函式以非預期的方式中斷。 客戶也可以透過繼承來擴充AEM元件 `sling:resourceSuperType`，或僅參考 **/libs** 直接透過sling:resourceType。 參考和覆寫使用案例可能會發生類似的升級問題。

為了讓客戶更安全、更輕鬆地了解 **/libs** 可安全地使用和覆蓋 **/libs** 已與下列混合項目分類：

* **公用(granite:PublicArea)**  — 將節點定義為公用節點，以便其可重疊、繼承( `sling:resourceSuperType`)或直接使用( `sling:resourceType`)。 標示為「公用」的/lib下的節點將可安全升級，並添加相容性包。 一般客戶應僅運用標示為「公用」的節點。

* **摘要(granite:AbstractArea)**  — 將節點定義為抽象。 節點可以重疊或繼承( `sling:resourceSupertype`)，但不得直接使用( `sling:resourceType`)。

* **最終(granite:FinalArea)**  — 將節點定義為最終節點。 最理想情況下分類為最終節點的節點不應重疊或繼承。 最終節點可直接透過 `sling:resourceType`. 根據預設，最終節點下的子節點視為內部節點。

* ***內部(Granite:InternalArea)*** *- *將節點定義為內部。 理想情況下，分類為內部的節點不應直接重疊、繼承或使用。 這些節點的用途僅止於AEM的內部功能

* **無注釋**  — 節點會根據樹狀結構繼承分類。 /根預設為公用。 **父節點分類為「內部」或「最終」，節點也視為「內部」。**

>[!NOTE]
>
>這些原則只會針對Sling搜尋路徑型機制強制執行。 其他領域 **/libs** 就像用戶端程式庫可能標示為 `Internal`，但仍可搭配標準clientlib包含使用。 在這些情況下，客戶必須繼續遵守內部分類。

#### CRXDE Lite內容類型指標 {#crxde-lite-content-type-indicators}

套用於CRXDE Lite的Mixin將顯示標示為的內容節點和樹 `INTERNAL` 顯示為灰色。 針對 `FINAL` 只有圖示會變灰。 這些節點的子節點也將顯示為灰色。 這兩種情況下，覆蓋節點功能都會停用。

**公共**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**最終**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**內部**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**內容健康狀況檢查**

>[!NOTE]
>
>自AEM 6.5起，Adobe建議使用模式偵測器來偵測內容存取違規。 模式偵測器報告更為詳細，偵測更多問題並降低誤判的機率。
>
>如需詳細資訊，請參閱 [使用模式檢測器評估升級複雜性](/help/sites-deploying/pattern-detector.md).

AEM 6.5隨附健康狀況檢查，當覆蓋或參考的內容的使用方式與內容分類不一致時，可提醒客戶。

** Sling/Granite內容存取檢查**是新的健全狀態檢查，可監控存放庫，查看客戶代碼是否未正確存取AEM中受保護的節點。

這會掃描 **/apps** 通常需要幾秒才能完成。

若要存取此新的健康狀況檢查，您必須執行下列動作：

1. 從AEM主畫面導覽至 **工具>操作>運行狀況報告**
1. 按一下 **Sling/Granite內容存取檢查** 如下所示：

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

掃描完成後，將顯示警告清單，通知正被錯誤引用的受保護節點的最終用戶：

![螢幕截圖 — 2018-2-5healthreports](assets/screenshot-2018-2-5healthreports.png)

修正違規後，將恢復綠色狀態：

![螢幕截圖 — 2018-2-5healthreports-violations](assets/screenshot-2018-2-5healthreports-violations.png)

運作狀況檢查會顯示背景服務所收集的資訊，當所有Sling搜尋路徑上都使用覆蓋或資源類型時，系統會以非同步方式檢查。 如果內容混合的使用不正確，則會報告違規。
