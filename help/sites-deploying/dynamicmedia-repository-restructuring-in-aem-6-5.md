---
title: Dynamic MediaAdobe Experience Manager6.5
description: 瞭解如何進行必要的更改，以便遷移到Dynamic Media第6.5號Experience Manager中的新儲存庫結構。
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

# Dynamic MediaAdobe Experience Manager6.5 {#dynamic-media-repository-restructuring-in-aem}

如父代中所述 [Adobe Experience Manager6.5的資料庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級到Experience Manager6.5的客戶應使用此頁面來評估與影響Dynamic Media的儲存庫更改相關的工作量。 某些更改需要在Experience Manager6.5升級過程中進行工作，而其他更改則可以推遲到以後升級。

**未來升級前**

* [自定義自適應視頻編碼配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media(DMS7)雲配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media（DM混合）Cloud Service配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media-YouTubeCloud Service配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [雜項](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 未來升級前 {#prior-to-upgrade}

### 自定義自適應視頻編碼配置  {#custom-adaptive-video-encoding-configurations}

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
   <td><strong>重組指導</strong></td>
   <td><p>您可以運行以下遷移指令碼以遷移到新位置：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，可以在Experience ManagerUI中編輯配置，並將更改保存到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media(DMS7)雲配置 {#dynamic-media-dms-cloud-configuration}

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
   <td><strong>重組指導</strong></td>
   <td><p>客戶可以在以下位置運行遷移指令碼：<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>重新啟動Dynamic MediaOSGi捆綁包。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### Dynamic Media（DM混合）Cloud Service配置 {#cloudserviceconfiguration}

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
   <td><strong>重組指導</strong></td>
   <td><p>您可以運行以下遷移指令碼，以便與最新型號對齊：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media-YouTubeCloud Service配置  {#youtubecloudserviceconfiguration}

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
   <td><strong>重組指導</strong></td>
   <td><p>1。取消發佈來自YouTube的所有視頻<br /> 2. 使用新的TouchUI建立YouTube配置(從 <code>/conf</code>)包括從舊位置複製所有通道<br /> 3. 將所有視頻發佈回YouTube。</p> <p>此工作流將生成新的YouTubeURL。 如果在建立TouchUIYouTube配置之前未取消發佈，則在「屬性」下列出了多個YouTubeURL，因為如果有機會，重新建立的通道將再次發佈。 此功能表示在「屬性」下列出了無用的URL。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
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
   <td><strong>重組指導</strong></td>
   <td><p>客戶可以運行以下遷移指令碼。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，可以在Experience ManagerUI中編輯配置，並將更改保存到新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
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
   <td><strong>重組指導</strong></td>
   <td><p>客戶可以運行以下遷移指令碼。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>
