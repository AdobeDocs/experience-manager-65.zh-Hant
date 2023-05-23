---
title: 使用內容屬性導出內容
seo-title: Using Content Properties to Export Content
description: 下頁顯示「應用程式屬性」和「節點」。
seo-description: The following page shows App Properties and Nodes.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 4%

---

# 使用內容屬性導出內容{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

應用程式表示為 *cq：頁面* 的上AEM界。

它們共用在任何 *cq：頁* 除下面顯示的其他表示整合支援屬性的屬性外。

## 應用程式屬性 {#app-properties}

下表顯示 **應用程式屬性和節點**。

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
   <td><p>配置的移動按需Cloud Service的路徑。 用於AEM Mobile到移動按需操作（API調用）</p> <p>當作者選擇Mobile On-DemandCloud Service將應用與關聯時，通過「管理連接」磁貼配置此關聯。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>字串：路徑</td>
   <td><p>應用導出配置的路徑。 導出配置是一個包含2個子ContentSync導出配置模板的資料夾；</p> <p><i>dps文章</i>:ContentSync導出配置以導出項目內容</p> <p><i>dps-HTMLR資源</i>:ContentSync導出配置以導出應用/項目共用資源</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>字串</td>
   <td><p>此應用連結到/綁定到的Mobile On-Demand項目的ID/URI。</p> <p>當作者從關聯的Mobile On-DemandCloud Service的可用項目清單中選擇項目時，通過「管理連接」磁貼配置此關聯。</p> </td>
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
   <td>上次將共用資源從上次上載到AEMAEM Mobile的日期。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>字串：用戶ID</td>
   <td>上次將共用資源請求上載到AEM Mobile的用戶AEMID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>字串：路徑</td>
   <td>儀表板配置的路徑。 路徑可以根據需要重定向到自定義儀表板配置。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字串：路徑</td>
   <td><p>cq的路徑：已擴展或已擴展的元件 <i>mobileapps/core/components/instance。</i></p> <p>這提供了應用程式目錄中的存在和呈現。</p> </td>
  </tr>
 </tbody>
</table>

您可以使用 ***內容屬性*** 的子菜單。 有關建立和導出項目和共用資源，請參閱以下資源：

* [內容屬性](/help/mobile/content-properties.md)
* [建立項目導出配置](/help/mobile/creating-article-export-configuration.md)
* [建立共用資源導出配置](/help/mobile/creating-shared-resources-export-configuration.md)
