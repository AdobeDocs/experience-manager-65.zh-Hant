---
title: AEM 6.5中的動態媒體儲存庫重組
seo-title: AEM 6.5中的動態媒體儲存庫重組
description: 瞭解如何進行必要的變更，以移轉至AEM 6.5 for Dynamic Media中的新儲存庫結構。
seo-description: 瞭解如何進行必要的變更，以移轉至AEM 6.5 for Dynamic Media中的新儲存庫結構。
uuid: e26d61a4-47b6-493a-9ba2-4c58b200ddd9
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 61cd5751-0dc8-48e0-873e-3a64899489bb
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# AEM 6.5中的動態媒體儲存庫重組 {#dynamic-media-repository-restructuring-in-aem}

如「AEM 6.5 [](/help/sites-deploying/repository-restructuring.md) 」中的父資料庫重組頁面所述，升級至AEM 6.5的客戶應使用此頁面來評估與影響動態媒體解決方案的資料庫變更相關的工作成果。 有些變更需要在AEM 6.5升級程式中努力工作，而其他變更則可延後至日後升級。

**未來升級前**

* [自訂最適化視訊編碼設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [動態媒體(DMS7)雲端設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [動態媒體(DM Hybrid)雲端服務組態](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [動態媒體- youTube雲端服務設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [其他](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 未來升級前 {#prior-to-upgrade}

### 自訂最適化視訊編碼設定 {#custom-adaptive-video-encoding-configurations}

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
   <td><p>您可以執行下列移轉指令碼，以移轉至新位置：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在AEM UI中編輯設定，而變更將儲存至新位置。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media (DMS7) Cloud configuration {#dynamic-media-dms-cloud-configuration}

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
     <li>重新啟動Dynamic Media OSGi套件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

### 動態媒體(DM Hybrid)雲端服務組態 {#cloudserviceconfiguration}

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
   <td><p>您可以執行下列移轉指令碼，以符合最新的模型：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 動態媒體- youTube雲端服務設定 {#youtubecloudserviceconfiguration}

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
   <td><p>1.從YouTube<br /> 2取消發佈所有視訊。 使用新的TouchUI（從）建立YouTube設定， <code>/conf</code>包括從舊位置<br /> 3複製所有頻道。 將所有視訊發佈回YouTube。</p> <p>此工作流程會產生新的YouTube URL。 如果您在建立新的TouchUI YouTube設定之前未解除發佈，則「屬性」下會列出多個YouTube URL，因為如果有機會，重新建立的渠道將會再次發佈。 這表示您的「屬性」下會列出無用的URL。</p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 其他 {#misc}

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
   <td><p>客戶可執行下列移轉指令碼。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>或者，您也可以在AEM UI中編輯設定，而變更將儲存至新位置。</p> </td>
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
   <td><p>客戶可執行下列移轉指令碼。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>附註</strong></td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

