---
title: MSM最佳實務
seo-title: MSM最佳實務
description: 尋找由Adobe工程和諮詢團隊編譯的最佳實務，協助您快速上手並執行AEM多網站管理員。
seo-description: 尋找由Adobe工程和諮詢團隊編譯的最佳實務，協助您快速上手並執行AEM多網站管理員。
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
feature: 多站點管理員
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 1%

---

# MSM最佳實務{#msm-best-practices}

## 一般 {#general}

MSM是可自動部署內容的可設定架構。 實作通常涉及網站的主要部分，並橫跨組織和地理區域。 因此，強烈建議您在規劃網站時，務必謹慎規劃MSM實作：

* 開始實作前，請務必小心&#x200B;**規劃結構和內容流**。
* **將即時副本的數量保持在最低。** 處理即時副本是一項耗用大量資源的任務。系統中的即時副本越多，對效能的影響就越大：從處理內部即時副本索引、從即時副本操作（例如轉出）到UI操作（例如在「網站管理員」參考邊欄中顯示即時副本關係）。 最佳實務是建立網站或網站分支的即時副本，其中即時副本關係繼承至網站或分支中的頁面。 當可將整個結構製作為即時副本時，請避免為網站或分支中的頁面建立個別的即時副本。
* **視需要自訂，但盡可能少。** 雖然MSM支援高度自訂（例如轉出設定），但針對網站效能、可靠性和可升級性，通常最佳實務是將自訂降至最低。
* 及早建立&#x200B;**governance**&#x200B;模型，並據此訓練使用者，以確保成功。 從治理角度來看，最佳做法是&#x200B;**最小化本地內容生成者擁有的將內容分配給其他本地用戶及其各自的即時副本/連接內容的權限。**&#x200B;這是因為不受管理、鏈式繼承可以顯著增加MSM結構的複雜性，並損害其效能和可靠性。

* 一旦您的結構有計畫，內容流程、自動化和控管 — **原型，並在開始即時實施之前徹底測試您的系統**。
* 請記住，**Adobe諮詢與領先的系統整合商**&#x200B;擁有透過MSM進行內容自動化規劃與實作的豐富經驗，因此可協助您開始使用MSM專案，以及完成整個實作。

>[!NOTE]
>
>有關與MSM合作的進一步資訊，請參閱知識庫文章：
>
>* [MSM常見問題集](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [疑難排解MSM問題](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>您也可以使用[參考元件](/help/sites-authoring/default-components-foundation.md#reference)來重複使用單一頁面或段落。 但請記住：
>
>* MSM更靈活，可對同步的內容和時間進行微調控制。
>* [現在](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 建議將核心元件置於基礎元件之上。

>



## 即時副本來源和Blueprint設定{#live-copy-sources-and-blueprint-configurations}

請記住，可使用[常規頁面](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)或[Blueprint設定](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)來建立即時副本。 兩者皆為有效的使用案例。

使用Blueprint配置的額外好處是：

* 允許作者在Blueprint上使用&#x200B;**轉出**&#x200B;選項 — 將修改（明確）推送至繼承自此Blueprint的Live Copy。
* 允許作者使用&#x200B;**建立網站**;這可讓使用者輕鬆選取語言並設定即時副本的結構。
* 為與Blueprint有關係的Live Copy定義預設轉出設定。

如果未參考Blueprint設定，則只能從即時副本本身啟動轉出，實際上是從來源提取內容。

使用Live Copy建立新網站時，建立Blueprint設定是有利的，以確保完整MSM功能集的可用性。

>[注意!]
>
> 請注意，「權限」頁簽中的CUG無法從Blueprint轉出到Live Copy。 設定Live Copy時，請針對此進行規劃。

## 元件和容器同步{#components-and-container-synchronization}

一般而言，MSM中關於元件同步的轉出規則為：

* 系統會推出元件，同步Blueprint中包含的任何資源。
* 容器僅同步當前資源。

這表示元件被視為聚合，在轉出時，元件本身及其所有子代將被藍圖中的元件替換。 這表示如果資源在本機新增至此類元件，在轉出時將會遺失至Blueprint的內容。

若要支援元件巢狀，以便轉出時維護本機新增的元件，必須將元件宣告為容器。 例如，預設的parsys會宣告為容器，以支援本機新增的內容。

>[!NOTE]
>
>將屬性`cq:isContainer`新增至元件，以將其指定為容器。

## 建立網站 {#create-site}

請注意，AEM有兩種建立Live Copy的主要方法：

* 當[建立即時副本時](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   這可視為較通用的方法，可讓您從任何頁面建立即時副本。 即時副本的內容結構完全符合來源。

* 當[建立站點時](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   這是更專業的方法，主要用於以多語言結構建立網站。

建立網站時，請謹記以下幾點：

* 若要建立新網站，您需要[blueprint設定](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations)。
* 若要允許選取要在新網站中建立的語言路徑，對應的語言根必須存在於Blueprint（來源）中。
* 一旦將[新網站建立為即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)（使用&#x200B;**Create**，然後使用&#x200B;**Site**），此即時副本的前兩個層級為&#x200B;*shallow*。 頁面的子項不屬於即時關係，但如果找到符合觸發器的即時關係，則轉出仍會下降。

   有助於避免：

   * 在blueprint中手動新增語言（在第一層以下）
   * 手動新增語言根目錄正下方的內容，
   * 不會導致轉出時自動將此新內容傳送到即時副本。

## MSM和多語言網站{#msm-and-multilingual-websites}

MSM可以以兩種方式協助建立多語言網站：

* 建立語言主版時。

   * 雖然MSM本身&#x200B;**不提供內容翻譯**，但可與提供內容的第三方翻譯連接器整合。 請注意：

      * MSM可讓您取消頁面和/或元件層級的繼承。 這有助於防止下次轉出時覆寫已翻譯的內容（來自即時副本，而來自Blueprint的尚未翻譯內容）。
      * 某些第三方翻譯連接器會自動管理MSM繼承內容。

         請洽詢您的翻譯服務提供商以了解更多資訊。

      * 建立和翻譯語言主版的替代方法是結合AEM現成的翻譯整合架構使用語言副本。

* 從語言主版轉出內容時。

   * 例如，從法語母版到特定國家的網站，如法國/法語、加拿大/法語、瑞士/法語。

如需詳細資訊，請參閱[翻譯多語言網站的內容](/help/sites-administering/translation.md)和[翻譯最佳實務](/help/sites-administering/tc-bp.md)。

## 結構變更與轉出{#structure-changes-and-rollouts}

Blueprint/來源樹狀結構中對內容結構的修改在即時副本中的反映不同。 這取決於修改類型：

* **** 在Blueprint中建立新頁面後，透過標準轉出設定轉出後，會在Live Copy中建立對應的頁面。

* **** 使用標準轉出設定轉出後，Blueprint中的刪除頁面將導致從Live Copy中刪除對應的頁面。

* **** 使用標準轉出設定轉出 **** 後，在Blueprint中移動頁面不會導致對應頁面在Live Copy中移動：

   * 此行為的原因是頁面移動隱含地包含頁面刪除。 這可能會在發佈時導致非預期的行為，因為刪除作者上的頁面會自動在發佈時停用對應的內容。 這也可能對相關項目（例如連結、書籤等）產生連結效應。
   * 會更新個別即時副本頁面中的內容繼承，以反映其來源在Blueprint中的新位置。
   * 若要完全實現頁面從Blueprint移至Live Copy，請考慮下列最佳實務：

>[!NOTE]
>
>這隻適用於[轉出觸發器](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers)。

* 建立自訂轉出設定：

   * 此新設定必須包含動作：

      `PageMoveAction`

      請勿將其他動作新增至此設定。

* 定位新配置：

   * 若要完全轉出頁面移動，同時在即時副本的舊位置刪除個別頁面：

      * 在標準轉出設定之前放置新建立的設定。

         標準轉出設定會處理刪除其舊位置中的頁面。
   * 若要展開頁面移動，同時將個別頁面保留在即時副本的舊位置（基本上重複內容）:

      * 在標準轉出設定後，放置新建立的設定。

         這可確保即時副本中不會刪除任何內容，或從發佈停用。


## 自訂轉出{#customizing-rollouts}

MSM轉出設定可高度自訂。 請注意，自動轉出可能會產生深遠的後果。 最佳實務是，您應事先謹慎規劃&#x200B;*very*，例如：

* 自動轉出；例如，若使用[onModify觸發器](#onmodify),
* 自定義[節點類型/屬性](#node-types-properties),
* 啟動後續工作流，
* 和/或在轉出中啟用內容。

### onModify {#onmodify}

使用[轉出觸發器](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify`時，您應考量：

* 使用`onModify`觸發器自動轉出可能會對製作效能造成負面影響，因為它們會在&#x200B;*every*&#x200B;頁面修改後觸發轉出。

* 轉出結果可能與預期的不同，如下所示：

   * 您無法指定產生的修改事件的順序。
   * 事件型架構無法保證傳遞至轉出管理器的事件順序。

* 如果同一資源同時更新，使用此類轉出設定可能會導致提交衝突。

因此，如果自動轉出啟動的好處超過任何潛在的效能問題，建議您&#x200B;*僅*&#x200B;使用`onModify`觸發器。

### 節點類型/屬性{#node-types-properties}

請記住：

* 除了自訂轉出動作，MSM也可讓您自訂正在轉出的節點屬性。 [MSM OSGi設定可讓您排除節點類型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization)，以避免從來源複製到即時副本。

## 更多資訊 {#further-information}

本頁及以下各頁涵蓋相關問題：

* [建立和同步Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy概述主控台](/help/sites-administering/msm-livecopy-overview.md)
* [配置Live Copy同步](/help/sites-administering/msm-sync.md)
* [MSM轉出衝突](/help/sites-administering/msm-rollout-conflicts.md)
