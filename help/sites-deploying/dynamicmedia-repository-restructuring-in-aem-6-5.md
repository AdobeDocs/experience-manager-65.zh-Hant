---
title: Dynamic Media6.AEM5儲存庫重組
seo-title: Dynamic Media6.AEM5儲存庫重組
description: 瞭解如何進行必要的更改，以便遷移到針對Dynamic Media的AEM6.5中的新儲存庫結構。
seo-description: 瞭解如何進行必要的更改，以便遷移到針對Dynamic Media的AEM6.5中的新儲存庫結構。
uuid: e26d61a4-47b6-493a-9ba2-4c58b200ddd9
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 61cd5751-0dc8-48e0-873e-3a64899489bb
feature: 升級
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 4%

---


# Dynamic MediaAEM6.5 {#dynamic-media-repository-restructuring-in-aem}儲存庫重組

如[父6.5](/help/sites-deploying/repository-restructuring.md)頁中的「資料庫重組」頁中所述，升級至AEM6.5的客戶應使用此頁評估與影響Dynamic Media解決方案的資料庫更改相關的工作成果。 有些變更需要在6.5升級程AEM序中努力工作，而有些則會延遲至日後升級。

**未來升級前**

* [自訂最適化視訊編碼設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media(DMS7)雲配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media(DM Hybrid)Cloud Service配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media- YouTubeCloud Service配置](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [其他](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 未來升級前{#prior-to-upgrade}

### 自訂最適化視訊編碼組態{#custom-adaptive-video-encoding-configurations}

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
   <td><p>您可以執行下列移轉指令碼，以移轉至新位置：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在UI中編AEM輯設定，而變更將儲存至新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media(DMS7)雲配置{#dynamic-media-dms-cloud-configuration}

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
   <td><p>客戶可在此位置運行遷移指令碼：<br /> </p>
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

### Dynamic Media(DM Hybrid)Cloud Service配置{#cloudserviceconfiguration}

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
   <td><p>您可以執行下列移轉指令碼，以便與最新模型對齊：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media- YouTubeCloud Service配置{#youtubecloudserviceconfiguration}

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
   <td><p>1.從YouTube<br /> 2取消發佈所有影片。 使用新的TouchUI（來自<code>/conf</code>）建立YouTube設定，包括從舊位置<br /> 3複製所有頻道。 將所有視訊發佈回YouTube。</p> <p>此工作流程會產生新的YouTube URL。 如果您在建立新的TouchUI YouTube設定之前未解除發佈，則「屬性」下會列出多個YouTube URL，因為如果有機會，重新建立的渠道將會再次發佈。 這表示您的「屬性」下會列出無用的URL。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Misc {#misc}

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
   <td><p>客戶可執行下列移轉指令碼。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在UI中編AEM輯設定，而變更將儲存至新位置。</p> </td>
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
   <td><strong>上一個位置</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>重組指導</strong></td>
   <td><p>客戶可執行下列移轉指令碼。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>不適用</td>
  </tr>
 </tbody>
</table>

