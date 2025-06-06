---
title: 內容處置篩選
description: 瞭解如何使用內容處置篩選器來防止XSS攻擊。
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# 內容處置篩選 {#content-disposition-filter}

內容處置篩選器是一項安全性功能，可抵禦SVG檔案上的XSS攻擊。

安裝後，篩選器會封鎖對所有資產的存取。 例如，您無法線上上檢視PDF。 本節說明如何根據您的需求設定篩選器。

## 設定內容處置篩選 {#configure-content-disposition-filter}

您可以在GitHub[&#128279;](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)中檢視Apache Sling內容配置篩選器。

「內容配置篩選」選項提供下列功能：

* **內容處置路徑：**&#x200B;套用篩選的路徑清單，後面接著要排除在該路徑上的mime型別清單。 此路徑必須是絕對路徑，且結尾可包含萬用字元(`*`)，以比對每個資源路徑與指定的路徑前置詞。 例如： `/content/*:image/jpeg,image/svg+xml`將篩選器套用至`/content?`中除了JPG和SVG影像之外的每個節點。

* **排除的資源路徑：**&#x200B;排除的資源清單，每個資源路徑都必須以絕對和完全合格的路徑提供。 不支援字首比對/萬用字元。

* **為所有資源路徑啟用：**&#x200B;此旗標控制是否為所有路徑啟用此篩選，排除的資源路徑所定義的排除路徑除外。 將此標幟設為「true」會導致忽略內容處置路徑。 與組態無關，只涵蓋包含名為`jcr:data`或`jcr:content/jcr:data`之屬性的資源路徑。
