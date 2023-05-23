---
title: 內容體系結構
seo-title: Content Architecture
description: 設計內容的提示（提示 — 所有內容都是內容）
seo-description: Tips for architecting your content in Adobe Experience Manager (AEM). (hint - everything is content)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# 內容體系結構{#content-architecture}

## 關注大衛的模式 {#follow-david-s-model}

大衛的模型是大衛·紐切勒幾年前寫的，但是今天的觀點是成立的。 David&#39;s Model的主要原則如下：

* 資料先，結構後。 也許吧。
* 驅動內容層次結構，不要讓它發生。
* 工作區 `clone()`。 `merge()`, `update()`。
* 注意同名兄弟姐妹。
* 參考被認為有害。
* 檔案是檔案。
* 身份證是邪惡的。

David&#39;s Model可在Jackrabbit維客上找到 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)。

### 一切都是內容 {#everything-is-content}

所有內容都應儲存在儲存庫中，而不是依賴於單獨的第三方資料源。 這適用於創作內容、二進位資料（如影像、代碼、配置等）。 這允許我們使用一組API來管理所有內容，並通過複製管理此內容的升級。 我們還獲得了備份、日誌記錄等單一來源。

### 運用&quot;內容模型優先&quot;設計原則 {#use-the-content-model-first-design-principle}

構建新功能時，請始終先設計JCR內容結構，然後使用預設的Sling Servlet查看內容的讀寫。 這樣，您就可以確保實現在開箱即用的訪問控制機制下運行良好，並避免生成不必要的CRUD樣式的Servlet。

### 為REST風格 {#be-restful}

Servlet應基於resourceTypes而不是路徑進行定義。 這使得可以使用JCR訪問控制，遵守REST原則，以及使用請求中提供給我們的資源和資源解析器。 這還允許我們更改在伺服器端呈現URL的指令碼，而無需更改客戶端的任何URL，同時隱藏客戶端實現詳細資訊以增加安全性。

### 避免定義新節點類型 {#avoid-defining-new-node-types}

節點類型在基礎結構層處於較低級別，通過使用分配給nt:atroblected、oak:Antrography、sling:Folder或cq:Page節點類型的sling:resourceType可滿足大多數要求。 節點類型等於儲存庫中的模式，而更改節點類型在將來可能會非常昂貴。

### 遵守JCR中的命名約定 {#adhere-to-naming-conventions-in-the-jcr}

遵守命名約定將增加代碼庫的一致性，降低缺陷發生率並提高開發人員在系統中工作的速度。 Adobe在制定方案時使用了以下公AEM約：

* 節點名稱

   * 全部小寫
   * 使用連字元的單詞分隔

* 屬性名稱

   * 駝峰，以小寫字母開頭

* 元件(JSP/HTML)

   * 全部小寫
   * 使用連字元的單詞分隔
