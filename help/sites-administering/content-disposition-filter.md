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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 內容處置篩選{#content-disposition-filter}

內容處置篩選器是針對SVG檔案的XSS攻擊的安全性功能。

安裝後，篩選器會封鎖對所有資產的存取。 例如，您無法線上上檢視pfd。 本節說明如何依您的需求設定篩選。

## 設定內容處置篩選 {#configure-content-disposition-filter}

您可以在GitHub中 [檢視Apache Sling Content Disposition篩選器](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)。

「內容處置篩選」選項提供下列功能：

* 內容處置路徑：將應用篩選器的路徑清單，後面接著要在該路徑上排除的mime類型清單。此路徑必須是絕對路徑，最後可包含通配符(&#39;&amp;ast;&#39;)，以匹配每個資源路徑與給定路徑前置詞。 例如：/content/&amp;ast;:image/jpeg,image/svg+xml &quot;將對/content（jpg和svg影像除外）中的每個節點應用過濾器

* 排除的資源路徑：排除的資源清單中，必須將每個資源路徑指定為絕對和完全限定路徑。 不支援首碼比對／萬用字元。

* 對所有資源路徑啟用：此標誌控制是否為所有路徑啟用此篩選器，但排除資源路徑定義的排除路徑除外。 將此設為&#39;true&#39;會忽略「內容處置路徑」。 不受僅包含配置的資源路徑的限制，這些資源路徑包含名為&#39;jcr:data&#39;或&#39;jcr:content jcr:data&#39;的屬性。

