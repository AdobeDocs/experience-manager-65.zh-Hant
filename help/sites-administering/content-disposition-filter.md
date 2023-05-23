---
title: 內容處置篩選器
seo-title: Content Disposition Filter
description: 瞭解如何使用內容處置過濾器來防止XSS攻擊。
seo-description: Learn how to use the Content Disposition Filter to prevent XSS attacks.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 內容處置篩選器 {#content-disposition-filter}

內容處置過濾器是針對SVG檔案的XSS攻擊的安全功能。

安裝後，篩選器將阻止對所有資產的訪問。 例如，您無法聯機查看PDF。 本節介紹如何根據需要配置篩選器。

## 配置內容處置篩選器 {#configure-content-disposition-filter}

您可以查看 [GitHub中的Apache Sling內容部署篩選器](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)。

「內容處置篩選器」選項提供以下功能：

* **內容處置路徑：** 應用篩選器的路徑清單，後面是該路徑上要排除的mime類型清單。此路徑必須是絕對路徑，並且可能包含通配符(`*`)，使每個資源路徑與給定路徑前置詞匹配。 例如： `/content/*:image/jpeg,image/svg+xml` 將篩選器應用於 `/content?` 除jpg和svg影像外

* **排除的資源路徑：** 排除的資源清單，每個資源路徑必須作為絕對和完全限定的路徑指定。 不支援前置詞匹配/通配符。

* **啟用所有資源路徑：** 此標誌控制是否為所有路徑啟用此篩選器，但由排除的資源路徑定義的排除路徑除外。 將此設定為「true」將導致忽略內容處置路徑。 與配置無關，僅覆蓋包含名為的屬性的資源路徑 `jcr:data` 或 `jcr:content/jcr:data`。
