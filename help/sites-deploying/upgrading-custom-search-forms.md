---
title: 升級自訂搜尋表單
seo-title: 升級自訂搜尋表單
description: 本文詳細說明在升級後需要進行的調整，以便自訂搜尋表單運作。
seo-description: 本文詳細說明在升級後需要進行的調整，以便自訂搜尋表單運作。
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 升級自訂搜尋表單{#upgrading-custom-search-forms}

在AEM 6.2中，自訂搜尋表單儲存在儲存庫中的位置已變更。 在升級後，它們會從6.1的位置移至：

* /apps/cq/gui/content/facets

到以下位置的新位置：

* /conf/global/settings/cq/search/facets

因此，在升級後需要手動調整，才能讓表單繼續運作。

這套用至新的搜尋表單，以及已自訂的預設表單。

如需詳細資訊，請參閱「搜尋 [刻面」檔案](/help/assets/search-facets.md)。

## 更改resourceType屬性 {#changing-the-resourcetype-property}

除非另有說明，在升級後需要進行的大部分調整都需要變更所設定自訂搜尋 `sling:resourceType` 表單的屬性。 這樣，屬性才能指向渲染指令碼的正確位置。

您可以執行下列動作來變更屬性：

1. 開啟CRXDE Lite，方法是前往 `https://server:port/crx/de/index.jsp`
1. 瀏覽至需要調整的節點位置，如下方自訂搜尋表單清 [單中所指定](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) 。
1. 按一下該節點。 在右側屬性窗格中，按一下並修改 **sling:resourceType** 屬性。
1. 最後，按「全部保存」按鈕 **保存更改** 。

## 自訂搜尋表單清單 {#list-of-custom-search-forms}

在下方，您將會找到所有自訂搜尋表單以及升級後需要的修改清單。 它們指中的名稱 `/conf/global/settings/cq/search/facets/sites/items`。

### 節點名為&quot;fulltext&quot;的Fulltext Predicate {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點</td>
   <td>全文</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

在AEM 6.1中，標準fulltext謂詞是搜尋表單的一部分。 在6.2中，全文欄位已由OmniSearch取代。 此謂語以程式設計方式跳過，可加以移除。

**** 動作：完全刪除節點。

### 其他全文謂語 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設「搜尋自」中的節點</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

### 路徑瀏覽器謂語 {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
   <td>路徑</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicates</p> </td>
  </tr>
 </tbody>
</table>

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

### 標籤謂語 {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
   <td>標記</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 動作：調整 **resourceType** 屬性(新增「**/coral**」，如上述6.2位置)。

### 頁面狀態述詞 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

「頁面狀態」已由兩個「選項屬性謂語」取代，一個用於發佈，另一個用於LiveCopy狀態。

**動作:**

* 刪除節 `pagestatuspredicate` 點
* 複製節點

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 至 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 複製節點

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 至 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 請務必將節 `listOrder` 點的屬性 `analyticspredicate` 設為「**8**」。 這是避免衝突的必要條件。

### 日期範圍謂語 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>6.1中的資源類型</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicates</p> </td>
  </tr>
 </tbody>
</table>

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

### 隱藏的篩選器 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
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

**** 動作：沒什麼可調整的。

### Analytics 述詞 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
   <td>分析用</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

### 範圍述詞 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
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

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

>[!NOTE]
>
>注意：與6.1相反，「範圍謂語」不再在搜尋列中演算標籤。

### 選項屬性述詞 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

### 滑桿範圍述詞 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

### 元件述詞 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
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

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

### 作者述詞 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicates</p> </td>
  </tr>
 </tbody>
</table>

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

### 範本述詞 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /><br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

## 資產管理搜尋邊欄 {#assets-admin-search-rail}

以下節點參考 `/conf/global/settings/dam/search/facets/assets/items`

### 節點名為&quot;fulltext&quot;的Fulltext Predicate {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1中預設搜尋表單中的節點 | 全文 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| 6.2中的資源類型 | N/A |

在6.1中，標準fulltext謂語是搜尋表單的一部分。 在6.2中，全文欄位已由OmniSearch取代。 此謂語以程式設計方式跳過，可加以移除。

**** 動作：刪除上述節點。

### 路徑瀏覽器謂語 {#path-browser-predicates-1}

| 6.1中預設搜尋表單中的節點 | 路徑瀏覽器 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicates |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicates |

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

### Mime類型謂語 {#mime-type-predicates}

| 6.1中預設搜尋表單中的節點 | mimetype |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicates |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicates |

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)。

### 檔案大小謂語 {#file-size-predicates}

| 6.1中預設搜尋表單中的節點 | 檔案大小 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicates |

**** 動作：如上 `resourceType` 述6.2位置所示調整。

### 資產上次修改的謂語 {#asset-last-modified-predicates}

| 6.1中預設搜尋表單中的節點 | assetlastmodifedpredicate |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifedpredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifedpredicate |

動作：調整resourceType屬性（如上方6.2位置中的新增&quot;/coral&quot;）。

### 發佈謂語 {#publish-predicate}

| 6.1中預設搜尋表單中的節點 | 發佈 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**動作:**

* 調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)

* 新增 `optionPaths` （類型為字串）屬性與值： `/libs/dam/options/predicates/publish`

* 使用 `singleSelect` 布林值新增屬性 `true`。

### 狀態謂語 {#status-predicates}

| 6.1中預設搜尋表單中的節點 | 狀態 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicates |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicates |

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)

### 到期狀態謂語 {#expiry-status-predicates}

| 6.1中預設搜尋表單中的節點 | 過期狀態 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)

### 中繼資料有效性謂語 {#metadata-validity-predicates}

| 6.1中預設搜尋表單中的節點 | 元資料有效性 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicates |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicates |

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)

### 分級謂語 {#rating-predicates}

| 6.1中預設搜尋表單中的節點 | 評等 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicates |

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)

### Orientation Predicate {#orientation-predicate}

| 6.1中預設搜尋表單中的節點 | 方向 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/tagfilterpredicate |
| 6.2中的資源類型 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**動作:**

* 調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)

* 在相 `fieldLabel` 同節點上添加與屬 `text` 性值相同的屬性。

* 在相 `emptyText` 同節點上添加與屬 `text` 性值相同的屬性。

* 在相 `rootPath` 同節點上添加與屬性值 `optionPaths` 相同的屬性。

### Style Predicate {#style-predicate}

| 6.1中預設搜尋表單中的節點 | 樣式 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/tagfilterpredicate |
| 6.2中的資源類型 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**動作:**

* 調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)

* 在相 `fieldLabel` 同節點上添加與屬 `text` 性值相同的屬性。

* 在相 `emptyText` 同節點上添加與屬 `text` 性值相同的屬性。

* 在相 `rootPath` 同節點上添加與屬性值 `optionPaths` 相同的屬性。

### 視訊格式謂語 {#video-format-predicates}

| 6.1中預設搜尋表單中的節點 | videoFormat |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicates |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicates |

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)

### Mainasset Predicate {#mainasset-predicate}

| 6.1中預設搜尋表單中的節點 | mainasset |
|---|---|
| 6.1中的資源類型 | granite/ui/components/foundation/form/hidden |
| 6.2中的資源類型 | granite/ui/components/coral/foundation/form/hidden |

**** 動作：調整 `resourceType` 屬性(新增「**/coral**」，如上述6.2位置)
