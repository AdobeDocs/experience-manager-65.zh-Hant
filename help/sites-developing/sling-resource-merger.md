---
title: Sling資源合併的應用研AEM究
seo-title: Using the Sling Resource Merger in AEM
description: Sling Resource Compurate提供訪問和合併資源的服務
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

# Sling資源合併的應用研AEM究{#using-the-sling-resource-merger-in-aem}

## 用途 {#purpose}

Sling Resource Compurate提供訪問和合併資源的服務。 它為以下兩項提供了差異（差異）機制：

* **[覆蓋](/help/sites-developing/overlays.md)** 使用 [配置的搜索路徑](/help/sites-developing/overlays.md#configuring-the-search-paths)。

* **覆蓋** 啟用觸摸的UI的元件對話框(`cq:dialog`)，使用資源類型層次結構(通過屬性 `sling:resourceSuperType`)。

使用Sling Resource Mobare，重疊/覆蓋資源和/或屬性與原始資源/屬性合併：

* 自定義定義的內容比原始定義的內容具有更高的優先順序(即 *重疊* 或 *覆蓋* )。

* 必要時， [屬性](#properties) 定義，指明如何使用從原始檔案合併的內容。

>[!CAUTION]
>
>Sling資源合併及相關方法只能用於 [花崗岩](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。 這也意味著它只適用於標準的、可觸摸的UI;尤其是，以這種方式定義的替代僅適用於元件的啟用觸摸的對話框。
>
>覆蓋/覆蓋其他區域（包括啟用觸摸的元件或標準UI的其他方面）涉及將相應的節點和結構從原始節點複製到定義自定義的位置。

### 目標AEM {#goals-for-aem}

在中使用Sling Resource Compure的目AEM標是：

* 確保未在中進行自定義更改 `/libs`。
* 減少複製自 `/libs`。

   使用Sling Resource Mobale時，建議不要從 `/libs` 這將導致在自定義中保留太多資訊(通常 `/apps`)。 當系統以任何方式升級時，重複資訊會不必要地增加出現問題的可能性。

>[!NOTE]
>
>替代不依賴於搜索路徑，它們使用屬性 `sling:resourceSuperType` 建立聯繫。
>
>但是，覆蓋通常在 `/apps`，因為中的最AEM佳做法是在 `/apps`;因為你不能在 `/libs`。

>[!CAUTION]
>
>你 ***必須*** 沒有改變 `/libs` 路徑。
>
>這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時很可能被覆蓋）。
>
>建議的配置和其他更改方法是：
>
>1. 重新建立所需項(如 `/libs`) `/apps`
>
>1. 在 `/apps`

>


### 屬性 {#properties}

資源合併提供以下屬性：

* `sling:hideProperties` ( `String` 或 `String[]`)

   指定要隱藏的屬性或屬性清單。

   通配符 `*` 全部隱藏。

* `sling:hideResource` ( `Boolean`)

   指示是否應完全隱藏資源，包括其子資源。

* `sling:hideChildren` ( `String` 或 `String[]`)

   包含要隱藏的子節點或子節點清單。 將維護節點的屬性。

   通配符 `*` 全部隱藏。

* `sling:orderBefore` ( `String`)

   包含當前節點應位於的前面的同級節點的名稱。

這些屬性影響相應/原始資源/屬性(來自 `/libs`)由覆蓋/覆蓋使用(通常在 `/apps`)。

### 建立結構 {#creating-the-structure}

要建立覆蓋或覆蓋，您需要在目標（通常是）下重新建立具有等效結構的原始節點 `/apps`)。 例如：

* 覆蓋

   * 「站點」控制台的導航條目定義，如滑軌中所示，定義如下：

      `/libs/cq/core/content/nav/sites/jcr:title`

   * 要覆蓋此節點，請建立以下節點：

      `/apps/cq/core/content/nav/sites`

      然後更新屬性 `jcr:title` 按需要。

* 覆寫

   * 「文本」控制台的「啟用觸摸」對話框的定義在以下位置定義：

      `/libs/foundation/components/text/cq:dialog`

   * 要覆蓋此項，請建立以下節點 — 例如：

      `/apps/the-project/components/text/cq:dialog`

要建立其中任何一種，您只需重新建立骨架結構。 為了簡化結構的重構，所有中間節點都可以是類型 `nt:unstructured` (不需要反映原節點類型；例如，在 `/libs`)。

因此，在上面的覆蓋示例中，需要以下節點：

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
>使用Sling Resource Mobale（即，在處理標準的啟用觸摸的UI時）時，建議不要從 `/libs` 因為它會導致太多資訊 `/apps`。 這會在系統以任何方式升級時引起問題。

### 使用案例 {#use-cases}

這些功能與標準功能相結合，使您能夠：

* **添加屬性**

   該屬性在 `/libs` 定義，但在 `/apps` 覆蓋/覆蓋。

   1. 在內建立相應的節點 `/apps`
   1. 在此節點「」上建立新屬性

* **重定義屬性（不是自動建立的屬性）**

   屬性在中定義 `/libs`，但在 `/apps` 覆蓋/覆蓋。

   1. 在內建立相應的節點 `/apps`
   1. 在此節點上建立匹配屬性（在/下） `apps`)

      * 屬性將具有基於Sling資源解析器配置的優先順序。
      * 支援更改屬性類型。

         如果使用的屬性類型與中使用的屬性類型不同 `/libs`，則將使用您定義的屬性類型。
   >[!NOTE]
   >
   >支援更改屬性類型。

* **重定義自動建立的屬性**

   預設情況下，自動建立的屬性(如 `jcr:primaryType`)不受覆蓋/覆蓋的影響，以確保當前位於 `/libs` 受人尊重。 要施加覆蓋/覆蓋，必須在中重新建立節點 `/apps`，顯式隱藏屬性並重定義它：

   1. 在下面建立相應節點 `/apps` 與期望 `jcr:primaryType`
   1. 建立屬性 `sling:hideProperties` 在該節點上，將值設定為自動建立屬性的值；比如說， `jcr:primaryType`

      此屬性，定義於 `/apps`，現在將優先於在 `/libs`

* **重定義節點及其子級**

   節點及其子代在中定義 `/libs`，但在 `/apps` 覆蓋/覆蓋。

   1. 組合下列操作：

      1. 隱藏節點的子級（保留節點的屬性）
      1. 重定義屬性/屬性

* **隱藏屬性**

   屬性在中定義 `/libs`，但在 `/apps` 覆蓋/覆蓋。

   1. 在內建立相應的節點 `/apps`
   1. 建立屬性 `sling:hideProperties` 類型 `String` 或 `String[]`。 使用此選項可指定要隱藏/忽略的屬性。 也可以使用通配符。 例如：

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **隱藏節點及其子級**

   節點及其子代在中定義 `/libs`，但在 `/apps` 覆蓋/覆蓋。

   1. 在/apps下建立相應的節點
   1. 建立屬性 `sling:hideResource`

      * 類型: `Boolean`
      * 值: `true`

* **隱藏節點的子級（同時保留節點的屬性）**

   節點、其屬性及其子代在中定義 `/libs`。 節點及其屬性在 `/apps` 覆蓋/覆蓋，但是在 `/apps` 覆蓋/覆蓋。

   1. 在下面建立相應節點 `/apps`
   1. 建立屬性 `sling:hideChildren`:

      * 類型: `String[]`
      * 值：子節點清單（如中定義） `/libs`)隱藏/忽略

      通配符&amp;ast;可用於隱藏/忽略所有子節點。


* **重新排序節點**

   節點及其同級在 `/libs`。 需要新位置，因此在 `/apps` 覆蓋/覆蓋，其中新位置是在引用中相應的同級節點時定義的 `/libs`。

   * 使用 `sling:orderBefore` 屬性：

      1. 在下面建立相應節點 `/apps`
      1. 建立屬性 `sling:orderBefore`:

         這指定節點(如 `/libs`)當前節點應位於以下位置之前：

         * 類型: `String`
         * 值: `<before-SiblingName>`

### 從您的代碼中調用Sling資源合併 {#invoking-the-sling-resource-merger-from-your-code}

Sling資源合併包括兩個自定義資源提供商 — 一個用於覆蓋，另一個用於覆蓋。 可以使用裝載點在代碼中調用以下每項：

>[!NOTE]
>
>訪問資源時，建議使用適當的裝載點。
>
>這可確保調用Sling資源合併並返回完全合併的資源（減少需要從中複製的結構） `/libs`)。

* 覆蓋:

   * 目的：根據其搜索路徑合併資源
   * 裝載點： `/mnt/overlay`
   * 用法： `mount point + relative path`
   * 示例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* 覆寫:

   * 目的：基於其超級類型合併資源
   * 裝載點： `/mnt/overide`
   * 用法： `mount point + absolute path`
   * 示例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 使用示例 {#example-of-usage}

包括以下一些示例：

* 覆蓋:

   * [自定義控制台](/help/sites-developing/customizing-consoles-touch.md)
   * [自定義頁面創作](/help/sites-developing/customizing-page-authoring-touch.md)

* 覆寫:

   * [配置頁面屬性](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
