---
title: 使用內容屬性匯出內容
description: 以下頁面顯示應用程式屬性和節點。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 3%

---

# 使用內容屬性匯出內容{#using-content-properties-to-export-content}

{{ue-over-mobile}}

在AEM中，應用程式會顯示為&#x200B;*cq：Pages*。

除了以下所示的其他表示整合支援屬性的屬性外，它們還共用在任何&#x200B;*cq：Page*&#x200B;中找到的相同一般屬性。

## 應用程式屬性 {#app-properties}

下表顯示&#x200B;**應用程式屬性和節點**。

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>字串：路徑</td>
   <td><p>已設定Mobile On-DemandCloud Service的路徑。 用於AEM Mobile以進行Mobile On-Demand動作（API叫用）</p> <p>作者選擇將應用程式與之建立關聯的「隨選行動」Cloud Service時，可透過「管理連線」圖磚設定此關聯。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>字串：路徑</td>
   <td><p>應用程式的匯出設定路徑。 匯出設定是包含2個子ContentSync匯出設定範本的資料夾；</p> <p><i>dps-article</i>： ContentSync匯出設定以匯出文章內容</p> <p><i>dps-HTMLResources</i>： ContentSync匯出設定以匯出應用程式/文章共用資源</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>字串</td>
   <td><p>此應用程式連結/繫結至Mobile On-Demand專案的ID/URI。</p> <p>作者從相關Mobile On-DemandCloud Service的可用專案清單選擇專案時，可透過「管理連線」圖磚設定此關聯。</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>字串</td>
   <td>應用程式標題。</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>字串</td>
   <td>內容型別。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>日期</td>
   <td>共用資源上次從AEM上傳至AEM Mobile的日期。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>字串：userid</td>
   <td>執行上次從AEM將共用資源請求上傳至AEM Mobile的使用者ID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>字串：路徑</td>
   <td>控制面板設定的路徑。 路徑可視需要重新導向至自訂控制面板設定。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字串：路徑</td>
   <td><p>屬於或擴充<i>mobileapps/core/components/instance的cq：Component的路徑。</i></p> <p>這會提供應用程式目錄中的顯示和轉譯。</p> </td>
  </tr>
 </tbody>
</table>

您可以使用&#x200B;***內容屬性***&#x200B;來建立內容。 請參閱下列資源，以建立和匯出文章與共用資源：

* [內容屬性](/help/mobile/content-properties.md)
* [建立文章匯出設定](/help/mobile/creating-article-export-configuration.md)
* [建立共用資源匯出設定](/help/mobile/creating-shared-resources-export-configuration.md)
