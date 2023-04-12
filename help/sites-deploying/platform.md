---
title: AEM Platform簡介
seo-title: Introduction to the AEM Platform
description: 本文提供AEM平台及其最重要元件的一般概述。
seo-description: This article provides a general overview of the AEM platform and its most important components.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# AEM Platform簡介{#introduction-to-the-aem-platform}

AEM 6中的AEM平台以Apache Jackrabbit Oak為基礎。

Apache Jackrabbit Oak致力實作可擴充且效能優異的階層式內容存放庫，以作為現代世界級網站及其他苛刻內容應用程式的基礎。

它是Jackrabbit 2的後繼版本，由AEM 6用作其內容存放庫CRX的預設後端。

## 設計原則與目標 {#design-principles-and-goals}

Oak實作 [JSR-283](https://jcp.org/en/jsr/detail?id=283) (JCR 2.0)規格。 其主要設計目標是：

* 更好地支援大型儲存庫
* 多分佈式群集節點以實現高可用性
* 效能更好
* 支援許多子節點和訪問控制級別

## 架構概念 {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### 儲存空間 {#storage}

儲存層的目的是：

* 實作樹模型
* 使儲存可插拔
* 提供群集機制

### Oak Core {#oak-core}

Oak Core在儲存層中新增數層：

* 訪問級別控制
* 搜尋和索引
* 觀察

### Oak JCR {#oak-jcr}

Oak JCR的主要目標是將JCR語義轉換為樹操作。 它還負責：

* 實作JCR API
* 包含實現JCR約束的提交掛接

此外，現在也可實作非Java，且為Oak JCR概念的一部分。

## 儲存概述 {#storage-overview}

Oak儲存層提供抽象層，用於實際儲存內容。

目前，AEM6提供兩種儲存實作： **Tar儲存** 和 **MongoDB儲存**.

### Tar儲存 {#tar-storage}

Tar儲存使用tar檔案。 它會將內容儲存為較大區段內的各種記錄類型。 日記帳用於跟蹤儲存庫的最新狀態。

它圍繞幾個關鍵設計原則而構建：

* **不可變區段**

內容儲存在最多256 KB的區段中。 它們不可變，因此可輕鬆快取經常存取的區段，並減少可能損壞儲存庫的系統錯誤。

每個區段都由唯一識別碼(UUID)識別，並包含內容樹狀結構的連續子集。 此外，區段可參考其他內容。 每個區段會保留其他參考區段的UUID清單。

* **位置**

相關記錄（如節點及其直接子項）儲存在相同的段中。 這樣可以快速搜索儲存庫，並避免每個會話訪問多個相關節點的典型客戶端的大多數快取丟失。

* **緊湊性**

記錄的格式化被優化為大小，以降低IO成本，並盡可能地調整快取中的內容。

### Mongo儲存 {#mongo-storage}

MongoDB儲存使用MongoDB進行共用和群集。 儲存庫樹將保留在一個MongoDB資料庫中，其中每個節點都是單獨的文檔。

它有幾項特點：

* 修訂

對於內容的每次更新（提交），都會建立新修訂。 修訂基本上是字串，包含三個元素：

1. 從其生成的電腦的系統時間派生的時間戳
1. 用於區分以相同時間戳記建立的修訂版本的計數器
1. 建立修訂的群集節點ID

* 分支

支援分支，可讓用戶端存放多項變更，並透過單一合併呼叫使其可見。

* 先前的文檔

MongoDB儲存將資料添加到每次修改的文檔。 不過，它只會在明確觸發清除時刪除資料。 達到特定臨界值時，會移動舊資料。 先前的文檔僅包含不可修改的資料，這表示它們僅包含已提交和合併的修訂。

* 群集節點元資料

有關活動和非活動群集節點的資料保留在資料庫中，以便進行群集操作。

具有MongoDB儲存的典型AEM叢集設定：

![chlimage_1-85](assets/chlimage_1-85.png)

## Jackrabbit 2有什麼不同？ {#what-is-different-from-jackrabbit}

由於Oak向後相容於JCR 1.0標準，因此使用者層級幾乎沒有變更。 不過，在設定Oak型AEM安裝時，您必須考慮一些顯著差異：

* Oak不會自動建立索引。 因此，必要時必須建立自訂索引。
* 不同於Jackrabbit 2，工作階段一律會反映存放庫的最新狀態，而Oak工作階段會反映從取得工作階段起存放庫的穩定檢視。 原因是Oak所依據的MVCC模型。
* Oak不支援同名同層級(SNS)。

## 其他平台相關檔案 {#other-platform-related-documentation}

如需AEM平台的詳細資訊，另請參閱下列文章：

* [在AEM 6中設定節點儲存和資料儲存](/help/sites-deploying/data-store-config.md)
* [Oak查詢和索引](/help/sites-deploying/queries-and-indexing.md)
* [AEM 6中的儲存元素](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM與MongoDB](/help/sites-deploying/aem-with-mongodb.md)
