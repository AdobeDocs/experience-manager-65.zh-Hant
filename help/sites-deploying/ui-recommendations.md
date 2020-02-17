---
title: 客戶的使用者介面建議
seo-title: 客戶的使用者介面建議
description: 與傳統和觸控最佳化使用者介面相關的建議清單。
seo-description: 與傳統和觸控最佳化使用者介面相關的建議清單。
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# 客戶的使用者介面建議{#user-interface-recommendations-for-customers}

Adobe Experience manager提供兩個UI —— 統一的Experience Cloud UI（也稱為觸控式UI）和Classic UI。

本檔案旨在引導客戶根據其情況選擇要使用的UI。

利息條款：

* **UI（或標準UI）** 5.6.0版中引進的現代化使用者介面，在後續版本中提供技術預覽和擴充。 它以Adobe Experience cloud的統一使用者體驗為基礎，Adobe Experience cloud先前稱為觸控式UI或觸控式UI。

* **2008年** CQ 5.1版引入的基於ExtJS技術的經典UI用戶介面。

* **網站管理**&#x200B;功能：管理網站階層（移動、啟用、管理的參考）並建立新頁面。

* **頁面編**&#x200B;寫功能，以新增／編輯頁面內容。

* **DAM/資產管理**&#x200B;功能，以管理數位資產（包括影像、視訊、檔案、下載）。

* **ContextHub** Capabilities，可匯整訪客的相關資訊，並用於各種用途。 提供使用者介面來模擬造訪網站的人員。 從AEM 6.2開始，ContextHub取代了先前的技術「用戶端內容」。

## 一般 {#general}

過去幾年中，Adobe以統一的使用者介面更新了所有Adobe Experience cloud解決方案。 Experience cloud解決方案的使用者在如何使用和操作應用程式時，都能享有一致的使用體驗。 在每個版本中，Adobe都根據客戶對各種解決方案的意見回應，來改善其使用者介面。

AEM 6.5中提供Adobe Experience Manager（先前稱為CQ5）的原始使用者介面，此介面於2008年推出，供執行5.0-5.6.1版的客戶使用。這可確保客戶可更新至6.5版，並受益於具備新功能的更新平台，同時仍能使用相同的使用者介面。

Adobe建議客戶在2018/19年度計畫改用新的UI。 這可在6.5版的更新期間完成，或在更新後的個別專案中完成，其中包括對自訂和元件對話方塊進行必要的調整。

Classic UI已在AEM 6.4中停用，而Adobe不打算對Classic UI進一步增強。 請注意，Classic UI在遭淘汰時仍完全受支援。

### 規則與建議 {#rules-and-recommendations}

以下是Adobe Experience Manager 6.5產品管理的建議清單：

<table>
 <tbody>
  <tr>
   <th>我的專案……</th>
   <th>建議</th>
  </tr>
  <tr>
   <td>Adobe Experience Manager才剛剛開始使用。</td>
   <td>使用預設的UI。</td>
  </tr>
  <tr>
   <td><p>已使用AEM一段時間。</p> <p>已使用產品現成可用的UI，並開發網站的自訂元件。<br /> </p> </td>
   <td>
    <ol>
     <li>更新至6.5</li>
     <li>使用預設的UI進行網站管理、資產、 等等。<br /> </li>
     <li>設定「編輯頁面」動作以開啟傳統UI頁面編輯器。 請參 <a href="#selecting-your-ui">閱選擇您的UI</a>。</li>
    </ol> <p>然後，在第二個階段：</p>
    <ol>
     <li>更新元件對話方塊，以使用Coral 3對話方塊格式。 Adobe建議使用對 <a href="/help/sites-developing/dialog-conversion.md">話轉換工具</a> ，以更新元件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>已建立使用ClientContext與整合的網站。<br /> </td>
   <td>
    <ol>
     <li>更新至6.5</li>
     <li>使用預設的UI進行網站管理、資產、 等等。</li>
     <li>設定「編輯頁面」動作以開啟傳統UI頁面編輯器。 請參 <a href="#selecting-your-ui">閱選擇您的UI</a>。</li>
    </ol> <p>然後，在第二個階段：</p>
    <ol>
     <li>更新元件對話方塊，以使用Coral 3對話方塊格式。 Adobe建議使用對 <a href="/help/sites-developing/dialog-conversion.md">話轉換工具</a> ，以更新元件。</li>
     <li>設定ContextHub（ClientContext的取代）並更新頁面範本以使用ContextHub。 請注意，ContextHub具有允許載入自訂ClientContext儲存區的相容性模式。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>已使用CQ/AEM多年。</p> <p>已擴充產品UI（例如網站管理員），並建立包含廣泛編輯對話方塊的元件。</p> </td>
   <td><p>更新至6.5，並將傳統UI設定為所有使用者的頁面編寫預設值。 請參 <a href="#selecting-your-ui">閱選擇您的UI</a>。</p> <p>然後開始專案，以套用自訂並最佳化Coral 3格式的元件對話方塊。 請參 <a href="#resources-to-help">閱說明資源</a>。<br /> </p> </td>
  </tr>
 </tbody>
</table>

### 常見問答集 {#faq}

如需詳細資訊，請參閱知識 [庫文章Touch UI Authoring常見問答集](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html);包括有關傳統UI淘汰排程的任何資訊。

### 選擇您的UI {#selecting-your-ui}

如需 [要設定系統的相關資訊](/help/sites-authoring/select-ui.md) ，請參閱選取您的UI。

### 啟用觸控的UI狀態 {#touch-enabled-ui-status}

如需AEM 6.5中觸控式UI增強功能的詳細資訊，請參閱「 [發行說明中的新增功能](/help/release-notes/release-notes.md#what-s-new) 」。

完整概述，請參閱「 [Touch UI Feature Status」頁](/help/release-notes/touch-ui-features-status.md) 。

### 說明資源 {#resources-to-help}

有關基本處理的背景資訊：

* [編寫頁面](/help/sites-authoring/page-authoring.md)。

如需詳細的開發資訊：

* [可觸控的UI架構](/help/sites-developing/touch-ui-concepts.md)。
* 使用「 [對話方塊轉換](/help/sites-developing/dialog-conversion.md) 」工具，將元件「編輯」對話方塊從傳統UI轉換為觸控式UI。

* [觸控式UI的結構](/help/sites-developing/touch-ui-structure.md)。

* [在觸控式UI中自訂控制台](/help/sites-developing/customizing-consoles-touch.md) （包含范常式式碼）。

* [在觸控式UI中自訂頁面製作](/help/sites-developing/customizing-page-authoring-touch.md) （包含范常式式碼）。

* [AEM Gem Session on touch-enabled customization](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).
* [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。

