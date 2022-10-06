---
title: 為AEM Forms安裝選擇持續性類型
seo-title: Choosing a persistence type for an AEM Forms installation
description: 明智地選擇持續性類型。 它可協助您建立有效且可擴充的AEM Forms環境。
seo-description: Choose a persistence type wisely. It helps you build an efficient and scale able AEM Forms environment.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---

# 為AEM Forms安裝選擇持續性類型 {#choosing-a-persistence-type-for-an-aem-forms-installation}

明智地選擇持續性類型。 它可協助您建立有效且可擴充的AEM Forms環境。

持久性是在物理儲存上儲存內容的方法。 它定義了資料的實際資料結構和儲存機制。 MicroKernels在AEM Forms中充當持久性管理器。 AEM Forms支援TarMK、MongoMK和RDBMK類型的持續性(MicroKernals)。 您可以根據AEM Forms執行個體的用途和部署類型（單伺服器、伺服器陣列或叢集），選擇AEM Forms的持續性類型。

>[!NOTE]
>
>LiveCycleES4 SP1使用TarPM持續性來儲存內容。

下表列出了所有支援的持久性類型以及各種參數，以幫助您為環境選擇持久性類型：

<table>
 <tbody>
  <tr>
   <th><strong>安裝類型/成本</strong></th>
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
   <th><strong>許可成本</strong></th>
   <td>隨附AEM </td>
   <td>需要單獨的許可證</td>
   <td>需要單獨的許可證</td>
  </tr>
 </tbody>
</table>

TarMK的設計目的是提升效能，而MongoMK和RDBMK的設計目的則是為了擴充性。 Adobe強烈建議，所有AEM Forms部署案例（製作和發佈例項），都使用TarMK做為預設永續性技術，但本節所述的使用案例除外 [選擇Mongo或關係資料庫微內核而不選擇TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

有關支援的微內核的清單，請參見 [AEM Forms OSGi技術要求](/help/sites-deploying/technical-requirements.md) 或 [AEM Forms on JEE支援的平台組合](/help/forms/using/aem-forms-jee-supported-platforms.md) 文章。

## 選擇Mongo或關係資料庫微內核而不選擇TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

可擴充（叢集）的AEM Forms環境是兩個或兩個以上水準設定的作用中製作例項的集合。 如果支援所有同時編寫活動的單一伺服器已無法持續運作，您可以選擇執行多個製作例項。

JEE環境上的可擴充（叢集）AEM Forms僅支援MongoMK和RDBMK持續性類型。 每個安裝的伺服器數量或可擴展環境的大小都不同。 如需考量事項和範例的清單，請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md) 和 [適用於AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md) 文章。 您也可以聯絡AEM Forms支援，取得有關使用RDBMK和TarMK進行AEM Forms容量規劃的詳細資訊。
