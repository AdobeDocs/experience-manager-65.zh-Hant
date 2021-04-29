---
title: 內容處置篩選
seo-title: 內容處置篩選
description: 瞭解如何使用「內容處置篩選」來防止XSS攻擊。
seo-description: 瞭解如何使用「內容處置篩選」來防止XSS攻擊。
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
translation-type: tm+mt
source-git-commit: cd895fcab5adce600ce230fb6867392e45963c16
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# 內容處置篩選器{#content-disposition-filter}

內容處置篩選器是針對SVG檔案的XSS攻擊的安全性功能。

安裝後，篩選器會封鎖對所有資產的存取。 例如，您無法線上檢視PDF。 本節說明如何依您的需求設定篩選。

## 設定內容處置篩選器{#configure-content-disposition-filter}

您可以在GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)中檢視[Apache Sling Content Disposition篩選器。

「內容處置篩選」選項提供下列功能：

* **內容處置路** 徑：一個路徑清單，其中將應用篩選器，後面接著一個要在該路徑上排除的mime類型清單。此路徑必須是絕對路徑，最後可能包含通配符(`*`)，以使每個資源路徑與給定路徑前置詞匹配。例如：`/content/*:image/jpeg,image/svg+xml`會將篩選器套用至「/content」中的每個節點？ 除了jpg和svg影像

* **排除的資源路** 徑：排除的資源清單，每個資源路徑必須作為絕對和完全限定路徑給定。不支援首碼比對／萬用字元。

* **對所有資源路徑啟用：此標** 志控制是否對所有路徑啟用此篩選器，但排除資源路徑定義的排除路徑除外。將此設為&#39;true&#39;會忽略「內容處置路徑」。 與配置無關，僅覆蓋包含名為`jcr:data`或`jcr:content/jcr:data`的屬性的資源路徑。
