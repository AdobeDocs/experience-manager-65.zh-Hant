---
title: 選擇AEM Forms安裝的永續性類型
seo-title: 選擇AEM Forms安裝的永續性類型
description: 明智地選擇永續性類型。 它可協助您建立有效率且可擴充的AEM Forms環境。
seo-description: 明智地選擇永續性類型。 它可協助您建立有效率且可擴充的AEM Forms環境。
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 選擇AEM Forms安裝的永續性類型 {#choosing-a-persistence-type-for-an-aem-forms-installation}

明智地選擇永續性類型。 它可協助您建立有效率且可擴充的AEM Forms環境。

持久性是在物理儲存上儲存內容的方法。 定義了資料的實際資料結構和儲存機制。 MicroKernels在AEM Forms中擔任永續性管理員。 AEM Forms支援TarMK、MongoMK和RDBMK類型的永續性(MicroKernals)。 您可以根據AEM Forms例項的用途和部署類型（單一伺服器、群組或叢集），為AEM Forms選擇永續性類型。

>[!NOTE]
>
>LiveCycle ES4 SP1使用TarPM永續性來儲存內容。

下表列出了所有支援的持久性類型以及各種參數，以幫助您為環境選擇持久性類型：

<table>
 <tbody>
  <tr>
   <th><strong>安裝類型／成本</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>獨立設定</strong></th>
   <td>支援<br /> </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <th><strong>群集設定</strong></th>
   <td>不支援</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <th><strong>授權成本</strong></th>
   <td>隨附於AEM </td>
   <td>需要個別授權</td>
   <td>需要個別授權</td>
  </tr>
 </tbody>
</table>

TarMK是針對效能而設計，而MongoMK和RDBMK則是針對可擴充性而設計。 Adobe強烈建議將TarMK做為所有AEM Forms部署藍本的預設永續性技術，適用於作者和發佈執行個體，但在 [Choosing Mongo或Relational Database Microkernel over TarMK一節中概述的使用案例除外](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p)。

如需支援的Microkernels清單，請參閱「OSGi技術需求上的 [AEM Forms](/help/sites-deploying/technical-requirements.md) 」或「 [JEE支援的平台組合文章上的AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md) 」。

## 選擇Mongo或TarMK上的關係資料庫微內核 {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

可擴充（叢集）的AEM Forms環境是兩個或兩個以上水準設定的作用中作者執行個體的集合。 如果單一伺服器支援所有並行編寫活動，而無法持續執行，您可以選擇執行多個作者例項。

JEE環境上的可擴充（叢集）AEM Forms僅支援MongoMK和RDBMK永續性類型。 每個安裝的伺服器數量或可擴展環境的大小都有所不同。 如需考量事項和範例的清單，請參閱「 [Recommended Deployments](/help/sites-deploying/recommended-deploys.md)[and or Architecture and deployment topologies for AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md) 」文章。 您也可以聯絡AEM Forms支援，以取得有關AEM Forms與RDBMK和TarMK的容量規劃詳細資訊。
