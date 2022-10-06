---
title: 內容架構
seo-title: Content Architecture
description: 設計內容的秘訣（提示 — 一切都是內容）
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

# 內容架構{#content-architecture}

## 追隨大衛的模式 {#follow-david-s-model}

《大衛的模型》是幾年前由大衛·紐謝勒寫的，但思想在今天仍然成立。 David&#39;s Model的主要原則如下：

* 資料首先，結構之後。 也許吧。
* 驅動內容階層，別讓它發生。
* 工作區適用於 `clone()`, `merge()`，和 `update()`.
* 請注意同名同胞。
* 引用被認為有害。
* 檔案是檔案。
* 身份是邪惡的。

David&#39;s Model可在Jackrabbit Wiki上找到，網址為 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### 一切都是內容 {#everything-is-content}

所有內容都應儲存在儲存庫中，而不是依賴獨立的第三方資料來源，例如資料庫。 這適用於製作內容、二進位資料，例如影像、程式碼、設定等。 這可讓我們使用一組API來管理所有內容，並透過復寫管理此內容的促銷活動。 我們還獲得了備份、日誌記錄等單一源。

### 使用「內容模型優先」的設計原則 {#use-the-content-model-first-design-principle}

建置新功能時，請一律從設計JCR內容結構開始，然後使用預設的Sling servlet來研究讀取和撰寫內容。 這可讓您確保實施可搭配現成的存取控制機制正常運作，並避免產生不必要的CRUD樣式servlet。

### RESTful {#be-restful}

Servlet應根據resourceTypes而非路徑來定義。 這可讓您使用JCR存取控制、遵循REST原則，以及使用要求中提供給我們的資源和資源解析程式。 這也可讓我們變更在伺服器端轉譯URL的指令碼，而不需從用戶端變更任何URL，同時從用戶端隱藏伺服器端實作詳細資訊，以提高安全性。

### 避免定義新的節點類型 {#avoid-defining-new-node-types}

節點類型在基礎結構層中處於較低的級別，而大多數要求都可以通過使用分配給nt:unstructured、oak:Unstructured、sling:Folder或cq:Page節點類型的sling:resourceType來滿足。 節點類型等於儲存庫中的架構，而更改節點類型可能非常昂貴。

### 遵循JCR中的命名慣例 {#adhere-to-naming-conventions-in-the-jcr}

遵循命名慣例可增加程式碼庫的一致性、降低缺陷發生率，並提高開發人員在系統中工作的速度。 Adobe在開發AEM時會使用下列慣例：

* 節點名稱

   * 全部小寫
   * 使用連字型大小分詞

* 屬性名稱

   * 駝峰式大小寫，以小寫字母開頭

* 元件(JSP/HTML)

   * 全部小寫
   * 使用連字型大小分詞
