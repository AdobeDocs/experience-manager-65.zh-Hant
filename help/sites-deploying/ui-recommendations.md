---
title: 面向客戶的用戶介面Recommendations
seo-title: User Interface Recommendations for Customers
description: 與經典和觸控優化用戶介面相關的建議清單。
seo-description: A list of recommendations related to the classic and touch-optimized user interfaces.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# 面向客戶的用戶介面Recommendations{#user-interface-recommendations-for-customers}

Adobe Experience Manager提供了兩個UI — 統一Experience CloudUI（也稱為啟用觸摸的UI）和經典UI。

本文檔旨在指導客戶根據其情況選擇要使用的UI。

利息條款：

* **UI（或標準UI）**
5.6.0中引入的現代用戶介面作為技術預覽，並在後續版本中擴展。 它基於Adobe Experience Cloud的統一用戶體驗，以前稱為「觸摸式用戶介面」或「觸摸式用戶介面」。

* **經典UI**
2008年CQ 5.1引入的基於ExtJS技術的用戶介面。

* **站點管理**
用於管理站點層次結構（移動、激活、托管引用）和建立新頁面的功能。

* **頁面創作**
添加/編輯頁面內容的功能。

* **DAM/資產管理**
管理數字資產（包括影像、視頻、文檔、下載）的功能。

* **上下文中心**
聚合訪問者資訊並將其用於各種目的的功能。 提供用戶介面以模擬訪問站點的人員。 從AEM6.2開始，ContextHub取代了以前的技術Client Context。

## 一般 {#general}

在過去幾年中，Adobe使用統一的用戶介面更新了所有Adobe Experience Cloud解決方案。 Experience Cloud解決方案中的用戶在如何使用和操作應用程式方面擁有共同的模式，從而獲得一致的體驗。 在每一版本中，Adobe都根據客戶對各種解決方案的反饋改進了它的用戶介面。

2008年推出的、由運行5.0-5.6.1版的客戶使用的Adobe Experience Manager（以前稱為CQ5）的原始用戶介面在AEM6.5中提供。這保證客戶可以更新到6.5，並受益於具有新功能的更新平台，同時繼續使用相同的用戶介面。

Adobe建議客戶計畫在2018/19年度切換到新用戶介面。 這可以在6.5的更新期間完成，也可以在更新後的單獨項目中完成，其中包括對自定義項和元件對話框進行必要的調整。

Classic UI已棄用，AEM帶有6.4，而Adobe不打算對Classic UI進行進一步增強。 請注意，不建議使用時，Classic UI仍完全受支援。

### 規則與Recommendations {#rules-and-recommendations}

以下是產品管理部門為Adobe Experience Manager6.5提出的建議清單：

<table>
 <tbody>
  <tr>
   <th>我的項目……</th>
   <th>建議</th>
  </tr>
  <tr>
   <td>才剛開始使用Adobe Experience Manager。</td>
   <td>使用預設UI。</td>
  </tr>
  <tr>
   <td><p>已經AEM有段時間了。</p> <p>已使用產品UI開箱即用，並為站點開發了自定義元件。<br /> </p> </td>
   <td>
    <ol>
     <li>更新為6.5</li>
     <li>使用預設UI進行站點管理、資產、 ... 等。<br /> </li>
     <li>配置「編輯頁面」操作以開啟經典UI頁面編輯器。 請參閱 <a href="#selecting-your-ui">選擇UI</a>。</li>
    </ol> <p>然後，在第二階段：</p>
    <ol>
     <li>更新元件對話框以使用Coral 3對話框格式。 Adobe建議使用 <a href="/help/sites-developing/modernization-tools.md">現代化AEM工具</a> 以更新元件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>已構建一個使用整合ClientContext的站點。<br /> </td>
   <td>
    <ol>
     <li>更新為6.5</li>
     <li>使用預設UI進行站點管理、資產、 ... 等。</li>
     <li>配置「編輯頁面」操作以開啟經典UI頁面編輯器。 請參閱 <a href="#selecting-your-ui">選擇UI</a>。</li>
    </ol> <p>然後，在第二階段：</p>
    <ol>
     <li>更新元件對話框以使用Coral 3對話框格式。 Adobe建議使用 <a href="/help/sites-developing/modernization-tools.md">現代化AEM工具</a> 以更新元件。</li>
     <li>配置ContextHub(ClientContext的替換項)並更新頁面模板以使用ContextHub。 請注意，ContextHub具有允許載入自定義ClientContext儲存的相容模式。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>已使用CQ/AEM多年。</p> <p>擴展了產品UI（如站點管理）並構建了包含大量編輯對話框的元件。</p> </td>
   <td><p>更新到6.5並將標準UI配置為所有用戶的頁面創作的預設UI。 請參閱 <a href="#selecting-your-ui">選擇UI</a>。</p> <p>然後啟動一個項目以應用Coral 3格式的自定義和優化元件對話框。 請參閱 <a href="#resources-to-help">要幫助的資源</a>。<br /> </p> </td>
  </tr>
 </tbody>
</table>

### 常見問題集 {#faq}

請參閱知識庫文章， [觸摸UI創作常見問題](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html)，以獲取詳細資訊。包括有關經典UI的棄用計畫的任何資訊。

### 選擇UI {#selecting-your-ui}

請參閱 [選擇UI](/help/sites-authoring/select-ui.md) 以獲取有關根據需要配置系統的資訊。

### 啟用觸摸的UI狀態 {#touch-enabled-ui-status}

有關6.5中對啟用觸摸的UI進行增強的詳細信AEM息，請參閱 [新增功能](/help/release-notes/release-notes.md#what-s-new) 的上界。

完整概述請參閱 [觸摸UI功能狀態](/help/release-notes/touch-ui-features-status.md) 頁

### 要幫助的資源 {#resources-to-help}

有關基本處理的背景資訊：

* [創作頁面](/help/sites-authoring/page-authoring.md)。

有關詳細開發資訊：

* [支援觸摸的UI體系結構](/help/sites-developing/touch-ui-concepts.md)。
* 使用 [現代化AEM工具](/help/sites-developing/modernization-tools.md) 將元件「編輯」對話框從傳統UI轉換為啟用觸摸的UI。

* [啟用觸摸的UI的結構](/help/sites-developing/touch-ui-structure.md)。

* [在啟用觸摸的UI中自定義控制台](/help/sites-developing/customizing-consoles-touch.md) （包括示例代碼）。

* [在啟用觸摸的UI中自定義頁面創作](/help/sites-developing/customizing-page-authoring-touch.md) （包括示例代碼）。

* [花崗岩用戶介面文檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。
