---
title: MSM最佳實務
seo-title: MSM最佳實務
description: 尋找由Adobe工程和諮詢團隊編譯的最佳實務，以協助您快速上手使用AEM Multi Site Manager。
seo-description: 尋找由Adobe工程和諮詢團隊編譯的最佳實務，以協助您快速上手使用AEM Multi Site Manager。
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# MSM最佳實務{#msm-best-practices}

## 一般 {#general}

MSM是可設定的架構，可自動化內容部署。 實作通常涉及網站的主要部分，而且涵蓋組織和地域。 因此，強烈建議您像規劃網站一樣，謹慎規劃MSM實作：

* 開始 **實施前，請仔細規劃結構** 和內容流程。
* **視需要自訂，但盡可能少。** 雖然MSM支援高度自訂（例如展出組態），但是您網站的效能、可靠性和可升級性的最佳實務是將自訂降至最低。
* 及早建立 **治理模式** ，並據此培訓使用者，以確保成功。 從治理角度來看，最佳做法是將本機內 **容製作者分配／連接內容給其他本機使用者及其個別即時副本的權限降至最低** 。 這是因為無管理、鏈式繼承可以顯著增加MSM結構的複雜性，並損害其效能和可靠性。

* 一旦您的結構、內容流程、自動化和治理有了計畫， **就可先建立原型並徹底測試您的系統**，然後再開始即時實作。
* 請記住， **** Adobe Consulting和頂尖的系統整合商有與MSM一起深入規劃和實施內容自動化的經驗，因此，他們可協助您開始進行MSM專案，並在整個實作過程中都能協助您。

>[!NOTE]
>
>有關與MSM合作的進一步資訊，請參閱知識庫文章：
>
>* [MSM常見問答集](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [MSM問題故障排除](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)
>



>[!NOTE]
>
>您也可以使用「參 [考」元件](/help/sites-authoring/default-components-foundation.md#reference) ，以重複使用單一頁面或段落。 但請記住：
>
>* MSM更有彈性，可精確控制同步哪些內容及時間。
>* [現在建議](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) ，核心元件比基礎元件更重要。
>



## 即時複製來源和Blueprint設定 {#live-copy-sources-and-blueprint-configurations}

請記住，即時副本可使用一般頁面 [或藍圖](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 設 [定建立](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)。 這兩種都是有效的使用案例。

使用Blueprint設定的額外好處是：

* 允許作者在藍圖上使 **用** 「轉出」選項——將修改（明確）推送至繼承自此藍圖的即時副本。
* 允許作者使用「建 **立網站」**;這可讓使用者輕鬆選擇語言並設定即時副本的結構。
* 為與藍圖有關的即時副本定義預設轉出設定。

如果未參考藍圖設定，則只能從即時副本本身啟動推播，實際上是從來源提取內容。

使用即時副本建立新網站時，建立藍圖組態有利於確保完整MSM功能集的可用性。

## 元件與容器同步 {#components-and-container-synchronization}

通常，MSM中關於元件同步的轉出規則是：

* 已推出元件，可同步藍圖中包含的任何資源。
* 容器僅同步目前的資源。

這表示元件會被視為總結，在推出時，元件本身及其所有子系會以藍圖中的元件取代。 這表示，如果資源在本機新增至此類元件，則在開始時會遺失在藍圖的內容中。

若要支援元件巢狀，以便在轉出中維護本機新增的元件，元件必須宣告為容器。 例如，預設parsys會宣告為容器，以便支援本機新增的內容。

>[!NOTE]
>
>將屬性新 `cq:isContainer` 增至元件，將其指定為容器。

## 建立網站 {#create-site}

請注意，AEM有兩種主要的建立即時副本的方法：

* 建立 [即時副本時](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   這可視為更一般的方法，讓您從任何頁面建立即時副本。 即時副本的內容結構完全符合來源。

* 建立 [網站時](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   這是更專業的方式，主要用於建立具有多語言結構的網站。

以下是建立網站時需注意的幾項考量：

* 若要建立新網站，您需要藍圖 [設定](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations)。
* 若要允許選擇語言路徑以在新網站中建立，對應的語言根目錄必須存在於Blueprint（來源）中。
* 將新網 [站建立為即時副本後](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (使用「建立」，然後使用「網站 ****」)，此即時副本的前兩個層級為 ******&#x200B;淺層副本。 頁面的子系不屬於即時關係，但如果找到符合觸發條件的即時關係，則推出仍會下降。

   它有助於避免：

   * 在Blueprint中手動新增語言（在第一層下）
   * 手動將內容直接新增至語言根目錄下方，
   * 不會導致在轉出時自動將新內容傳送至即時副本。

## MSM與多語言網站 {#msm-and-multilingual-websites}

MSM可協助建立多語言網站，方式有兩種：

* 建立語言主版時。

   * 雖然MSM本身 **不提供內容轉譯**，但可與協力廠商轉譯連接器整合。 請注意：

      * MSM允許您在頁面和／或元件級別取消繼承。 這有助於防止在下次推出時覆寫已翻譯的內容（來自即時副本，含來自藍圖的尚未翻譯內容）。
      * 某些協力廠商轉譯連接器會自動管理MSM繼承。

         請洽詢您的翻譯服務供應商以取得更多資訊。

      * 建立和翻譯語言主版的另一種方式是搭配AEM的現成可用的翻譯整合架構使用語言副本。

* 從語言大師版推出內容時。

   * 例如，從法文主版到國家特定網站，例如法文／法文、加拿大／法文、瑞士／法文。

如需詳細資訊，請 [參閱多語言網站翻譯內容](/help/sites-administering/translation.md) ，以 [及翻譯最佳實務](/help/sites-administering/tc-bp.md)。

## 結構變更與推出 {#structure-changes-and-rollouts}

藍圖／來源樹狀結構中的內容結構修改在即時副本中的反映不同。 這取決於修改類型：

* **在Blueprint中** ，建立新頁面將導致在使用標準轉出設定轉出後，在即時副本中建立對應頁面。

* **在Blueprint中** ，刪除頁面將導致在使用標準轉出設定轉出後，從即時副本中刪除對應頁面。

* **在藍圖中移** 動頁面 **** ，在使用標準轉出設定轉出後，不會導致對應頁面移入即時副本：

   * 此行為的原因是頁面移動隱含地包含頁面刪除。 這可能會導致發佈時發生非預期的行為，因為作者刪除頁面會自動停用發佈時的對應內容。 這也可能會對相關項目（例如連結、書籤等）產生連鎖效果。
   * 更新個別即時副本頁面中的內容繼承，以反映其來源在藍圖中的新位置。
   * 要完全實現從藍圖到即時拷貝的頁面，請考慮以下最佳做法：

>[!NOTE]
>
>這隻適用於「轉出時」 [觸發器](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers)。

* 建立自訂轉出設定：

   * 此新設定必須包含動作：

      `PageMoveAction`

      請勿將其他動作新增至此設定。

* 定位新配置：

   * 若要完全展開頁面移動，同時刪除即時副本中舊位置的各個頁面：

      * 在標準轉出設定之前，先定位新建立的設定。

         標準的轉出設定將負責刪除其舊位置的頁面。
   * 若要展開頁面移動，同時將各頁面保留在即時副本的舊位置（實質上是複製內容）:

      * 在標準轉出設定後，放置新建立的設定。

         如此可確保即時副本中不會刪除任何內容，或是從發佈中停用。


## 自訂推展 {#customizing-rollouts}

MSM首次展示配置具有高度可定製性。 您應該注意到，自動化推展可能產生深遠影響。 作為最佳實務，您應在之前 *仔細* 規劃，例如：

* 自動推展；例如，使用 [onModify觸發器](#onmodify),
* 自定義 [節點類型／屬性](#node-types-properties),
* 啟動後續工作流程，
* 和／或啟動內容做為推展的一部分。

### onModify {#onmodify}

使用轉出觸 [發器時](/help/sites-administering/msm-sync.md#rollout-triggers)`onModify` ，您應考慮：

* 使用觸發器自 `onModify` 動推出可能會對製作效能造成負面影響，因為它們會在每次修改頁面後觸發 *推出* 。

* 首次推出的結果可能與預期的不同：

   * 您無法指定產生的修改事件的順序。
   * 事件型架構無法保證傳遞至轉出管理員的事件順序。

* 如果同一資源發生併發更新，使用這種轉出配置可能會導致提交衝突。

因此，建議您僅在自動 *啟動*`onModify` 的優點超過任何潛在效能問題時使用觸發器。

### 節點類型／屬性 {#node-types-properties}

請記住：

* 除了自訂轉出動作，MSM還可讓您自訂正在轉出的節點屬性。 MSM [OSGi配置允許您排除節點類型](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) ，使其不從源複製到即時副本。

## 更多資訊 {#further-information}

本頁及下列各頁涵蓋相關問題：

* [建立和同步即時副本](/help/sites-administering/msm-livecopy.md)
* [即時副本概述主控台](/help/sites-administering/msm-livecopy-overview.md)
* [配置即時拷貝同步](/help/sites-administering/msm-sync.md)
* [MSM推出衝突](/help/sites-administering/msm-rollout-conflicts.md)

