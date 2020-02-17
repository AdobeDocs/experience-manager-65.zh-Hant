---
title: 使用內容屬性匯出內容
seo-title: 使用內容屬性匯出內容
description: 下頁顯示「應用程式屬性」和「節點」。
seo-description: 下頁顯示「應用程式屬性」和「節點」。
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用內容屬性匯出內容{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

應用程式在AEM中 *會以cq:Pages* 表示。

除了下列顯示的其他代表整合支援屬性的屬性 *外，這些屬性與任何* cq:Page中的相同公用屬性。

## 應用程式屬性 {#app-properties}

下表顯示「應用程 **式屬性」和「節點」**。

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
   <td><p>已設定Mobile On-Demand cloud服務的路徑。 用於AEM mobile到Mobile的隨選動作（API呼叫）</p> <p>當作者選擇Mobile On-Demand cloud服務將應用程式關聯至時，此關聯會透過「管理連線」方塊設定。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>字串：路徑</td>
   <td><p>應用程式匯出設定的路徑。 導出配置是一個資料夾，包含2個子ContentSync導出配置模板；</p> <p><i>dps-article</i>:ContentSync匯出設定，以匯出文章內容</p> <p><i>dps-HTMLResources</i>:ContentSync匯出設定可匯出應用程式／文章共用資源</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>字串</td>
   <td><p>此應用程式連結／系結至之行動隨選專案的ID/URI。</p> <p>當作者從相關Mobile On-Demand cloud服務的可用專案清單中選擇專案時，此關聯會透過「管理連線」方塊設定。</p> </td>
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
   <td>上次從AEM上傳共用資源至AEM mobile的日期。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>字串：userid</td>
   <td>從AEM上次上傳共用資源請求至AEM mobile的使用者ID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>字串：路徑</td>
   <td>控制面板設定的路徑。 路徑可視需要重新導向至自訂儀表板設定。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字串：路徑</td>
   <td><p>cq：元件的路徑，此為或延伸 <i>mobileapps/core/components/instance。</i></p> <p>如此可在「應用程式目錄」中呈現和呈現。</p> </td>
  </tr>
 </tbody>
</table>

您可以使用「 ***內容屬性*** 」來建立內容。 請參閱下列建立和匯出文章和共用資源的資源：

* [內容屬性](/help/mobile/content-properties.md)
* [建立文章匯出設定](/help/mobile/creating-article-export-configuration.md)
* [建立共用資源導出配置](/help/mobile/creating-shared-resources-export-configuration.md)
