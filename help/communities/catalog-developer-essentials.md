---
title: 目錄要點
seo-title: Catalog Essentials
description: 目錄概述
seo-description: Catalog overview
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 2%

---

# 目錄要點 {#catalog-essentials}

本頁面提供使用啟用社群網站目錄功能的基本資訊。

目錄功能包含在社群網站中時，可讓社群成員瀏覽並選取目錄中列出的啟用資源。

此 [ `enablement catalog` 元件](catalog.md) 允許社區成員訪問 [啟用資源](resources.md). 使用AEM標籤是管理目錄中啟用資源外觀的重要部分。

請參閱 [標籤啟用資源](tag-resources.md).

## 用戶端的要點 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包括</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.beadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>範本</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>cs</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> 屬性</strong></td>
   <td>請參閱 <a href="catalog.md">目錄功能</a></td>
  </tr>
 </tbody>
</table>

## 伺服器端的Essentials {#essentials-for-server-side}

### 目錄功能 {#catalog-function}

包含 [目錄函式](functions.md#catalog-function)，包含已設定的 `enablement catalog` 元件。

### 預先篩選 {#pre-filters}

將目錄功能新增至社群網站後，您可以指定預先篩選，以限制目錄中出現的啟用資源和學習路徑。 若要這麼做，請在網站目錄資源的例項上設定屬性。

使用 [啟用教學課程](getting-started-enablement.md):

* 論作者
* 使用 [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * 例如 [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* 導覽至目錄頁面上的目錄資源

   * 例如， `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* 添加子篩選器節點

   * 選取 `catalog`節點
   * 選擇 **[!UICONTROL 建立節點]**

      * 名稱: `filters`
      * 類型: `nt:unstructured`
      * 選擇 **[!UICONTROL 全部儲存]**

* 新增 `se_resource-tags` 屬性 `filters` 節點

   * 選取 `filters` 節點
   * 新增多重屬性

      * 名稱: `se_resource-tags`
      * 類型：字串
      * 值： *&lt;enter a=&quot;&quot; span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; />TagID](#pre-filter-tagids)>*[
         * 選擇 **[!UICONTROL 多]**
         * 選擇 **[!UICONTROL 新增]**

            * 在彈出式對話方塊中，選取 `+` 新增其他預先篩選TagID的方式

* 重新發佈社群網站

![configure-catalog](assets/configure-catalog.png)

#### 預先篩選TagID {#pre-filter-tagids}

預先篩選 [TagIDs](../../help/sites-developing/framework.md#tagid) 必須完全符合套用至啟用資源的標籤。 這些項目會顯示在 `resources` 資料夾，作為屬性的值 `se_resource-tags`.

![設定篩選器](assets/configure-catalog1.png)

### 參考API {#reference-apis}

* [啟用API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [報表API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [報表分析API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
