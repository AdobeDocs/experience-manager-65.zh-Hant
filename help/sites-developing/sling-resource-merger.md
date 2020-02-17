---
title: 在AEM中使用Sling Resource Merger
seo-title: 在AEM中使用Sling Resource Merger
description: Sling Resource Merger提供存取和合併資源的服務
seo-description: Sling Resource Merger提供存取和合併資源的服務
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 在AEM中使用Sling Resource Merger{#using-the-sling-resource-merger-in-aem}

## 目的 {#purpose}

Sling Resource Merger提供存取和合併資源的服務。 它為兩者提供差異（差異）機制：

* **[使用](/help/sites-developing/overlays.md)**已設定搜尋路徑[的資源覆蓋](/help/sites-developing/overlays.md#configuring-the-search-paths)。

* **覆寫** UI(`cq:dialog`)的元件對話方塊，使用資源類型階層(透過屬性 `sling:resourceSuperType`)。

透過Sling Resource Merger，覆蓋／覆寫資源及／或屬性會與原始資源／屬性合併：

* 自訂定義的內容優先順序高於原始定義的內容(亦即 *覆*&#x200B;蓋&#x200B;*或覆* 蓋)。

* 視需要， [在自訂中定義](#properties) ，指出如何使用合併自原稿的內容。

>[!CAUTION]
>
>Sling Resource Merger和相關方法僅能與 [Granite搭配使用](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。 這也表示它僅適用於標準的觸控式使用者介面；尤其是，以此方式定義的覆蓋僅適用於元件的觸控式對話框。
>
>其他區域的覆蓋／覆寫（包括可觸控元件或傳統UI的其他方面）包括將適當的節點和結構從原始節點複製到定義自訂的位置。

### AEM的目標 {#goals-for-aem}

在AEM中使用Sling Resource Merger的目標為：

* 確保未在中進行自定義更改 `/libs`。
* 減少複製的結構 `/libs`。

   使用Sling Resource Mergare時，不建議從中複製整個結構， `/libs` 因為這會導致在自訂中保留太多資訊(通常 `/apps`)。 在以任何方式升級系統時，重複資訊會不必要地增加問題的可能性。

>[!NOTE]
>
>覆蓋不依賴於搜索路徑，它們使用屬 `sling:resourceSuperType` 性建立連接。
>
>不過，覆寫通常在下面定義， `/apps`因為AEM的最佳實務是在下面定義自訂 `/apps`;這是因為，您不得變更下方的任何項 `/libs`目。

>[!CAUTION]
>
>您 ***不得*** 更改路徑中的任 `/libs` 何內容。
>
>這是因為下次升級 `/libs` 實例時會覆寫的內容（套用修補程式或功能套件時可能會覆寫）。
>
>配置和其他更改的建議方法為：
>
>1. 重新建立必要項目(如中所 `/libs`示) `/apps`
   >
   >
1. 在 `/apps`
>



### 屬性 {#properties}

資源合併提供以下屬性：

* `sling:hideProperties` ( `String` 或 `String[]`)

   指定要隱藏的屬性或屬性清單。

   萬用字元 `*` 會隱藏所有。

* `sling:hideResource` ( `Boolean`)

   指出資源是否應完全隱藏，包括其子項。

* `sling:hideChildren` ( `String` 或 `String[]`)

   包含要隱藏的子節點或子節點清單。 節點的屬性將被保留。

   萬用字元 `*` 會隱藏所有。

* `sling:orderBefore` ( `String`)

   包含當前節點應位於前面的同級節點的名稱。

這些屬性會影響覆蓋／覆寫(通常在 `/libs`中)使用對應／原始資源／屬性的 `/apps`方式。

### 建立結構 {#creating-the-structure}

若要建立覆蓋或覆寫，您需要在目標（通常）下重新建立具有等同結構的原始 `/apps`節點。 例如：

* 覆蓋

   * Sites控制台的導覽項目定義，如邊欄中所示，定義於：

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 若要覆蓋此節點，請建立下列節點：

      `/apps/cq/core/content/nav/sites`

      然後視需要更 `jcr:title` 新屬性。

* 覆寫

   * 「文本」(Texts)控制台的「啟用觸控」(touch-enabled)對話框的定義定義如下：

      `/libs/foundation/components/text/cq:dialog`

   * 要覆蓋此節點，請建立以下節點——例如：

      `/apps/the-project/components/text/cq:dialog`

要建立其中一種，只需重新建立骨架結構。 為了簡化結構的重構，所有中間節點都可以是 `nt:unstructured` 類型的(它們不需要反映原始節點類型；例如，在 `/libs`)中。

因此，在上述覆蓋範例中，需要下列節點：

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>當使用Sling Resource Merger（即處理標準、觸控式UI）時，不建議從中複製整個結構， `/libs` 因為這會造成太多資訊被保留 `/apps`。 這在系統以任何方式升級時都可能造成問題。

### 使用案例 {#use-cases}

這些功能與標準功能搭配使用，可讓您：

* **新增屬性**

   屬性不存在於定義中， `/libs` 但是覆蓋／覆寫中 `/apps` 是必要的。

   1. 在 `/apps`
   1. 在此節點「」上建立新屬性

* **重新定義屬性（非自動建立的屬性）**

   屬性在中定義 `/libs`，但覆蓋／覆寫中需要 `/apps` 新值。

   1. 在 `/apps`
   1. 在此節點上建立匹配屬性(在／下 `apps`)

      * 屬性會根據Sling Resource Resolver組態有優先順序。
      * 支援變更屬性類型。

         如果您使用與中使用的屬性類型不同的 `/libs`屬性類型，則會使用您定義的屬性類型。
   >[!NOTE]
   >
   >支援變更屬性類型。

* **重新定義自動建立的屬性**

   依預設，自動建立的屬性( `jcr:primaryType`例如)不受覆蓋／覆寫的約束，以確保目前位於下方的節 `/libs` 點類型。 若要套用覆蓋／覆寫，您必須在中重新建立節 `/apps`點，請明確隱藏屬性並重新定義：

   1. 在下面建立相 `/apps` 應的節點 `jcr:primaryType`
   1. 在該節 `sling:hideProperties` 點上建立屬性，其值設定為自動建立屬性；例如， `jcr:primaryType`

      此屬性(定義於 `/apps`下)現在會優先於定義於 `/libs`

* **重新定義節點及其子項**

   節點及其子項在中定義 `/libs`，但覆蓋／覆寫中需要 `/apps` 新的設定。

   1. 結合下列動作：

      1. 隱藏節點的子項（保留節點的屬性）
      1. 重新定義屬性／屬性

* **隱藏屬性**

   屬性在中定義， `/libs`但在覆蓋／覆寫中並 `/apps` 非必要項。

   1. 在 `/apps`
   1. 建立類型 `sling:hideProperties` 或的 `String` 屬性 `String[]`。 使用此選項可指定要隱藏／忽略的屬性。 也可使用萬用字元。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隱藏節點及其子項**

   節點及其子項在中定義， `/libs`但在覆蓋／覆蓋中並 `/apps` 非必要項。

   1. 在/apps下建立對應的節點
   1. 建立屬性 `sling:hideResource`

      * 類型: `Boolean`
      * 值: `true`

* **隱藏節點的子代（同時保留節點的屬性）**

   節點、其屬性及其子項在中定義 `/libs`。 覆蓋／覆蓋中需要節點及其屬 `/apps` 性，但覆蓋／覆蓋中不需要部分或全部 `/apps` 子節點。

   1. 在 `/apps`
   1. 建立屬性 `sling:hideChildren`:

      * 類型: `String[]`
      * 值：要隱藏／忽略的子節點清單(如中 `/libs`定義)
      通配符&amp;ast;可用於隱藏／忽略所有子節點。


* **重新排序節點**

   節點及其同級在中定義 `/libs`。 需要新位置，以便在覆蓋／覆蓋中重新建立節點，其中新位置是在參照中相應的同級節點時定義的 `/apps``/libs`。

   * 使用屬 `sling:orderBefore` 性：

      1. 在 `/apps`
      1. 建立屬性 `sling:orderBefore`:

         這指定了當前節點應在以 `/libs`下位置之前放置的節點（如中）:

         * 類型: `String`
         * 值: `<before-SiblingName>`

### 從您的程式碼叫用Sling Resource Merger {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger包含兩個自訂資源提供者——一個用於覆蓋，另一個用於覆蓋。 您可以使用裝載點，在程式碼中叫用這些項目：

>[!NOTE]
>
>訪問資源時，建議使用適當的裝載點。
>
>這可確保呼叫Sling Resource Merger並傳回完全合併的資源(減少需要從中複製的結構 `/libs`)。

* 覆蓋:

   * 目的：根據其搜索路徑合併資源
   * 裝載點： `/mnt/overlay`
   * usage: `mount point + relative path`
   * 範例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 覆寫：

   * 目的：根據超類型合併資源
   * 裝載點： `/mnt/overide`
   * usage: `mount point + absolute path`
   * 範例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 使用範例 {#example-of-usage}

其中包含一些範例：

* 覆蓋:

   * [自定義控制台](/help/sites-developing/customizing-consoles-touch.md)
   * [自訂頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md)

* 覆寫：

   * [設定您的頁面屬性](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)

