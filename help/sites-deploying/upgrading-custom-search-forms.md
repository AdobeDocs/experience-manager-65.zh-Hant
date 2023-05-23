---
title: 升級自定義搜索Forms
seo-title: Upgrading Custom Search Forms
description: 本文詳細介紹了升級後為使自定義搜索表單正常運行而需要的調整。
seo-description: This article details the adjustments that are required after an upgrade in order for the custom search forms to function.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
feature: Upgrading
exl-id: 797bbdf9-917a-4537-a5f9-bf2682db968b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 3%

---

# 升級自定義搜索Forms{#upgrading-custom-search-forms}

在AEM6.2中，自定義搜索Forms儲存在儲存庫中的位置已更改。 升級後，它們將從6.1中的位置移至：

* /apps/cq/gui/content/facets

到下面的新位置：

* /conf/global/settings/cq/search/facets

因此，在升級後需要手動調整，以使表單繼續工作。

這適用於新的搜索Forms以及已自定義的預設Forms。

有關詳細資訊，請參閱 [搜索小平面](/help/assets/search-facets.md)。

## 更改resourceType屬性 {#changing-the-resourcetype-property}

除非另有說明，否則升級後需要進行的大多數調整都要求更改 `sling:resourceType` 配置的自定義搜索Forms的屬性。 這是必需的，以便屬性指向呈現指令碼的正確位置。

可通過執行以下操作來更改屬性：

1. 通過轉到開啟CRXDE Lite `https://server:port/crx/de/index.jsp`
1. 瀏覽到需要調整的節點的位置，如清單中所指定 [自定義搜索Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) 下。
1. 按一下節點。 在右側的屬性窗格中，按一下並修改 **sling:resourceType** 屬性。
1. 最後，通過按 **全部保存** 按鈕

## 自定義搜索清單Forms {#list-of-custom-search-forms}

在下面，您將找到所有自定義搜索Forms及其升級後所需修改的清單。 他們指的是 `/conf/global/settings/cq/search/facets/sites/items`。

### 節點名為&quot;fulltext&quot;的全文謂詞 {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒</td>
   <td>全文</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/common/admin/customsearch/search謂詞/fulltext謂詞</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

在AEM6.1中，標準全文謂詞是搜索表單的一部分。 在6.2中，全文欄位已被OmniSearch替換。 此謂語以寫程式方式跳過，可以刪除。

**操作：** 完全刪除節點。

### 其他全文謂詞 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索自中的節點/秒</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/common/admin/customsearch/search謂詞/fulltext謂詞</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>common/admin/customsearch/search謂詞/fulltext謂詞</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### 路徑瀏覽器謂詞 {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>路徑</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/common/admin/customsearch/search謂詞/路徑謂詞</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>常見/管理員/自定義搜索/搜索謂語/路徑謂語</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### 標籤謂語 {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>標記</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/common/admin/customsearch/search謂詞/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>common/admin/customsearch/search謂詞/tagpredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 **資源類型** 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### 頁面狀態述詞 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>pagestus謂詞</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/siteadmin/admin/searchpanel/search謂詞/pagestatus謂詞</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

「頁面狀態」已被兩個「選項」屬性謂語替換，一個用於發佈，一個用於LiveCopy狀態。

**動作:**

* 刪除 `pagestatuspredicate` 節點
* 複製節點

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 至 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 複製節點

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 至 `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 確保已設定 `listOrder` 屬性 `analyticspredicate` 節點到「**8**。 為避免衝突，需要這樣做。

### 日期範圍謂語 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>達蘭治謂語</td>
  </tr>
  <tr>
   <td>6.1中的資源類型</td>
   <td>cq/gui/元件/common/admin/customsearch/search謂語/daterange謂語</td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>common/admin/customsearch/search謂語/daterange謂詞</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### 隱藏的篩選器 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>類型</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>花崗岩/ui/元件/地基/形式/隱藏</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>花崗岩/ui/元件/地基/形式/隱藏</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 沒什麼可調整的。

### Analytics 述詞 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>分析</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/siteadmin/admin/searchpanel/search謂詞/分析</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>siteadmin/admin/searchpanel/search謂詞/分析</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### 範圍述詞 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/siteadmin/admin/searchpanel/search謂詞/range謂詞</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>siteadmin/admin/searchpanel/search謂詞/range謂詞</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

>[!NOTE]
>
>注：與6.1相反，「範圍謂語」不再在搜索欄中呈現標籤。

### 選項屬性述詞 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/siteadmin/admin/searchpanel/search謂詞/選項spredicates</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>siteadmin/admin/searchpanel/search謂詞/選項指定</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### 滑桿範圍述詞 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/siteadmin/admin/searchpanel/search謂詞/sliderrang謂詞</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>siteadmin/admin/searchpanel/search謂詞/sliderrange謂詞</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### 元件述詞 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>siteadmin/admin/searchpanel/search謂詞/元件指南</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### 作者述詞 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/siteadmin/admin/searchpanel/search謂詞/userpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>siteadmin/admin/searchpanel/search謂詞/用戶謂詞</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### 範本述詞 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>6.1中預設搜索表單中的節點/秒<br /> <br /> </td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><p>6.1中的資源類型</p> </td>
   <td><p>cq/gui/元件/siteadmin/admin/searchpanel/search謂詞/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的資源類型</td>
   <td><p>cq/gui/元件<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

## 資產管理搜尋邊欄 {#assets-admin-search-rail}

以下節點引用 `/conf/global/settings/dam/search/facets/assets/items`

### 節點名為&quot;fulltext&quot;的全文謂詞 {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1中預設搜索表單中的節點/秒 | 全文 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search謂詞/fulltext謂詞 |
| 6.2中的資源類型 | N/A |

在6.1中，標準全文謂詞是搜索表單的一部分。 在6.2中，全文欄位已被OmniSearch替換。 此謂語以寫程式方式跳過，可以刪除。

**操作：** 刪除上述節點。

### 路徑瀏覽器謂詞 {#path-browser-predicates-1}

| 6.1中預設搜索表單中的節點/秒 | 路徑瀏覽器 |
|---|---|
| 6.1中的資源類型 | dam/gui/元件/admin/customsearch/search謂語/pathbrowser謂詞 |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search謂語/pathbrowser謂詞 |

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### MIME類型謂詞 {#mime-type-predicates}

| 6.1中預設搜索表單中的節點/秒 | mimetype |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search謂詞/選項指定 |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search謂語/選項spredicate |

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)。

### 檔案大小謂語 {#file-size-predicates}

| 6.1中預設搜索表單中的節點/秒 | 檔案大小 |
|---|---|
| 6.1中的資源類型 | dam/gui/元件/admin/customsearch/search謂語/filesize謂詞 |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search謂語/sliderange謂語 |

**操作：** 調整 `resourceType` 如上面6.2位置所示。

### 資產上次修改的謂詞 {#asset-last-modified-predicates}

| 6.1中預設搜索表單中的節點/秒 | asselastmodified謂詞 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search謂詞/assetlastmodified謂詞 |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search謂語/assetlastmodified謂詞 |

操作：調整resourceType屬性（添加「/coral」，如上所示的6.2位置）。

### 發佈謂詞 {#publish-predicate}

| 6.1中預設搜索表單中的節點/秒 | 發佈 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search謂詞/publishpredicate |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search謂語/publishpredicate |

**動作:**

* 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)

* 添加 `optionPaths` （類型為字串）屬性，其值為： `/libs/dam/options/predicates/publish`

* 添加 `singleSelect` 布爾值屬性 `true`。

### 狀態謂詞 {#status-predicates}

| 6.1中預設搜索表單中的節點/秒 | 狀態 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search謂詞/選項指定 |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search謂語/選項spredicate |

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)

### 到期狀態謂詞 {#expiry-status-predicates}

| 6.1中預設搜索表單中的節點/秒 | 過期狀態 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search謂語/expiredasse謂詞 |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search謂語/expiredasse謂詞 |

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)

### 元資料有效性謂語 {#metadata-validity-predicates}

| 6.1中預設搜索表單中的節點/秒 | 元資料有效性 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search謂詞/選項指定 |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search謂語/選項spredicate |

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)

### 評級謂語 {#rating-predicates}

| 6.1中預設搜索表單中的節點/秒 | 評等 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search謂詞/rating謂詞 |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search謂語/sliderange謂語 |

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)

### 方向謂詞 {#orientation-predicate}

| 6.1中預設搜索表單中的節點/秒 | 方向 |
|---|---|
| 6.1中的資源類型 | dam/gui/元件/admin/customsearch/search謂語/tagfilter謂詞 |
| 6.2中的資源類型 | cq/gui/元件/coral/common/admin/customsearch/search謂詞/tagspredicate |

**動作:**

* 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)

* 添加 `fieldLabel` 與 `text` 屬性。

* 添加 `emptyText` 值與 `text` 屬性。

* 添加 `rootPath` 與 `optionPaths` 屬性。

### 樣式謂詞 {#style-predicate}

| 6.1中預設搜索表單中的節點/秒 | 風格 |
|---|---|
| 6.1中的資源類型 | dam/gui/元件/admin/customsearch/search謂語/tagfilter謂詞 |
| 6.2中的資源類型 | cq/gui/元件/coral/common/admin/customsearch/search謂詞/tagspredicate |

**動作:**

* 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)

* 添加 `fieldLabel` 與 `text` 屬性。

* 添加 `emptyText` 值與 `text` 屬性。

* 添加 `rootPath` 與 `optionPaths` 屬性。

### 視頻格式謂語 {#video-format-predicates}

| 6.1中預設搜索表單中的節點/秒 | 視頻格式 |
|---|---|
| 6.1中的資源類型 | dam/gui/components/admin/customsearch/search謂詞/選項指定 |
| 6.2中的資源類型 | dam/gui/coral/components/admin/customsearch/search謂語/選項spredicate |

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)

### Mainasset謂詞 {#mainasset-predicate}

| 6.1中預設搜索表單中的節點/秒 | 維護 |
|---|---|
| 6.1中的資源類型 | 花崗岩/ui/元件/地基/形式/隱藏 |
| 6.2中的資源類型 | 花崗岩/ui/元件/珊瑚/地基/形式/隱藏 |

**操作：** 調整 `resourceType` 屬性（添加&quot;）**/coral**&quot;如上文6.2所示)
