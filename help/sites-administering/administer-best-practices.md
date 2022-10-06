---
title: 最佳作法
seo-title: Best Practices
description: 尋找由Adobe工程和諮詢團隊編譯的最佳實務，以協助管理員快速上手並執行。
seo-description: Find best practices compiled by Adobe engineering and consulting teams to help administrators get up and running.
uuid: 862d4fcf-ca61-4228-9344-b95a49b59b32
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f6468a0-7721-454f-9334-c449968b8fe7
exl-id: 576d87c8-cc96-45a0-b3cf-defb440babbb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 3%

---

# 最佳作法{#best-practices}

最佳實務說明如何以盡可能最有效率和最有效的方式開發、管理或使用AEM。 這份不斷增加的主題清單包含AEM中的多個領域。

以下幾方面提供有關最佳做法的檔案：

* [Assets](#assets)
* [Sites](#sites)

如需製作、部署和維護或開發的最佳實務，請參閱下列其中一項：

* [製作最佳實務](/help/sites-authoring/best-practices.md)
* [制定最佳做法](/help/sites-developing/best-practices.md)
* [部署最佳實務](/help/sites-deploying/best-practices.md)

下面的表中描述了特定文檔並連結到這些文檔。

## 資產 {#assets}

以下主題說明有關Assets的最佳實務，包括Dynamic Media功能和Dynamic Media Classic整合：

<table>
 <tbody>
  <tr>
   <td>Assets周圍不同區域的最佳實務，可在負載下增強系統穩定性和效能</td>
   <td><a href="/help/assets/best-practices-for-assets.md">Assets 最佳實務</a></td>
   <td>包含Assets不同區域最佳實務指南的連結。 在審核後，您將擁有構建和管理企業資產管理系統的知識和工具。</td>
  </tr>
  <tr>
   <td>如何組織內容（資料夾階層）</td>
   <td><a href="/help/assets/organize-assets.md">檔案管理最佳作法</a></td>
   <td>許多處理設定檔都是以資料夾為基礎，因為視訊、中繼資料、影像處理一律會套用至資料夾。 本最佳實務檔案說明如何定義和設定資料夾階層，因為階層對內容的處理方式有重大影響。 </td>
  </tr>
  <tr>
   <td>整合Scene7和AEM</td>
   <td><a href="/help/sites-administering/scene7.md#best-practices-for-integrating-scene-with-aem">整合Scene7與AEM的最佳作法</a></td>
   <td><p>說明何時開啟輪詢匯入工具、如何測試以促進整合，以及何時使用內容瀏覽器或直接上傳至資產。</p> </td>
  </tr>
  <tr>
   <td>影像預設集選項</td>
   <td>了解 <a href="/help/assets/managing-image-presets.md#understanding-image-presets">影像預設集</a> 和 <a href="/help/assets/managing-image-presets.md#image-preset-options">影像預設集最佳作法</a></td>
   <td>作為 <a href="/help/assets/managing-image-presets.md">管理影像預設集</a>，以下主題說明哪些影像預設集以及選取影像預設集選項的最佳實務。</td>
  </tr>
  <tr>
   <td>Dynamic Media與Scene7直接整合</td>
   <td><a href="/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media">Scene7/AEM整合與Dynamic Media</a></td>
   <td>說明何時最適合使用Dynamic Media解決方案、何時應將S7與AEM整合，或何時應同時使用兩者。</td>
  </tr>
 </tbody>
</table>

## 網站 {#sites}

管理和編寫網站內容有一些最佳實務，概述如下：

<table>
 <tbody>
  <tr>
   <td>GDPR法規遵循</td>
   <td><a href="/help/sites-administering/gdpr-compliance-sites.md">AEM Sites GDPR法規遵循</a></td>
   <td>歐盟資料隱私權一般資料保護規範自2018年5月起生效。 AEM Sites符合GDPR。 本頁引導客戶完成在AEM Sites中處理GDPR請求的程式。 它說明了儲存的私人資料位置，以及如何手動或使用程式碼移除這些資料。</td>
  </tr>
  <tr>
   <td>定義執行個體的預設UI。</td>
   <td><p><a href="/help/sites-authoring/select-ui.md#configuring-the-default-ui-for-your-instance">設定您執行個體的預設UI</a></p> </td>
   <td>AEM有兩個UI:觸控最佳化且經典。 本節詳細說明如何定義執行個體的預設UI。</td>
  </tr>
  <tr>
   <td>多網站管理</td>
   <td><a href="/help/sites-administering/msm-best-practices.md">MSM最佳實務</a></td>
   <td>使用MSM來自動部署內容的最佳作法。 </td>
  </tr>
  <tr>
   <td>轉譯內容</td>
   <td><a href="/help/sites-administering/tc-bp.md">翻譯最佳實務</a></td>
   <td>規劃及實作多語言網站的最佳實務。</td>
  </tr>
  <tr>
   <td>使用者管理</td>
   <td><a href="/help/sites-administering/security.md#best-practices">權限和權限最佳實務</a></td>
   <td>說明使用權限時的最佳作法 </td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md#configuration">工作流程最佳實務 — 設定</a></td>
   <td>工作流程可讓您自動化Adobe Experience Manager(AEM)活動，並可代表AEM環境中發生的大量處理，因此強烈建議您謹慎規劃和設定工作流程實作。</td>
  </tr>
 </tbody>
</table>
