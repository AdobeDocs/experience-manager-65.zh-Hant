---
title: 幫助管理員啟動和運行的最佳做法
description: 查找由Adobe工程和咨詢團隊編製的最佳實踐，以幫助管理員啟動並運行。
uuid: 862d4fcf-ca61-4228-9344-b95a49b59b32
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f6468a0-7721-454f-9334-c449968b8fe7
exl-id: 576d87c8-cc96-45a0-b3cf-defb440babbb
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 7%

---

# 最佳做法{#best-practices}

最佳做法描述了如何以盡可能最高效和最AEM有效的方式開發、管理或使用。 這個不斷增加的主題清單包括了多個AEM領域。

以下領域提供了有關最佳做法的文檔：

* [Assets](#assets)
* [Sites](#sites)

有關創作、部署和維護或開發的最佳做法，請參閱以下內容之一：

* [編寫最佳做法](/help/sites-authoring/best-practices.md)
* [制定最佳做法](/help/sites-developing/best-practices.md)
* [部署最佳做法](/help/sites-deploying/best-practices.md)

具體文檔將在隨後的表中進行描述和連結。

## Assets {#assets}

以下主題介紹了圍繞資產的最佳做法，包括Dynamic Media能力和Dynamic Media Classic整合：

<table>
 <tbody>
  <tr>
   <td>在資產周圍的不同領域中採用最佳做法，以增強負載下的系統穩定性和效能</td>
   <td><a href="/help/assets/best-practices-for-assets.md">Assets 最佳實務</a></td>
   <td>包括指向圍繞資產的不同領域的最佳做法指南的連結。 在審閱這些資訊後，您將擁有構建和管理企業資產管理系統的知識和工具。</td>
  </tr>
  <tr>
   <td>如何組織您的內容（資料夾層次結構）</td>
   <td><a href="/help/assets/organize-assets.md">檔案管理最佳作法</a></td>
   <td>很多處理配置檔案都是基於資料夾的，因為視頻、元資料、影像處理總是應用於資料夾。 此最佳做法文檔介紹如何定義和設定資料夾層次結構，因為該層次結構對內容的處理方式有重大影響。 </td>
  </tr>
  <tr>
   <td>整合Scene7AEM和</td>
   <td><a href="/help/sites-administering/scene7.md#best-practices-for-integrating-scene-with-aem">將Scene7與</a></td>
   <td><p>介紹何時啟用輪詢導入程式、如何test驅動整合，以及何時使用內容瀏覽器而不是直接上載到資產。</p> </td>
  </tr>
  <tr>
   <td>影像預設選項</td>
   <td>理解 <a href="/help/assets/managing-image-presets.md#understanding-image-presets">影像預設</a> 和 <a href="/help/assets/managing-image-presets.md#image-preset-options">映像預設最佳實踐</a></td>
   <td>作為文檔的一部分 <a href="/help/assets/managing-image-presets.md">管理影像預設</a>中，這些主題描述了什麼是影像預設以及選擇影像預設選項的最佳做法。</td>
  </tr>
  <tr>
   <td>Dynamic Media與Scene7直接整合</td>
   <td><a href="/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media">Scene7/AEM一體化與Dynamic Media</a></td>
   <td>描述何時最好使用Dynamic Media解決方案、何時將S7與整合AEM，或何時使用兩者。</td>
  </tr>
 </tbody>
</table>

## Sites {#sites}

管理和創作網站內容有一些最佳做法概述如下：

<table>
 <tbody>
  <tr>
   <td>GDPR合規性</td>
   <td><a href="/help/sites-administering/gdpr-compliance-sites.md">AEM SitesGDPR合規性</a></td>
   <td>歐盟關於資料隱私權的一般資料保護條例自2018年5月起生效。 AEM Sites遵守了GDPR。 本頁指導客戶完成處理AEM SitesGDPR請求的過程。 它描述了儲存私人資料的位置，以及如何以手動方式或使用程式碼移除它們。</td>
  </tr>
  <tr>
   <td>定義實例的預設UI。</td>
   <td><p><a href="/help/sites-authoring/select-ui.md#configuring-the-default-ui-for-your-instance">配置實例的預設UI</a></p> </td>
   <td>有AEM兩個UI:觸摸優化，經典。 本節詳細介紹如何定義實例的預設UI。</td>
  </tr>
  <tr>
   <td>多站點管理</td>
   <td><a href="/help/sites-administering/msm-best-practices.md">MSM 最佳做法</a></td>
   <td>使用MSM自動化內容部署的最佳做法。 </td>
  </tr>
  <tr>
   <td>翻譯內容</td>
   <td><a href="/help/sites-administering/tc-bp.md">翻譯最佳實務</a></td>
   <td>規劃和實施多語言站點的最佳做法。</td>
  </tr>
  <tr>
   <td>用戶管理</td>
   <td><a href="/help/sites-administering/security.md#best-practices">權限和權限最佳實踐</a></td>
   <td>介紹使用權限和權限時的最佳做法 </td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md#configuration">工作流最佳實踐 — 配置</a></td>
   <td>工作流使您能夠自動執行Adobe Experience Manager(AEM)活動，並可代表在環境中發生的大量處理AEM，因此強烈建議仔細規劃和配置您的工作流實施。</td>
  </tr>
 </tbody>
</table>
