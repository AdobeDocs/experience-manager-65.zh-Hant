---
title: MSM最佳實踐
description: 查找由Adobe工程和咨詢團隊編製的最佳做法，以幫助多站點管理AEM器啟動和運行。
topic-tags: site-features, best-practices
feature: Multi Site Manager
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: c6ccd204dbd514d6195424aff495bc38f1f31bce
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 0%

---

# MSM最佳實踐{#msm-best-practices}

## 一般 {#general}

MSM是一個可配置的框架，用於自動化內容部署。 實施通常涉及網站的主要部分，並跨組織和地理區域。 因此，強烈建議您像規劃網站一樣仔細規劃MSM實施：

* 小心 **規劃結構和內容流** 開始實施。
* **將即時副本的數量保持在最小。** 處理即時拷貝是一項資源密集型任務。 系統中存在的即時拷貝越多，效能就會受到影響：從處理內部即時拷貝索引，到UI操作（如在「站點管理參考」欄中顯示即時拷貝關係）。 最佳做法是建立站點或站點分支的即時拷貝，其中即時拷貝關係繼承到站點或分支中的頁面。 當整個結構可以製作為即時副本時，請避免為站點或分支中的頁面建立單個即時副本。
* **盡量定製，但盡可能少。** 雖然MSM支援高度定制（例如部署配置），但通常，網站效能、可靠性和可升級性的最佳做法是最大限度地減少定制。
* 建立 **治理** 及早建模，並據此培訓用戶，確保成功。 從治理角度來看，最佳做法是 **盡量減少本地內容製作者的權威** 將內容分配/連接到其他本地用戶及其各自的即時拷貝。 這是因為未管理的、鏈式的繼承可以顯著增加MSM結構的複雜性並損害其效能和可靠性。

* 一旦您的結構、內容流、自動化和治理制定了計畫 —  **原型並徹底test系統**，然後開始即時實施。
* 記住 **Adobe咨詢和領先的系統整合商** 擁有與MSM一起規劃和實施內容自動化的豐富經驗，因此他們可以幫助您開始實施MSM項目，並幫助您完成整個實施過程。

>[!NOTE]
>
>有關與MSM合作的進一步資訊，請參閱知識文庫文章：
>
>* [MSM問題故障排除和常見問題](troubleshoot-msm.md)
>


>[!NOTE]
>
>您還可以使用 [參考元件](/help/sites-authoring/default-components-foundation.md#reference) 重新使用單個頁面或段落。 但請記住：
>
>* MSM更靈活，允許對同步的內容和時間進行細粒度控制。
>* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 現在推薦使用基礎元件。
>


## 即時拷貝源和藍圖配置 {#live-copy-sources-and-blueprint-configurations}

請記住，可以使用 [常規頁面](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 或 [藍圖配置](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)。 這兩個都是有效的使用案例。

使用藍圖配置的額外好處是：

* 允許作者使用 **推廣** 中的選項 — 將修改推送到從此藍圖繼承的活動副本。
* 允許作者使用 **建立站點**;這允許用戶輕鬆選擇語言並配置即時副本的結構。
* 為與藍圖有關的即時副本定義預設的部署配置。

如果未引用藍圖配置，則只能從即時副本本身啟動部署，實際上是從源中提取內容。

建立帶即時拷貝的新站點時，建立藍圖配置是有利的，可確保完整MSM功能集的可用性。

>[注意!]
>
> 請注意，「權限」頁籤中的CUG無法從「藍圖」中展開為「即時副本」。 配置Live Copy時，請圍繞此進行規劃。

## 元件和容器同步 {#components-and-container-synchronization}

通常，MSM中關於元件同步的展示規則是：

* 已推出元件，以同步藍圖中包含的所有資源。
* 容器僅同步當前資源。

這意味著元件被視為一個集合，在部署中，元件本身及其所有子代都被藍圖中的元件所取代。 這意味著如果資源在本地添加到此元件中，將丟失到部署時藍圖的內容中。

為了支援元件的嵌套，以便在部署中維護本地添加的元件，必須將元件聲明為容器。 例如，預設parsys聲明為容器，以便它支援本地添加的內容。

>[!NOTE]
>
>添加屬性 `cq:isContainer` 將其指定為容器。

## 建立網站 {#create-site}

請注意，AEM建立即時副本的主要方法有兩種：

* 當 [建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   這可以視為更一般的方法，允許您從任何頁面建立即時副本。 即時副本的內容結構與源完全匹配。

* 當 [建立站點](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   這是一種更為專業的方法，主要用於建立具有多語言結構的網站。

以下是建立站點時要注意的幾個注意事項：

* 要建立新站點，您需要 [藍圖配置](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations)。
* 要允許選擇要在新站點中建立的語言路徑，藍圖（源）中必須存在相應的語言根。
* 一次 [新網站已建立為即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (使用 **建立**，則 **站點**)，此即時拷貝的前兩個級別是 *淺*。 頁面的子級不屬於即時關係，但如果找到與觸發器匹配的即時關係，則仍會下拉展開。

   它有助於避免：

   * 手動在藍圖中添加語言（在第一級以下）
   * 手動添加語言根目錄下的內容，
   * 不會導致在推廣時自動將新內容傳送到即時拷貝。

## MSM和多語言網站 {#msm-and-multilingual-websites}

MSM可通過兩種方式協助建立多語言網站：

* 建立語言母版時。

   * 而MSM本身 **不提供內容翻譯**，它可與第三方翻譯連接器整合。 請注意：

      * MSM允許您在頁面和/或元件級別取消繼承。 這有助於防止在下次部署時覆蓋已翻譯的內容（從即時拷貝，以及藍圖中尚未翻譯的內容）。
      * 某些第三方翻譯連接器可自動管理MSM遺產。

         有關詳細資訊，請咨詢翻譯服務提供商。

      * 建立和翻譯語言母版的另一種方法是將語言副本AEM與現成翻譯整合框架結合使用。

* 從語言母版中推出內容時。

   * 例如，從法語母版到特定國家的網站，如法國/法語、加拿大/法語、瑞士/法語。

有關詳細資訊，請參閱 [翻譯多語言站點的內容](/help/sites-administering/translation.md) 和 [翻譯最佳做法](/help/sites-administering/tc-bp.md)。

## 結構更改和展開 {#structure-changes-and-rollouts}

藍圖/源樹中對內容結構的修改在即時副本中反映不同。 這取決於修改類型：

* **建立** 藍圖中的新頁面將導致在使用標準部署配置進行部署後以即時副本建立相應的頁面。

* **刪除** 藍圖中的頁面將導致在使用標準部署配置進行部署後從即時副本中刪除相應的頁面。

* **移動** 藍圖中的頁面 **不** 在使用標準部署配置進行部署後，將相應的頁面移動到即時副本中：

   * 此行為的原因是頁面移動隱式包含頁面刪除。 這可能會導致發佈時出現意外行為，因為刪除作者上的頁面會自動在發佈時停用相應內容。 這也可對相關項目（如連結、書籤和其他）產生連鎖效應。
   * 更新各個即時拷貝頁面中的內容繼承以反映其源在藍圖中的新位置。
   * 要充分實現從藍圖到即時拷貝的頁面遷移，請考慮以下最佳做法：

>[!NOTE]
>
>這隻適用於 [On Roult觸發器](/help/sites-administering/msm-sync.md#rollout-triggers)。

* 建立自定義部署配置：

   * 此新配置必須包括操作：

      `PageMoveAction`

      請勿將此配置添加其他操作。

* 定位新配置：

   * 要完全展開頁面移動，同時刪除即時副本中舊位置的相應頁面：

      * 在標準部署配置之前定位新建立的配置。

         標準部署配置將負責刪除其舊位置中的頁面。
   * 在將各頁保留在其舊位置的即時副本中（實質上是複製內容）時，滾動頁面移動：

      * 在標準部署配置後定位新建立的配置。

         這將確保即時副本中未刪除任何內容，也不會從發佈中停用。


## 自定義部署 {#customizing-rollouts}

MSM部署配置可高度定制。 您應該知道，自動實施可能會產生深遠的影響。 作為最佳做法，您應該 *非常* 例如，以前要小心：

* 自動實施；例如， [onModify觸發器](#onmodify)。
* 自定義 [節點類型/屬性](#node-types-properties)。
* 啟動後續工作流，
* 和/或激活內容，作為部署的一部分。

### 修改 {#onmodify}

使用 [調用觸發](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify` 您應考慮：

* 自動執行部署 `onModify` 觸發器可能會對創作效能產生負面影響，因為它們在 *每* 頁面修改。

* 展出結果可能與預期結果不同：

   * 不能指定結果修改事件的順序。
   * 基於事件的體系結構無法保證傳遞到部署管理器的事件的順序。

* 如果同一資源的併發更新發生，則使用這種部署配置可能會導致提交衝突。

因此，建議您 *僅* 使用 `onModify` 觸發器。

### 節點類型/屬性 {#node-types-properties}

記住：

* 除了自定義推廣操作外，MSM還允許您自定義正在推廣的節點屬性。 的 [MSM OSGi配置允許您排除節點類型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) 從源複製到即時副本。

## 更多資訊 {#further-information}

本頁及以下各頁介紹相關問題：

* [建立和同步即時拷貝](/help/sites-administering/msm-livecopy.md)
* [Live Copy概述控制台](/help/sites-administering/msm-livecopy-overview.md)
* [配置即時拷貝同步](/help/sites-administering/msm-sync.md)
* [MSM部署衝突](/help/sites-administering/msm-rollout-conflicts.md)
