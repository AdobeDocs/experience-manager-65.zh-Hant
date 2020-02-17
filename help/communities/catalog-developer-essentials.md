---
title: Catalog Essentials
seo-title: Catalog Essentials
description: 目錄概觀
seo-description: 目錄概觀
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Catalog Essentials {#catalog-essentials}

本頁提供使用啟用社群網站目錄功能的基本資訊。

目錄功能包含在社群網站中時，可讓社群成員瀏覽並選擇目錄中所列的啟用資源。

該組 [ 件 `enablement catalog` 允許社區成員訪問](catalog.md) 支援資源目錄 [](resources.md)。 使用AEM標籤是管理目錄中啟用資源外觀的重要部分。

請參閱 [標籤啟用資源](tag-resources.md)。

## 用戶端基本功能 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>included</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱 <a href="catalog.md">目錄功能</a></td>
  </tr>
 </tbody>
</table>

## 伺服器端的基本功能 {#essentials-for-server-side}

### 目錄功能 {#catalog-function}

一種包括目錄功能的社區 [站點結構](functions.md#catalog-function)，包括配置的 `enablement catalog` 元件。

### 預先篩選 {#pre-filters}

將目錄功能新增至社群網站時，可以透過指定預先篩選來限制目錄中出現的啟用資源和學習路徑。 這是通過在站點的目錄資源實例上設定屬性來完成的。

使用啟用教學課程 [的範例](getting-started-enablement.md):

* 論作者
* 使用 [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * 例如 [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* 導覽至目錄頁面上的目錄資源

   * 例如， `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* 添加子篩選器節點

   * 選擇節 `catalog`點
   * 選擇 **[!UICONTROL 建立節點]**

      * 名稱: `filters`
      * 類型: `nt:unstructured`
   * 選擇「 **[!UICONTROL 全部保存」]**


* 向節 `se_resource-tags` 點添加屬 `filters` 性

   * 選擇節 `filters` 點
   * 新增多重屬性

      * 名稱: `se_resource-tags`
      * 類型：字串
      * 值： *&lt;輸入[TagID](#pre-filter-tagids)>*
      * 選擇 **[!UICONTROL 多]**
      * 選擇「添 **[!UICONTROL 加」]**

         * 在彈出式對話方塊中，選 `+` 取以新增其他預先篩選的TagID

* 重新發佈社群網站

![chlimage_1-189](assets/chlimage_1-189.png)

#### 預先篩選TagID {#pre-filter-tagids}

預先篩選的 [TagID](../../help/sites-developing/framework.md#tagid) 必須完全符合套用至啟用資源的標籤。 這些值在站點的 `resources` 資料夾中顯示為屬性值 `se_resource-tags`。

![chlimage_1-190](assets/chlimage_1-190.png)

### 參考API {#reference-apis}

* [啟用API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [報告API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [報告分析API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

