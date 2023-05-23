---
title: 遷移到Touch UI
seo-title: Migration to the Touch UI
description: 遷移到Touch UI
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

# 遷移到Touch UI{#migration-to-the-touch-ui}

從6.0版開始，Adobe Experience Manager(AEM)引入了稱為 *啟用觸摸的UI* (也稱為 *觸摸UI*)。 它與Adobe Marketing Cloud和整個Adobe用戶介面指南相一致。 這已成為標準UI,AEM其中的傳統、面向案頭的介面稱為 *經典UI*。

如果您一直在AEM使用經典UI，則需要採取措施遷移實例。 本頁旨在通過提供到單個資源的連結充當跳板。

>[!NOTE]
>
>此類遷移項目可能會對您的實例產生重大影響。 請參閱 [管理項目 — 最佳做法](/help/managing/best-practices.md) 建議的准則。

## 基礎 {#the-basics}

遷移時，您應注意到經典介面和觸摸介面之間的以下（主要）區別：

<table>
 <tbody>
  <tr>
   <td>傳統 UI</td>
   <td>啟用觸摸的UI</td>
  </tr>
  <tr>
   <td>在JCR儲存庫中將其描述為節點結構。 表示UI元素的每個節點都稱為 <em>ExtJS小部件</em> 在客戶端上呈現 <code>ExtJS</code>。</td>
   <td>在JCR儲存庫中也將其描述為節點結構。 但是，在這種情況下，每個節點都指Sling資源類型（Sling元件），負責其渲染。 所以UI（基本上）是呈現的伺服器端。</td>
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
     <li>使用監聽器直接嵌入命令部件或在客戶端中管理。</li>
    </ul> </td>
   <td><p>Javascript位置：</p>
    <ul>
     <li>必需部件不能嵌入對話定義；責任分離。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>事件處理：</p>
    <ul>
     <li>對話框小部件直接引用Javascript代碼。</li>
    </ul> </td>
   <td><p>事件處理：</p>
    <ul>
     <li>Javascript觀察對話事件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>客戶端完成的呈現：
    <ul>
     <li>客戶端動態建立UI元件。</li>
     <li>從伺服器發出的客戶端請求（拉）元件定義(JSON)。</li>
    </ul> </td>
   <td>由伺服器完成的呈現：
    <ul>
     <li>客戶端請求頁面以及相關的UI。</li>
     <li>伺服器將UI作為HTML文檔發送（推送）;使用Coral UI元件。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

換句話說，將UI的一部分從經典UI遷移到觸摸UI意味著 *ExtJS小部件* 到 *吊具元件*。 為了緩解這一問題，觸摸UI基於Granite UI框架，該框架已經為UI提供了一些Sling元件（稱為Granite UI元件）。

在開始之前，請檢查狀態和相關建議：

* [觸摸UI功能狀態](/help/release-notes/touch-ui-features-status.md)
* [面向客戶的用戶介面Recommendations](/help/sites-deploying/ui-recommendations.md)

開發觸摸UI的基礎將提供堅實的基礎：

* [啟用觸摸AEM的UI的概念](/help/sites-developing/touch-ui-concepts.md)
* [啟用觸摸AEM的UI的結構](/help/sites-developing/touch-ui-structure.md)

## 遷移頁面創作 {#migrating-page-authoring}

對話框是遷移元件時的主要因素：

* [開發組AEM件](/help/sites-developing/developing-components.md) （使用啟用觸摸的UI）
* [從經典元件遷移](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [現代化AEM工具](/help/sites-developing/modernization-tools.md)  — 幫助您將傳統UI元件的對話框轉換為觸摸UI

   * 在「觸摸UI包裝器」中，有一個相容層用於開啟標準UI對話框，但功能有限，因此長期不建議使用。

* [自定義Touch UI中的對話框欄位](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [建立新花崗岩UI欄位元件](/help/sites-developing/granite-ui-component.md)
* [自定義頁面創作](/help/sites-developing/customizing-page-authoring-touch.md) （使用啟用觸摸的UI）

## 遷移控制台 {#migrating-consoles}

您還可以定制控制台：

* [自定義控制台](/help/sites-developing/customizing-consoles-touch.md) （用於啟用觸摸的UI）

## 相關注意事項 {#related-considerations}

雖然與遷移到觸摸UI不直接相關，但有一些相關問題值得同時考慮，因為它們也是建議的做法：

* [模板](/help/sites-developing/templates.md) - [可編輯模板](/help/sites-developing/page-templates-editable.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)

>[!NOTE]
>
>另請參閱 [開發 — 最佳做法](/help/sites-developing/best-practices.md)。

## 更多資源 {#further-resources}

有關發展的全AEM部資訊，請參閱：

* [開發使用手冊](/help/sites-developing/home.md)
* [花崗岩UI文檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [6AEM.5站點Tutorials和視頻](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/overview.html)
* [開發 AEM Sites 快速入門 - WKND 教學課程](/help/sites-developing/getting-started.md)
* [寶石AEM](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html)
* [AEM 現代化工具](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>現AEM代化工具是社區工作，不受Adobe支援或授權。
