---
title: 使用內容屬性來匯出內容
seo-title: 使用內容屬性來匯出內容
description: 以下頁面顯示應用程式屬性和節點。
seo-description: 以下頁面顯示應用程式屬性和節點。
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 4%

---

# 使用內容屬性來匯出內容{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

應用程式在AEM中會以&#x200B;*cq:Pages*&#x200B;呈現。

除了下列其他表示整合支援屬性的屬性外，這些屬性共用在任何&#x200B;*cq:Page*&#x200B;中找到的相同共同屬性。

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
   <td><p>已設定的Mobile On-DemandCloud Service的路徑。 用於AEM Mobile到Mobile On-Demand動作（API叫用）</p> <p>當作者選擇行動隨選Cloud Service將應用程式與之建立關聯時，此關聯會透過「管理連線」方塊設定。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>字串：路徑</td>
   <td><p>應用程式匯出設定的路徑。 導出配置是一個包含2個子ContentSync導出配置模板的資料夾；</p> <p><i>dps-article</i>:匯出文章內容的ContentSync匯出設定</p> <p><i>dps-HTMLResources</i>:ContentSync匯出設定，以匯出應用程式/文章共用資源</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>字串</td>
   <td><p>此應用連結/綁定到的Mobile On-Demand項目的ID/URI。</p> <p>當作者從相關行動隨選Cloud Service的可用專案清單中選擇專案時，此關聯會透過「管理連線」方塊設定。</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>字串</td>
   <td>應用程式標題。</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>字串</td>
   <td>內容類型.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>日期</td>
   <td>上次從AEM上傳共用資源至AEM Mobile的日期。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:userid</td>
   <td>上次從AEM上傳共用資源請求至AEM Mobile的使用者ID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>字串：路徑</td>
   <td>控制面板配置的路徑。 路徑可視需要重新導向至自訂控制面板設定。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字串：路徑</td>
   <td><p>cq：元件的路徑，此元件為或延伸<i>mobileapps/core/components/instance。</i></p> <p>這可提供應用程式目錄中的呈現和呈現。</p> </td>
  </tr>
 </tbody>
</table>

您可以使用&#x200B;***內容屬性***&#x200B;來建立內容。 請參閱下列資源，以建立和匯出文章及共用資源：

* [內容屬性](/help/mobile/content-properties.md)
* [建立文章匯出設定](/help/mobile/creating-article-export-configuration.md)
* [建立共用資源導出配置](/help/mobile/creating-shared-resources-export-configuration.md)
