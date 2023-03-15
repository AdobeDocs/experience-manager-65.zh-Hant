---
title: 移轉至Touch UI
seo-title: Migration to the Touch UI
description: 移轉至Touch UI
seo-description: Migration to the Touch UI
uuid: 47c43b56-532b-4ada-8503-04d66bab3564
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: b315720f-e9b8-4063-99e2-1b9aa6bba460
docset: aem65
exl-id: 33dc1ee7-1e34-43d8-9265-c66535f5e002
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 4%

---

# 移轉至Touch UI{#migration-to-the-touch-ui}

從6.0版開始，Adobe Experience Manager(AEM)推出新的使用者介面，稱為 *觸控式UI* (也簡稱為 *觸控式UI*)。 它符合Adobe Marketing Cloud和整體Adobe使用者介面准則。 這已成為AEM中的標準UI，其舊版案頭導向介面稱為 *傳統UI*.

如果您一直將AEM與傳統UI搭配使用，則需採取動作來移轉執行個體。 本頁面旨在提供個別資源的連結，以作為跳板。

>[!NOTE]
>
>這類移轉專案可能會對您的執行個體造成重大影響。 請參閱 [管理專案 — 最佳實務](/help/managing/best-practices.md) 供建議的指引使用。

## 基本概念 {#the-basics}

移轉時，請注意傳統和觸控式UI之間的下列（主要）差異：

<table>
 <tbody>
  <tr>
   <td>傳統 UI</td>
   <td>觸控式UI</td>
  </tr>
  <tr>
   <td>在JCR存放庫中以節點結構形式說明。 代表UI元素的每個節點都稱為 <em>ExtJS Widget</em> 並在用戶端上呈現 <code>ExtJS</code>.</td>
   <td>在JCR存放庫中也以節點結構的形式說明。 不過，在此案例中，每個節點都會參照Sling資源類型（Sling元件），負責其轉譯。 因此UI（基本上）是在伺服器端轉譯。</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>未使用</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>已使用</li>
     <li>例如<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
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
     <li>必要部件是使用偵聽器直接嵌入的，或在clientlibs中進行管理。</li>
    </ul> </td>
   <td><p>Javascript位置：</p>
    <ul>
     <li>必要部件不能嵌入對話定義中；責任分離。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件處理：</p>
    <ul>
     <li>對話方塊小工具會直接參考Javascript程式碼。</li>
    </ul> </td>
   <td><p>事件處理：</p>
    <ul>
     <li>Javascript會觀察對話事件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>由用戶端完成的呈現：
    <ul>
     <li>用戶端會動態建立UI元件。</li>
     <li>從伺服器取得用戶端要求（提取）元件定義（如JSON）。</li>
    </ul> </td>
   <td>伺服器完成的呈現：
    <ul>
     <li>用戶端會連同相關UI一起要求頁面。</li>
     <li>伺服器傳送（推送）UI作為HTML檔案；使用Coral UI元件。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

換句話說，將UI的區段從傳統UI移轉至觸控式UI，表示會移植 *ExtJS Widget* 到 *Sling元件*. 為方便使用，觸控式UI以Granite UI架構為基礎，此架構已為UI提供一些Sling元件（稱為Granite UI元件）。

開始之前，請檢查狀態和相關建議：

* [觸控式UI功能狀態](/help/release-notes/touch-ui-features-status.md)
* [適用於客戶的使用者介面Recommendations](/help/sites-deploying/ui-recommendations.md)

開發觸控式UI的基本基礎將提供堅實的基礎：

* [AEM觸控式UI的概念](/help/sites-developing/touch-ui-concepts.md)
* [AEM觸控式UI的結構](/help/sites-developing/touch-ui-structure.md)

## 移轉頁面編寫 {#migrating-page-authoring}

對話方塊是移轉元件時的主要因素：

* [開發AEM元件](/help/sites-developing/developing-components.md) （使用觸控式UI）
* [從傳統元件移轉](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [AEM現代化工具](/help/sites-developing/modernization-tools.md)  — 協助您將傳統UI元件的對話方塊轉換為觸控式UI

   * 觸控式UI中有相容層，可在「觸控式UI包裝函式」中開啟傳統UI對話方塊，但此功能有限，長期而言不建議使用。

* [在觸控式UI中自訂對話方塊欄位](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [建立新的Granite UI欄位元件](/help/sites-developing/granite-ui-component.md)
* [自訂頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md) （使用觸控式UI）

## 移轉主控台 {#migrating-consoles}

您也可以自訂主控台：

* [自訂主控台](/help/sites-developing/customizing-consoles-touch.md) （適用於觸控式UI）

## 相關考量事項 {#related-considerations}

雖然與移轉至觸控式UI並非直接相關，但有相關問題需同時考慮，因為也是建議的作法：

* [範本](/help/sites-developing/templates.md) - [可編輯的範本](/help/sites-developing/page-templates-editable.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)

>[!NOTE]
>
>另請參閱 [開發 — 最佳實務](/help/sites-developing/best-practices.md).

## 更多資源 {#further-resources}

如需開發AEM的完整資訊，請參閱下列資源收集：

* [開發使用手冊](/help/sites-developing/home.md)
* [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [AEM 6.5 SitesTutorials和影片](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/overview.html)
* [開發 AEM Sites 快速入門 - WKND 教學課程](/help/sites-developing/getting-started.md)
* [AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM 現代化工具](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>AEM現代化工具是社群的努力成果，不受Adobe支援或保固。
