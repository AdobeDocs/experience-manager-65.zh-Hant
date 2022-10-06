---
title: 適用於客戶的使用者介面Recommendations
seo-title: User Interface Recommendations for Customers
description: 與傳統和觸控最佳化使用者介面相關的建議清單。
seo-description: A list of recommendations related to the classic and touch-optimized user interfaces.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# 適用於客戶的使用者介面Recommendations{#user-interface-recommendations-for-customers}

Adobe Experience Manager隨附兩個UI：統一的Experience CloudUI（也稱為觸控式UI）和傳統UI。

本檔案旨在引導客戶根據其情況選擇要使用的UI。

利息條款：

* **UI（或標準UI）**
5.6.0導入的現代使用者介面是技術預覽，並在後續版本中延伸。 它以Adobe Experience Cloud的統一使用者體驗為基礎，先前稱為觸控式UI或觸控式UI。

* **傳統UI**
2008年CQ 5.1推出的基於ExtJS技術的使用者介面。

* **網站管理員**
管理網站階層（移動、啟動、管理的參考）和建立新頁面的功能。

* **頁面編寫**
新增/編輯頁面內容的功能。

* **DAM/資產管理員**
管理數位資產（包括影像、視訊、檔案、下載）的功能。

* **ContextHub**
可匯總訪客的相關資訊，並用於各種用途的功能。 提供用於模擬訪問站點的人員的用戶介面。 自AEM 6.2起，ContextHub已取代先前的技術「用戶端內容」。

## 一般 {#general}

過去幾年來，Adobe已使用統一的使用者介面更新所有Adobe Experience Cloud解決方案。 Experience Cloud解決方案的使用者在如何使用和操作應用程式方面，都能享有一致的常見模式體驗。 在每個版本中，Adobe都根據客戶在各種解決方案中提供的意見回饋，完善了其使用者介面。

AEM 6.5中提供原始的Adobe Experience Manager使用者介面（先前稱為CQ5）（於2008年推出，供執行5.0至5.6.1版的客戶使用）。這可保證客戶可更新至6.5版，並受益於具有新功能的更新平台，同時持續使用相同的使用者介面。

Adobe建議客戶在2018/19年度計畫改用新的UI。 這可在6.5版的更新期間完成，或在更新後的個別專案中完成，包括對自訂項目和元件對話方塊進行必要的調整。

AEM 6.4已淘汰傳統UI，且Adobe不打算對傳統UI進一步增強。 請注意，舊版UI仍完全受支援。

### 規則與Recommendations {#rules-and-recommendations}

以下為Adobe Experience Manager 6.5產品管理的建議清單：

<table>
 <tbody>
  <tr>
   <th>我的項目……</th>
   <th>建議</th>
  </tr>
  <tr>
   <td>才開始使用Adobe Experience Manager。</td>
   <td>使用預設UI。</td>
  </tr>
  <tr>
   <td><p>已使用AEM一段時間。</p> <p>已使用產品UI現成可用，並為網站開發自訂元件。<br /> </p> </td>
   <td>
    <ol>
     <li>更新至6.5</li>
     <li>使用網站管理、資產、的預設UI。 等。<br /> </li>
     <li>設定「編輯頁面」動作，以開啟傳統UI頁面編輯器。 請參閱 <a href="#selecting-your-ui">選取您的UI</a>.</li>
    </ol> <p>然後，在第二階段：</p>
    <ol>
     <li>更新元件對話方塊，使用Coral 3對話方塊格式。 Adobe建議使用 <a href="/help/sites-developing/modernization-tools.md">AEM現代化工具</a> 以更新元件。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>已建立網站，透過整合使用ClientContext。<br /> </td>
   <td>
    <ol>
     <li>更新至6.5</li>
     <li>使用網站管理、資產、的預設UI。 等。</li>
     <li>設定「編輯頁面」動作，以開啟傳統UI頁面編輯器。 請參閱 <a href="#selecting-your-ui">選取您的UI</a>.</li>
    </ol> <p>然後，在第二階段：</p>
    <ol>
     <li>更新元件對話方塊，使用Coral 3對話方塊格式。 Adobe建議使用 <a href="/help/sites-developing/modernization-tools.md">AEM現代化工具</a> 以更新元件。</li>
     <li>設定ContextHub(取代ClientContext)並更新頁面範本以使用ContextHub。 請注意，ContextHub具有可載入自訂ClientContext存放區的相容模式。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>已使用CQ/AEM多年。</p> <p>已擴充產品UI（例如網站管理員）並建置元件，提供廣泛的編輯對話方塊。</p> </td>
   <td><p>更新至6.5，並將傳統UI設為所有使用者的頁面編寫預設UI。 請參閱 <a href="#selecting-your-ui">選取您的UI</a>.</p> <p>接著，啟動專案以套用自訂，並以Coral 3格式最佳化元件對話方塊。 請參閱 <a href="#resources-to-help">協助資源</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### 常見問題集 {#faq}

請參閱知識庫文章， [Touch UI編寫常見問題集](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html)，以取得詳細資訊；包括傳統UI淘汰排程的任何相關資訊。

### 選取您的UI {#selecting-your-ui}

請參閱 [選取您的UI](/help/sites-authoring/select-ui.md) ，以獲得有關根據需要配置系統的資訊。

### 觸控式UI狀態 {#touch-enabled-ui-status}

如需AEM 6.5中觸控式UI所增強功能的詳細資訊，請參閱 [新增功能](/help/release-notes/release-notes.md#what-s-new) 中。

完整概述請參閱 [觸控式UI功能狀態](/help/release-notes/touch-ui-features-status.md) 頁面

### 協助資源 {#resources-to-help}

有關基本處理的背景資訊：

* [編寫頁面](/help/sites-authoring/page-authoring.md).

有關詳細開發資訊：

* [觸控式UI架構](/help/sites-developing/touch-ui-concepts.md).
* 使用 [AEM現代化工具](/help/sites-developing/modernization-tools.md) 若要將元件「編輯」對話方塊從傳統UI轉換為觸控式UI。

* [觸控式UI的結構](/help/sites-developing/touch-ui-structure.md).

* [在觸控式UI中自訂主控台](/help/sites-developing/customizing-consoles-touch.md) （包含范常式式碼）。

* [在觸控式UI中自訂頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md) （包含范常式式碼）。

* [AEM Gem接觸式自訂課程](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).
* [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
