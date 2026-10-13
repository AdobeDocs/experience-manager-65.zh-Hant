---
title: Adobe Experience Manager 6.5中的Dynamic Media存放庫重組
description: 瞭解如何進行必要的變更，以移轉至Dynamic Media的Experience Manager 6.5中的新存放庫結構。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 835ee49e-9248-5578-a60a-15c097807178
    internal-label: Upgrading
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 3%
---
# Adobe Experience Manager 6.5中的Dynamic Media存放庫重組 {#dynamic-media-repository-restructuring-in-aem}

如Adobe Experience Manager 6.5[&#128279;](/help/sites-deploying/repository-restructuring.md)頁面的上層存放庫重新調整中所述，升級至Experience Manager 6.5的客戶應使用此頁面評估與影響Dynamic Media的存放庫變更相關的工作量。 在Experience Manager 6.5升級程式期間，有些變更需要大量工作量，而其他變更則可能延遲到未來升級為止。

**未來升級之前**

* [自訂最適化視訊編碼設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media (DMS7)雲端設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media (DM Hybrid) Cloud Service設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - YouTube Cloud Service設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [雜項](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 在日後升級之前 {#prior-to-upgrade}

### 自訂最適化視訊編碼設定  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>您可以執行下列移轉指令碼，以移轉至新位置：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在Experience Manager UI中編輯設定，並將變更儲存至新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>備註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media (DMS7)雲端設定 {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>客戶可以在此位置執行移轉指令碼： <br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>重新啟動Dynamic Media OSGi套件組合。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>備註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

### Dynamic Media (DM Hybrid) Cloud Service設定 {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>您可以執行以下移轉指令碼，以符合最新模式：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>備註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media - YouTube Cloud Service設定  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>1. 從YouTube<br /> 2取消發佈所有視訊。 使用新的TouchUI （從<code>/conf</code>）建立YouTube設定，包括從舊位置<br /> 3複製所有頻道。 將所有影片發佈回YouTube。</p> <p>此工作流程會產生新的YouTube URL。 如果您在建立TouchUI YouTube設定之前未取消發佈，則您在「屬性」下列出多個YouTube URL，因為重新建立的管道會再次發佈（如果有機會的話）。 此功能表示您有「屬性」底下所列出的無用URL。</p> </td>
  </tr>
  <tr>
   <td><strong>備註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### 雜項 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>客戶可執行以下移轉指令碼。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在Experience Manager UI中編輯設定，並將變更儲存至新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>備註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>重組指南</strong></td>
   <td><p>客戶可執行以下移轉指令碼。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>備註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>
