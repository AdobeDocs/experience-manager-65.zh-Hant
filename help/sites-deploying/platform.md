---
title: AEM平台簡介
seo-title: AEM平台簡介
description: 本文提供AEM平台及其最重要元件的一般概觀。
seo-description: 本文提供AEM平台及其最重要元件的一般概觀。
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM平台簡介{#introduction-to-the-aem-platform}

AEM 6中的AEM平台以Apache Jackrabbit Oak為基礎。

Apache Jackrabbit Oak致力於建置可擴充且具效能的階層式內容儲存庫，以做為現代世界級網站和其他繁重內容應用程式的基礎。

它是Jackrabbit 2的後繼版本，AEM 6會將其用作其內容存放庫CRX的預設後端。

## 設計原則與目標 {#design-principles-and-goals}

Oak建置 [JSR-283](https://www.day.com/day/en/products/jcr/jsr-283.html) (JCR 2.0)規格。 其主要設計目標是：

* 更好地支援大型儲存庫
* 多個分佈式群集節點以實現高可用性
* 更佳的效能
* 支援許多子節點和訪問控制級別

## 架構概念 {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### 儲存 {#storage}

儲存層的目的是：

* 實作樹模型
* 使儲存可插拔
* 提供叢集機制

### Oak Core {#oak-core}

Oak Core在儲存層中添加了幾個層：

* 存取層級控制
* 搜尋與索引
* 觀察

### Oak JCR {#oak-jcr}

Oak JCR的主要目的是將JCR語義轉換為樹操作。 它還負責：

* 實作JCR API
* 包含實現JCR約束的提交掛接

此外，非Java實作現在也已可能，並成為Oak JCR概念的一部分。

## 儲存空間概觀 {#storage-overview}

Oak儲存層提供實際儲存內容的抽象層。

目前，AEM6提供兩種儲存空間實作：Tar **Storage** 和 **MongoDB Storage**。

### Tar Storage {#tar-storage}

Tar儲存使用tar檔案。 它會將內容儲存為較大區段內的各種記錄類型。 日記帳用於跟蹤儲存庫的最新狀態。

它圍繞以下幾個關鍵設計原則：

* **不可變區段**

內容會儲存在最大大小可達256KiB的區段中。 它們是不可變的，因此可以輕鬆快取經常訪問的段並減少可能損壞儲存庫的系統錯誤。

每個段由唯一標識符(UUID)標識，並包含內容樹的連續子集。 此外，區段可參照其他內容。 每個區段會保留其他參考區段的UUID清單。

* **本地**

節點及其直接子項等相關記錄通常會儲存在相同的區段中。 這使得搜索儲存庫的速度非常快，並且避免了每個會話訪問多個相關節點的典型客戶機的大多數快取丟失。

* **緊湊性**

記錄的格式設定已針對大小進行優化，以降低IO成本，並盡可能使快取中的內容適合。

### Mongo Storage {#mongo-storage}

MongoDB儲存利用MongoDB進行共用和群集。 儲存庫樹保存在一個MongoDB資料庫中，其中每個節點都是獨立的文檔。

它有幾個特點：

* 修訂

對於內容的每次更新（提交），都會建立新修訂。 修訂版本基本上是由三個元素組成的字串：

1. 從生成電腦的系統時間衍生的時間戳
1. 用來區分使用相同時間戳記建立的修訂的計數器
1. 建立修訂的群集節點ID

* 分支

支援分支，可讓用戶端儲存多個變更，並透過單一合併呼叫加以顯示。

* 舊版檔案

MongoDB儲存通過每次修改將資料添加到文檔中。 但是，只有明確觸發清除時，才會刪除資料。 當符合特定臨界值時，舊資料會移動。 舊版檔案僅包含不可變的資料，這表示它們僅包含已提交和合併的修訂。

* 群集節點元資料

有關活動和非活動群集節點的資料保存在資料庫中，以便於群集操作。

具有MongoDB儲存空間的典型AEM叢集設定：

![chlimage_1-85](assets/chlimage_1-85.png)

## Jackrabbit 2有什麼不同？ {#what-is-different-from-jackrabbit}

由於Oak的設計是向後相容於JCR 1.0標準，所以使用者層級幾乎不會有任何變更。 不過，在設定Oak架構的AEM安裝時，您需要考慮一些明顯的差異：

* Oak不會自動建立索引。 因此，需要建立自定義索引。
* 與Jackrabbit 2不同，Jackrabbit 2中的作業一律會反映存放庫的最新狀態，而Oak a作業則會反映從取得作業時儲存庫的穩定檢視。 這是由於Oak所依據的MVCC模型。
* Oak中不支援同名同級(SNS)。

## 其他平台相關檔案 {#other-platform-related-documentation}

如需AEM平台的詳細資訊，請另行查看下列文章：

* [在AEM 6中設定節點儲存區和資料儲存區](/help/sites-deploying/data-store-config.md)
* [Oak查詢和索引](/help/sites-deploying/queries-and-indexing.md)
* [AEM 6中的儲存元素](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM與MongoDB](/help/sites-deploying/aem-with-mongodb.md)

