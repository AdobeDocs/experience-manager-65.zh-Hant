---
title: 客戶適用的使用者介面Recommendations
description: 和傳統及觸控最佳化使用者介面相關的建議清單。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 客戶適用的使用者介面Recommendations{#user-interface-recommendations-for-customers}

Adobe Experience Manager提供兩個UI — 統一的Experience CloudUI （也稱為觸控式UI）和傳統UI。

本檔案旨在引導客戶根據其情況選擇要使用的UI。

興趣條款：

* **UI （或標準UI）**
在5.6.0中引入作為技術預覽的現代使用者介面，並在後續發行版本中進行擴展。 這是以Adobe Experience Cloud的統一使用者體驗為基礎，先前稱為觸控式UI或觸控式UI。

* **傳統UI**
以ExtJS技術為基礎的使用者介面，此技術於2008年隨CQ 5.1推出。

* **網站管理員**
管理場地階層（移動、啟動、受管理的參照）和建立新頁面的功能。

* **頁面製作**
新增/編輯頁面內容的功能。

* **DAM/Assets管理員**
管理數位資產（包括影像、影片、檔案和下載）的功能。

* **ContextHub**
彙總訪客相關資訊並將其用於各種用途的功能。 提供使用者介面來模擬造訪網站的人。 從AEM 6.2開始，ContextHub取代舊版技術Client Context。

## 一般 {#general}

過去幾年，Adobe已更新所有Adobe Experience Cloud解決方案，並具備統一的使用者介面。 整個Experience Cloud解決方案的使用者都能透過使用與操作應用程式的共同模式，獲得一致的體驗。 在每次發行中，Adobe都會根據客戶在各種解決方案中的意見回饋，改進其使用者介面。

Adobe Experience Manager （先前稱為CQ5）的原始使用者介面於2008年推出，供執行5.0-5.6.1版本的客戶使用，現在位於AEM 6.5中。這可保證客戶可更新至6.5版，並可獲益於具有新功能的更新平台，同時繼續使用相同的使用者介面。

Adobe建議客戶在2018/19年度計畫切換至新的UI。 這可以在6.5更新期間完成，或者在更新後的單獨專案中完成，這將包括對自訂和元件對話方塊的必要調整。

Classic UI已透過AEM 6.4棄用，Adobe不打算進一步增強Classic UI。 請注意，傳統UI在被取代時仍完全受支援。

### 規則與Recommendations {#rules-and-recommendations}

以下是來自Adobe Experience Manager 6.5產品管理的建議清單：

<table>
 <tbody>
  <tr>
   <th>我的專案……</th>
   <th>建議</th>
  </tr>
  <tr>
   <td>剛開始使用Adobe Experience Manager。</td>
   <td>使用預設的UI。</td>
  </tr>
  <tr>
   <td><p>已使用AEM一段時間。</p> <p>使用現成可用的產品UI，並為網站開發自訂元件。<br /> </p> </td>
   <td>
    <ol>
     <li>更新至6.5</li>
     <li>使用預設UI進行網站管理、資產…… 等等。<br /> </li>
     <li>設定「編輯頁面」動作以開啟傳統UI頁面編輯器。 另請參閱 <a href="#selecting-your-ui">選取您的UI</a>.</li>
    </ol> <p>然後，在第二階段：</p>
    <ol>
     <li>更新您的元件對話方塊，以使用Coral 3對話方塊格式。 Adobe建議使用 <a href="/help/sites-developing/modernization-tools.md">AEM現代化工具</a> 以更新元件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>已建立一個使用ClientContext與整合的網站。<br /> </td>
   <td>
    <ol>
     <li>更新至6.5</li>
     <li>使用預設UI進行網站管理、資產…… 等等。</li>
     <li>設定「編輯頁面」動作以開啟傳統UI頁面編輯器。 另請參閱 <a href="#selecting-your-ui">選取您的UI</a>.</li>
    </ol> <p>然後，在第二階段：</p>
    <ol>
     <li>更新您的元件對話方塊，以使用Coral 3對話方塊格式。 Adobe建議使用 <a href="/help/sites-developing/modernization-tools.md">AEM現代化工具</a> 以更新元件。</li>
     <li>設定ContextHub (取代ClientContext)並更新頁面範本，以使用ContextHub。 ContextHub的相容性模式允許載入自訂ClientContext存放區。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>已使用CQ/AEM許多年。</p> <p>已擴充產品UI （例如網站管理員），並建立具有大量編輯對話方塊的元件。</p> </td>
   <td><p>更新至6.5，並將傳統UI設定為所有使用者的頁面編寫預設值。 另請參閱 <a href="#selecting-your-ui">選取您的UI</a>.</p> <p>然後啟動專案以套用自訂並最佳化Coral 3格式的元件對話方塊。 另請參閱 <a href="#resources-to-help">需要說明的資源</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### 常見問題集 {#faq}

請參閱知識庫文章， [Touch UI編寫常見問題集](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html)，以取得詳細資訊；包括傳統UI淘汰排程的任何相關資訊。

### 選取您的UI {#selecting-your-ui}

另請參閱 [選取您的UI](/help/sites-authoring/select-ui.md) 以取得視需要設定系統的相關資訊。

### 觸控式UI狀態 {#touch-enabled-ui-status}

如需AEM 6.5觸控式UI增強功能的詳細資訊，請參閱 [新增功能](/help/release-notes/release-notes.md#what-s-new) 發行說明中的。

完整的概觀請參閱 [觸控式UI功能狀態](/help/release-notes/touch-ui-features-status.md) 頁面

### 需要說明的資源 {#resources-to-help}

如需基本處理的背景資訊：

* [製作頁面](/help/sites-authoring/page-authoring.md).

如需詳細的開發資訊：

* [觸控式UI架構](/help/sites-developing/touch-ui-concepts.md).
* 使用 [AEM現代化工具](/help/sites-developing/modernization-tools.md) 將元件「編輯」對話方塊從傳統UI轉換為觸控式UI。

* [觸控式UI的結構](/help/sites-developing/touch-ui-structure.md).

* [在觸控式UI中自訂主控台](/help/sites-developing/customizing-consoles-touch.md) （包含範常式式碼）。

* [在觸控式UI中自訂頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md) （包含範常式式碼）。

* [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
