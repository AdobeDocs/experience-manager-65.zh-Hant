---
title: 在AEM中使用Sling Resource Merger
seo-title: Using the Sling Resource Merger in AEM
description: Sling Resource Merger提供存取和合併資源的服務
seo-description: The Sling Resource Merger provides services to access and merge resources
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
source-git-commit: c07fa148054b69b0da7bb402ef96a50d0895abfa
workflow-type: tm+mt
source-wordcount: '1254'
ht-degree: 1%

---

# 在AEM中使用Sling Resource Merger{#using-the-sling-resource-merger-in-aem}

## 用途 {#purpose}

Sling Resource Merger提供存取和合併資源的服務。 它為以下兩者提供差異（差異）機制：

* **[覆蓋](/help/sites-developing/overlays.md)** 使用 [配置的搜索路徑](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **覆寫** 觸控式UI的元件對話方塊(`cq:dialog`)，使用資源類型階層(透過屬性 `sling:resourceSuperType`)。

透過Sling Resource Merger，覆蓋/覆寫資源和/或屬性會與原始資源/屬性合併：

* 自訂定義的內容具有比原始定義更高的優先順序(即 *覆蓋* 或 *覆寫* )。

* 必要時， [屬性](#properties) 在自訂中定義，指出如何使用合併自原始內容的內容。

>[!CAUTION]
>
>Sling Resource Merger及相關方法只能搭配 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). 這也表示這僅適用於標準觸控式UI;尤其是，以此方式定義的覆寫僅適用於元件的觸控式對話方塊。
>
>其他區域的覆蓋/覆寫（包括觸控式元件或傳統UI的其他方面）涉及將適當的節點和結構從原始節點複製到將定義自訂的位置。

### AEM目標 {#goals-for-aem}

在AEM中使用Sling Resource Merger的目標為：

* 確保未在中進行自訂變更 `/libs`.
* 減少從複製的結構 `/libs`.

   使用Sling Resource Merger時，不建議從 `/libs` 因此，會導致在自訂中保留太多資訊(通常 `/apps`)。 以任何方式升級系統時，重複資訊會不必要地增加出現問題的機會。

>[!NOTE]
>
>覆寫不取決於搜尋路徑，而是使用屬性 `sling:resourceSuperType` 來建立連接。
>
>不過，覆寫通常定義於 `/apps`,AEM中的最佳實務是在 `/apps`;因為您不得變更下方的任何項目 `/libs`.

>[!CAUTION]
>
>您 ***必須*** 不會變更 `/libs` 路徑。
>
>這是因為 `/libs` 下次升級執行個體時即會覆寫（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
>
>設定和其他變更的建議方法為：
>
>1. 重新建立所需項目(亦即， `/libs`)底下 `/apps`
>
>1. 在內進行任何變更 `/apps`

>


### 屬性 {#properties}

資源合併提供以下屬性：

* `sling:hideProperties` ( `String` 或 `String[]`)

   指定要隱藏的屬性或屬性清單。

   萬用字元 `*` 全部隱藏。

* `sling:hideResource` ( `Boolean`)

   指出是否應完全隱藏資源，包括其子項。

* `sling:hideChildren` ( `String` 或 `String[]`)

   包含要隱藏的子節點或子節點清單。 節點的屬性將會保留。

   萬用字元 `*` 全部隱藏。

* `sling:orderBefore` ( `String`)

   包含當前節點應位於前面的同級節點的名稱。

這些屬性會影響對應/原始資源/屬性(來自 `/libs`)會由覆蓋/覆寫使用(通常在 `/apps`)。

### 建立結構 {#creating-the-structure}

若要建立覆蓋或覆寫，您必須在目標(通常為 `/apps`)。 例如：

* 覆蓋

   * 如邊欄中所示，Sites主控台的導覽項目定義如下：

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 若要覆蓋，請建立下列節點：

      `/apps/cq/core/content/nav/sites`

      然後更新屬性 `jcr:title` 視需要。

* 覆寫

   * Texts控制台的觸控式對話方塊的定義，定義於：

      `/libs/foundation/components/text/cq:dialog`

   * 若要覆寫此值，請建立下列節點，例如：

      `/apps/the-project/components/text/cq:dialog`

要建立其中任一項，您只需重新建立骨架結構。 為簡化結構的重構，所有中間節點都可以是類型 `nt:unstructured` (不必反映原節點類型；例如， `/libs`)。

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
>使用Sling Resource Merger時（亦即處理標準觸控式UI時），不建議從 `/libs` 因此，將導致資訊被保留過多 `/apps`. 這在系統以任何方式升級時都可能造成問題。

### 使用案例 {#use-cases}

這些功能與標準功能結合，可讓您：

* **新增屬性**

   屬性不存在於 `/libs` 定義，但是 `/apps` 覆蓋/覆寫。

   1. 在內建立對應的節點 `/apps`
   1. 在此節點上建立新屬性「

* **重定義屬性（非自動建立的屬性）**

   屬性定義於 `/libs`，但需要新值 `/apps` 覆蓋/覆寫。

   1. 在內建立對應的節點 `/apps`
   1. 在此節點上建立相符的屬性（在/底下） `apps`)

      * 屬性的優先順序會以Sling資源解析器設定為基礎。
      * 支援變更屬性類型。

         如果您使用的屬性類型與 `/libs`，則會使用您定義的屬性類型。
   >[!NOTE]
   >
   >支援變更屬性類型。

* **重定義自動建立的屬性**

   依預設，自動建立的屬性(例如 `jcr:primaryType`)不受覆蓋/覆寫的限制，以確保目前位在下的節點類型 `/libs` 受人尊重。 若要加上覆蓋/覆寫，您必須在中重新建立節點 `/apps`，顯式隱藏屬性並重定義它：

   1. 在下建立對應的節點 `/apps` 與所需 `jcr:primaryType`
   1. 建立屬性 `sling:hideProperties` 在該節點上，將值設為自動建立屬性的值；例如， `jcr:primaryType`

      此屬性，定義於 `/apps`，現在會比下定義的優先順序 `/libs`

* **重新定義節點及其子節點**

   節點及其子項定義於 `/libs`，但需要新的設定 `/apps` 覆蓋/覆寫。

   1. 結合下列動作：

      1. 隱藏節點的子項（保留節點的屬性）
      1. 重定義屬性/屬性

* **隱藏屬性**

   屬性定義於 `/libs`，但不是 `/apps` 覆蓋/覆寫。

   1. 在內建立對應的節點 `/apps`
   1. 建立屬性 `sling:hideProperties` 類型 `String` 或 `String[]`. 使用它指定要隱藏/忽略的屬性。 您也可以使用萬用字元。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隱藏節點及其子代**

   節點及其子項定義於 `/libs`，但不是 `/apps` 覆蓋/覆寫。

   1. 在/apps下建立對應節點
   1. 建立屬性 `sling:hideResource`

      * 類型: `Boolean`
      * 值: `true`

* **隱藏節點的子項（同時保留節點的屬性）**

   節點、其屬性及其子項定義於 `/libs`. 節點及其屬性是 `/apps` 覆蓋/覆蓋，但部分或所有子節點在 `/apps` 覆蓋/覆寫。

   1. 在下建立對應的節點 `/apps`
   1. 建立屬性 `sling:hideChildren`:

      * 類型: `String[]`
      * 值：子節點的清單(如 `/libs`)以隱藏/忽略

      通配符&amp;ast;可用於隱藏/忽略所有子節點。


* **重新排序節點**

   節點及其同層級在 `/libs`. 需要新位置，因此會在 `/apps` 覆蓋/覆蓋，其中新位置是在參考中適當的同級節點時定義 `/libs`.

   * 使用 `sling:orderBefore` 屬性：

      1. 在下建立對應的節點 `/apps`
      1. 建立屬性 `sling:orderBefore`:

         這會指定節點(如 `/libs`)，目前節點應放置在以下位置之前：

         * 類型: `String`
         * 值: `<before-SiblingName>`

### 從程式碼叫用Sling Resource Merger {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger包含兩個自訂資源提供者：一個用於覆蓋，另一個用於覆寫。 您可以使用裝載點在您的代碼中叫用其中的每一項：

>[!NOTE]
>
>訪問資源時，建議使用適當的裝載點。
>
>這可確保叫用Sling Resource Merger並傳回完全合併的資源(減少需要從 `/libs`)。

* 覆蓋:

   * 目的：根據資源的搜索路徑合併資源
   * 裝載點： `/mnt/overlay`
   * 用法： `mount point + relative path`
   * 範例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 覆寫:

   * 目的：根據資源的超類型合併資源
   * 裝載點： `/mnt/overide`
   * 用法： `mount point + absolute path`
   * 範例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 使用範例 {#example-of-usage}

其中包括：

* 覆蓋:

   * [自訂主控台](/help/sites-developing/customizing-consoles-touch.md)
   * [自訂頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md)

* 覆寫:

   * [設定頁面屬性](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
