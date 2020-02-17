---
title: 移轉至Touch UI
seo-title: 移轉至Touch UI
description: 移轉至Touch UI
seo-description: 移轉至Touch UI
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# 移轉至Touch UI{#migration-to-the-touch-ui}

從6.0版開始，Adobe Experience Manager(AEM)推出新的使用者介面，稱為觸控式 *UI* (也稱為 *觸控式UI*)。 它符合Adobe Marketing cloud和整體Adobe使用者介面准則。 這已成為AEM中的標準UI，其舊版案頭導向介面稱為 *傳統UI*。

如果您已將AEM與傳統UI搭配使用，您將需要採取行動來移轉您的例項。 本頁提供個別資源的連結，以做為跳板。

>[!NOTE]
>
>此類移轉專案可能會對您的執行個體產生重大影響。 如需 [建議的准則，請參閱管理專案](/help/managing/best-practices.md) -最佳實務。

## 基本概念 {#the-basics}

移轉時，您應注意到傳統UI和觸控UI之間的下列（主要）差異：

<table>
 <tbody>
  <tr>
   <td>傳統 UI</td>
   <td>觸控式UI</td>
  </tr>
  <tr>
   <td>在JCR儲存庫中將其描述為節點的結構。 每個代表UI元素的節點都稱為 <em>ExtJS介面工具集</em> ，並由用戶端呈現 <code>ExtJS</code>。</td>
   <td>在JCR儲存庫中也將其描述為節點結構。 不過，在此範例中，每個節點都會參照Sling資源類型（Sling元件），負責其演算。 因此，UI（基本上）是在伺服器端轉換。</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>未使用</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>已使用</li>
     <li>例如<br /><code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>對話框節點：</p>
    <ul>
     <li>名稱: <code>dialog</code></li>
     <li>jcr:primaryType: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>對話框節點：</p>
    <ul>
     <li>名稱: <code>cq:dialog</code></li>
     <li>jcr:primaryType: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Javascript位置：</p>
    <ul>
     <li>必要部件是使用偵聽器直接嵌入的，或是在clientlibs中管理的。</li>
    </ul> </td>
   <td><p>Javascript位置：</p>
    <ul>
     <li>必要部件不能嵌入對話定義中；職責分離。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件處理：</p>
    <ul>
     <li>對話介面工具集直接參考Javascript程式碼。</li>
    </ul> </td>
   <td><p>事件處理：</p>
    <ul>
     <li>Javascript會觀察對話事件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>由用戶端完成演算：
    <ul>
     <li>用戶端會動態建立UI元件。</li>
     <li>從伺服器要求（提取）元件定義(JSON)。</li>
    </ul> </td>
   <td>由伺服器完成演算：
    <ul>
     <li>用戶端會要求頁面及相關的UI。</li>
     <li>伺服器將UI以HTML檔案傳送（推送）;使用Coral UI元件。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

換言之，將您UI的區段從傳統UI移轉至觸控UI意味著將 *ExtJS Widget* 移植至 *Sling元件*。 為方便使用，觸控UI是以Granite UI架構為基礎，此架構已針對UI提供一些Sling元件（稱為Granite UI元件）。

開始之前，請檢查狀態和相關建議：

* [Touch UI功能狀態](/help/release-notes/touch-ui-features-status.md)
* [客戶的使用者介面建議](/help/sites-deploying/ui-recommendations.md)

開發觸控式UI的基本功能將提供穩固的基礎：

* [AEM Touch-Enabled UI的概念](/help/sites-developing/touch-ui-concepts.md)
* [AEM Touch-Enabled UI的結構](/help/sites-developing/touch-ui-structure.md)

## 移轉頁面編寫 {#migrating-page-authoring}

對話方塊是移轉元件時的主要因素：

* [開發AEM元件](/help/sites-developing/developing-components.md) （使用觸控式UI）
* [從傳統元件遷移](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [對話方塊轉換工具](/help/sites-developing/dialog-conversion.md) -協助您將傳統UI元件的對話方塊轉換為觸控UI

   * 觸控UI中有相容層，可在「觸控UI包裝函式」中開啟傳統UI對話方塊，但功能有限，長期而言不建議使用。

* [自訂Touch UI中的對話方塊欄位](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [建立新的Granite UI欄位元件](/help/sites-developing/granite-ui-component.md)
* [自訂頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md) （使用啟用觸控的UI）

## 遷移控制台 {#migrating-consoles}

您也可以自訂控制台：

* [自訂控制台](/help/sites-developing/customizing-consoles-touch.md) （適用於觸控式UI）

## 相關考量事項 {#related-considerations}

雖然與移轉至觸控式使用者介面並非直接相關，但有一些相關問題值得同時考慮，因為這些問題也是建議的作法：

* [範本](/help/sites-developing/templates.md) -可編 [輯的範本](/help/sites-developing/page-templates-editable.md)
* [核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)

>[!NOTE]
>
>另請參閱 [開發——最佳做法](/help/sites-developing/best-practices.md)。

## 更多資源 {#further-resources}

如需開發AEM的完整資訊，請參閱以下資源收集：

* [開發使用指南](/help/sites-developing/home.md)
* [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5網站教學課程與影片](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/overview.html)
* [開始開發AEM網站- WKND教學課程](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM Meduration Tools](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM現代化工具是社群的努力，Adobe不支援或保證。

