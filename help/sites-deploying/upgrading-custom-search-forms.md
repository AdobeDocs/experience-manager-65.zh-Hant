---
title: 升級自訂搜尋Forms
seo-title: Upgrading Custom Search Forms
description: 本文詳細說明為了讓自訂搜尋表單正常運作，在升級後所需的調整。
seo-description: This article details the adjustments that are required after an upgrade in order for the custom search forms to function.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
feature: Upgrading
exl-id: 797bbdf9-917a-4537-a5f9-bf2682db968b
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 3%

---

# 升級自訂搜尋Forms{#upgrading-custom-search-forms}

在AEM 6.2中，存放庫內儲存自訂搜尋Forms的位置已變更。 升級後，這些檔案會從6.1中的位置移至：

* /apps/cq/gui/content/facets

移至下的新位置：

* /conf/global/settings/cq/search/facets

因此，升級後需要手動調整，表單才能繼續運作。

這適用於新的搜尋Forms以及已自訂的預設Forms。

如需詳細資訊，請參閱以下檔案： [搜尋Facet](/help/assets/search-facets.md).

## 變更resourceType屬性 {#changing-the-resourcetype-property}

除非另有說明，否則升級後需要完成的大部分調整都需要變更 `sling:resourceType` 屬性來搜尋已設定的自訂搜尋Forms。 此屬性是必要的，這樣屬性才能指向轉譯指令碼的正確位置。

您可以執行下列動作來變更屬性：

1. 前往以下位置開啟CRXDE Lite： `https://server:port/crx/de/index.jsp`
1. 瀏覽到需要調整的節點位置，如清單中的指定 [自訂搜尋Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) 底下。
1. 按一下節點。 在右側屬性窗格中，按一下並修改 **sling：resourceType** 屬性。
1. 最後，按下 **全部儲存** 按鈕。

## 自訂搜尋Forms清單 {#list-of-custom-search-forms}

在下方，您會找到所有自訂Search Forms的清單，以及升級後所需的修改。 它們是指中的名稱 `/conf/global/settings/cq/search/facets/sites/items`.

### 節點名稱為「全文」的全文述詞 {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點</td>
   <td>全文</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

在AEM 6.1中，標準全文檢索述詞是搜尋表單的一部分。 在6.2中，全文欄位已由OmniSearch取代。 這個述詞會以程式設計方式略過，而且可以移除。

**動作：** 完全移除節點。

### 其他全文檢索述詞 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋來源中的節點</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### 路徑瀏覽器述詞 {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>path</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### 標籤述詞 {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>標記</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 **resourceType** 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### 頁面狀態述詞 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

「頁面狀態」已被兩個「選項」屬性述詞取代，一個用於「發佈」，另一個用於「即時副本」狀態。

**動作:**

* 移除 `pagestatuspredicate` 節點
* 複製節點

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 至 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 複製節點

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 至 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 請務必設定 `listOrder` 的屬性 `analyticspredicate` 節點至&quot;**8**「。 這是避免衝突所需。

### 日期範圍述詞 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>日期範圍述詞</td>
  </tr>
  <tr>
   <td>6.1中的資源型別</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### 隱藏的篩選器 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>類型</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 沒有可調整的內容。

### Analytics 述詞 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>analyticsspredicate</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticsspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticsspredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### 範圍述詞 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

>[!NOTE]
>
>注意：相對於6.1，範圍述詞不再在搜尋列中呈現標籤。

### 選項屬性述詞 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### 滑桿範圍述詞 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### 元件述詞 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### 作者述詞 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### 範本述詞 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜尋表單中的節點<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源型別</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源型別</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

## 資產管理搜尋邊欄 {#assets-admin-search-rail}

以下節點代表中的名稱 `/conf/global/settings/dam/search/facets/assets/items`

### 節點名稱為「全文」的全文述詞 {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1中預設搜尋表單中的節點 | 全文 |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| 6.2中的資源型別 | N/A |

在6.1中，標準全文檢索述詞是搜尋表單的一部分。 在6.2中，全文欄位已由OmniSearch取代。 這個述詞會以程式設計方式略過，而且可以移除。

**動作：** 移除上述節點。

### 路徑瀏覽器述詞 {#path-browser-predicates-1}

| 6.1中預設搜尋表單中的節點 | 路徑瀏覽器 |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| 6.2中的資源型別 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### Mime型別述詞 {#mime-type-predicates}

| 6.1中預設搜尋表單中的節點 | mimetype |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2中的資源型別 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上面指示的6.2位置中)。

### 檔案大小述詞 {#file-size-predicates}

| 6.1中預設搜尋表單中的節點 | filesize |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| 6.2中的資源型別 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**動作：** 調整 `resourceType` 如上方6.2位置所示。

### 資產上次修改時間述詞 {#asset-last-modified-predicates}

| 6.1中預設搜尋表單中的節點 | assetlastmodifiedpredicate |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| 6.2中的資源型別 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

動作：調整resourceType屬性（新增「/coral」，如上方所示的6.2位置）。

### 發佈述詞 {#publish-predicate}

| 6.1中預設搜尋表單中的節點 | 發佈 |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| 6.2中的資源型別 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**動作:**

* 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上方所示的6.2位置)

* 新增 `optionPaths` （型別為String）屬性，其值為： `/libs/dam/options/predicates/publish`

* 新增 `singleSelect` 含布林值的屬性 `true`.

### 狀態述詞 {#status-predicates}

| 6.1中預設搜尋表單中的節點 | 狀態 |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2中的資源型別 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上方所示的6.2位置)

### 到期狀態述詞 {#expiry-status-predicates}

| 6.1中預設搜尋表單中的節點 | 到期狀態 |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| 6.2中的資源型別 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上方所示的6.2位置)

### 中繼資料有效性述詞 {#metadata-validity-predicates}

| 6.1中預設搜尋表單中的節點 | 中繼資料有效性 |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2中的資源型別 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上方所示的6.2位置)

### 評等述詞 {#rating-predicates}

| 6.1中預設搜尋表單中的節點 | 評等 |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| 6.2中的資源型別 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上方所示的6.2位置)

### 方向述詞 {#orientation-predicate}

| 6.1中預設搜尋表單中的節點 | 方向 |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| 6.2中的資源型別 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**動作:**

* 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上方所示的6.2位置)

* 新增 `fieldLabel` 與的值相同的屬性 `text` 屬性。

* 新增 `emptyText` 屬性的值與 `text` 屬性。

* 新增 `rootPath` 與具有相同值的屬性 `optionPaths` 屬性。

### 樣式述詞 {#style-predicate}

| 6.1中預設搜尋表單中的節點 | 樣式 |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| 6.2中的資源型別 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**動作:**

* 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上方所示的6.2位置)

* 新增 `fieldLabel` 與的值相同的屬性 `text` 屬性。

* 新增 `emptyText` 屬性的值與 `text` 屬性。

* 新增 `rootPath` 與具有相同值的屬性 `optionPaths` 屬性。

### 視訊格式述詞 {#video-format-predicates}

| 6.1中預設搜尋表單中的節點 | videoFormat |
|---|---|
| 6.1中的資源型別 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2中的資源型別 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上方所示的6.2位置)

### Mainasset述詞 {#mainasset-predicate}

| 6.1中預設搜尋表單中的節點 | 主要資產 |
|---|---|
| 6.1中的資源型別 | granite/ui/components/foundation/form/hidden |
| 6.2中的資源型別 | granite/ui/components/coral/foundation/form/hidden |

**動作：** 調整 `resourceType` 屬性(新增&quot;**/coral**&quot;如上方所示的6.2位置)
