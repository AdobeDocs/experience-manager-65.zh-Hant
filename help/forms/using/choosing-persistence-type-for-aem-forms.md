---
title: 為AEM Forms安裝選擇持久性類型
seo-title: Choosing a persistence type for an AEM Forms installation
description: 明智地選擇持久性類型。 它幫助您構建高效且可擴展的AEM Forms環境。
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

# 為AEM Forms安裝選擇持久性類型 {#choosing-a-persistence-type-for-an-aem-forms-installation}

明智地選擇持久性類型。 它幫助您構建高效且可擴展的AEM Forms環境。

持久性是在物理儲存上儲存內容的方法。 定義了資料的實際資料結構和儲存機制。 MicroKernels在AEM Forms充當持久性管理者。 AEM Forms支援TarMK、MongoMK和RDBMK類型的持久性(MicroKernals)。 您可以根據AEM Forms實例的用途和部署類型（單伺服器、場或群集）為AEM Forms選擇持久性類型。

>[!NOTE]
>
>LiveCycleES4 SP1使用TarPM持久性儲存內容。

下表列出了所有支援的持久性類型以及各種參數，以幫助您為環境選擇持久性類型：

<table>
 <tbody>
  <tr>
   <th><strong>安裝類型/成本</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>蒙戈克</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>獨立安裝</strong></th>
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
   <th><strong>許可證成本</strong></th>
   <td>隨附AEM </td>
   <td>需要單獨的許可證</td>
   <td>需要單獨的許可證</td>
  </tr>
 </tbody>
</table>

TarMK是為效能而設計的，而MongoMK和RDBMK則是為可擴充性而設計的。 Adobe強烈建議將TarMK作為所有AEM Forms部署方案（作者和發佈實例）的預設持久性技術，但本節中概述的使用案例除外 [選擇Mongo或TarMK上的關係資料庫微內核](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p)。

有關支援的微內核的清單，請參見 [AEM Forms關於OSGi技術要求](/help/sites-deploying/technical-requirements.md) 或 [AEM FormsJEE支援平台組合](/help/forms/using/aem-forms-jee-supported-platforms.md) 文章。

## 選擇Mongo或TarMK上的關係資料庫微內核 {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

可擴展（群集）的AEM Forms環境是兩個或兩個以上水準配置的活動作者實例的集合。 如果支援所有併發創作活動的單個伺服器不再可持續，則可以選擇運行多個作者實例。

JEE環境上的可擴展（群集）AEM Forms僅支援MongoMK和RDBMK持久性類型。 每個安裝的伺服器數量或可擴展環境的大小都有所不同。 有關注意事項和示例的清單，請參見 [建議的部署](/help/sites-deploying/recommended-deploys.md) 和 [用於AEM Forms的體系結構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md) 文章。 您還可以聯繫AEM Forms支援部門，以獲取有關AEM FormsRDBMK和TarMK容量規劃的詳細資訊。
