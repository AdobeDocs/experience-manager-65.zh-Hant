---
title: Dynamic Media 6.5的存放庫重新調整
description: 了解如何進行必要的變更，以移轉至Dynamic Media適用的Experience Manager6.5中的新存放庫結構。
uuid: e26d61a4-47b6-493a-9ba2-4c58b200ddd9
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 61cd5751-0dc8-48e0-873e-3a64899489bb
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---

# Dynamic Media 6.5的存放庫重新調整 {#dynamic-media-repository-restructuring-in-aem}

如父項所述 [Adobe Experience Manager 6.5中的存放庫重新調整](/help/sites-deploying/repository-restructuring.md) 頁面中，升級至Experience Manager6.5的客戶應使用此頁面評估與影響Dynamic Media的存放庫變更相關的工作量。 某些變更需要Experience Manager6.5升級程式期間的工作量，而其他變更可能會延遲至日後升級。

**未來升級前**

* [自訂最適化視訊編碼設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media(DMS7)雲端設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media（DM混合）Cloud Service設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - YouTubeCloud Service設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [雜項](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 未來升級前 {#prior-to-upgrade}

### 自訂最適化視訊編碼設定  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>您可以執行下列移轉指令碼，以移轉至新位置：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在Experience ManagerUI中編輯設定，並將變更儲存至新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media(DMS7)雲端設定 {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>客戶可在以下位置執行移轉指令碼：<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>重新啟動Dynamic Media OSGi套件組合。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Dynamic Media（DM混合）Cloud Service設定 {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>您可以執行下列移轉指令碼，以符合最新模型：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media - YouTubeCloud Service設定  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>1.從YouTube取消發佈所有影片<br /> 2. 使用新的觸控式UI建立YouTube設定(從 <code>/conf</code>)，包括從舊位置複製所有通道<br /> 3. 將所有影片發佈回YouTube。</p> <p>此工作流程會產生新的YouTube URL。 如果您在建立觸控式UI YouTube設定前未取消發佈，則「屬性」下方會列出多個YouTube URL，因為重新建立的管道會重新發佈（如果有機會的話）。 此功能表示您的「屬性」下方會列出無用的URL。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用<br /> </td>
  </tr>
 </tbody>
</table>

### 雜項 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>客戶可執行以下移轉指令碼。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在Experience ManagerUI中編輯設定，並將變更儲存至新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>上一位置</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>客戶可執行以下移轉指令碼。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>
