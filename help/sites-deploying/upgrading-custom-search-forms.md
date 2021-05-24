---
title: 升級自訂搜尋Forms
seo-title: 升級自訂搜尋Forms
description: 本文詳細說明升級後所需的調整，以便自訂搜尋表單運作。
seo-description: 本文詳細說明升級後所需的調整，以便自訂搜尋表單運作。
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
feature: 升級
exl-id: 797bbdf9-917a-4537-a5f9-bf2682db968b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 3%

---

# 升級自訂搜尋Forms{#upgrading-custom-search-forms}

在AEM 6.2中，自訂搜尋Forms儲存於存放庫的位置已變更。 升級後，它們會從6.1的位置移至：

* /apps/cq/gui/content/facets

到以下的新位置：

* /conf/global/settings/cq/search/facets

因此，升級後需要手動調整，表單才能繼續運作。

這會套用至新的搜尋Forms，以及已自訂的預設Forms。

如需詳細資訊，請參閱[搜尋Facet](/help/assets/search-facets.md)上的檔案。

## 更改resourceType屬性{#changing-the-resourcetype-property}

除非另有說明，否則升級後需要進行的大部分調整都需要變更已設定自訂搜尋Forms的`sling:resourceType`屬性。 這是必需的，以便屬性指向呈現指令碼的正確位置。

您可以執行下列動作來變更屬性：

1. 前往`https://server:port/crx/de/index.jsp`開啟CRXDE Lite
1. 瀏覽至需要調整的節點位置，如下方[自訂搜尋Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms)清單中所指定。
1. 按一下節點。 在右側屬性窗格中，按一下並修改&#x200B;**sling:resourceType**&#x200B;屬性。
1. 最後，按&#x200B;**Save All**&#x200B;按鈕保存更改。

## 自訂搜尋Forms清單{#list-of-custom-search-forms}

以下是所有自訂搜尋Forms的清單，以及升級後所需的修改。 它們指`/conf/global/settings/cq/search/facets/sites/items`中的名稱。

### 節點名為&quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}的全文謂詞

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點</td>
   <td>全文</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

在AEM 6.1中，標準全文述詞是搜尋表單的一部分。 在6.2中，全文欄位已由OmniSearch取代。 此謂語會以程式設計方式跳過，且可以移除。

**動作：** 完全移除節點。

### 其他全文謂詞{#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設的「搜索自」節點</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

### 路徑瀏覽器述詞{#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>路徑</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

### 標籤謂語{#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>標記</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicates</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 **** resourceTypeproperty(新增「**/coral**」，如同上述6.2位置)。

### 頁面狀態述詞 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>pagestatuspredipate</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

「頁面狀態」已由兩個「選項」屬性述詞取代，一個用於發佈，另一個用於LiveCopy狀態。

**動作:**

* 移除`pagestatuspredicate`節點
* 複製節點

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 至 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 複製節點

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 至 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 請務必將`analyticspredicate`節點的`listOrder`屬性設定為&quot;**8**&quot;。 這是避免衝突所必需的。

### 日期範圍述詞{#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>6.1中的資源類型</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

### 隱藏的篩選器 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>類型</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 無需調整。

### Analytics 述詞 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>分析</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicates</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

### 範圍述詞 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

>[!NOTE]
>
>注意：與6.1相反，「範圍述詞」不再在搜尋列中轉譯標籤。

### 選項屬性述詞 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicates</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

### 滑桿範圍述詞 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

### 元件述詞 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

### 作者述詞 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

### 範本述詞 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1<br /> <br />中預設搜尋表單中的節點 </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicates</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

## 資產管理搜尋邊欄 {#assets-admin-search-rail}

以下節點引用`/conf/global/settings/dam/search/facets/assets/items`中的名稱

### 節點名為&quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}的全文謂詞

| 6.1中預設搜尋表單中的節點 | 全文 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| 6.2中的資源類型 | N/A |

在6.1中，標準全文謂語是搜索表單的一部分。 在6.2中，全文欄位已由OmniSearch取代。 此謂語會以程式設計方式跳過，且可以移除。

**動作：** 移除上述節點。

### 路徑瀏覽器述詞{#path-browser-predicates-1}

| 6.1中預設搜尋表單中的節點 | pathbrowser |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchdedicates/pathbrowserpredicate |

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

### Mime類型謂詞{#mime-type-predicates}

| 6.1中預設搜尋表單中的節點 | mimetype |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search述詞/optionspdicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search述詞/optionspredicates |

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)。

### 檔案大小謂詞{#file-size-predicates}

| 6.1中預設搜尋表單中的節點 | 檔案大小 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search述詞/filesizepredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**動作：** 如 `resourceType` 上方6.2位置所示調整。

### 資產上次修改的謂語{#asset-last-modified-predicates}

| 6.1中預設搜尋表單中的節點 | assetlastmodifedpredicate |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchdredicates/assetlastmodifedpredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchdredicates/assetlastmodifedpredicate |

動作：調整resourceType屬性（新增「/coral」，如上方6.2位置所示）。

### 發佈述詞{#publish-predicate}

| 6.1中預設搜尋表單中的節點 | 發佈 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**動作:**

* 調整`resourceType`屬性（新增&quot;**/coral**&quot;，如上所示6.2位置）

* 使用值新增`optionPaths`（類型為字串）屬性：`/libs/dam/options/predicates/publish`

* 使用布林值`true`添加`singleSelect`屬性。

### 狀態謂詞{#status-predicates}

| 6.1中預設搜尋表單中的節點 | 狀態 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search述詞/optionspdicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search述詞/optionspredicates |

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)

### 到期狀態謂詞{#expiry-status-predicates}

| 6.1中預設搜尋表單中的節點 | 有效狀態 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchdredicates/expiredassetpredicate |

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)

### 元資料有效性謂語{#metadata-validity-predicates}

| 6.1中預設搜尋表單中的節點 | 中繼資料有效性 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search述詞/optionspdicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search述詞/optionspredicates |

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)

### 分級謂語{#rating-predicates}

| 6.1中預設搜尋表單中的節點 | 評等 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search述詞/ratingpredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)

### 方向述詞{#orientation-predicate}

| 6.1中預設搜尋表單中的節點 | 方向 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/tagfilterpredicate |
| 6.2中的資源類型 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicates |

**動作:**

* 調整`resourceType`屬性（新增&quot;**/coral**&quot;，如上所示6.2位置）

* 在相同節點上，新增與`text`屬性值相同的`fieldLabel`屬性。

* 在相同節點上新增與`text`屬性值相同的`emptyText`屬性。

* 在相同節點上，新增與`optionPaths`屬性值相同的`rootPath`屬性。

### 樣式述詞{#style-predicate}

| 6.1中預設搜尋表單中的節點 | 樣式 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/tagfilterpredicate |
| 6.2中的資源類型 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicates |

**動作:**

* 調整`resourceType`屬性（新增&quot;**/coral**&quot;，如上所示6.2位置）

* 在相同節點上，新增與`text`屬性值相同的`fieldLabel`屬性。

* 在相同節點上新增與`text`屬性值相同的`emptyText`屬性。

* 在相同節點上，新增與`optionPaths`屬性值相同的`rootPath`屬性。

### 視訊格式述詞{#video-format-predicates}

| 6.1中預設搜尋表單中的節點 | videoFormat |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search述詞/optionspdicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search述詞/optionspredicates |

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)

### Mainasset謂語{#mainasset-predicate}

| 6.1中預設搜尋表單中的節點 | mainasset |
|---|---|
| 6.1中的資源類型 | granite/ui/components/foundation/form/hidden |
| 6.2中的資源類型 | granite/ui/components/coral/foundation/form/hidden |

**動作：** 調整 `resourceType` 屬性(新增「**/coral**」，如同上述6.2位置)
