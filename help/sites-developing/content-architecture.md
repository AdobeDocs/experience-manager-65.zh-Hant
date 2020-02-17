---
title: 內容架構
seo-title: 內容架構
description: 設計內容架構的秘訣（提示——一切都是內容）
seo-description: 在Adobe Experience Manager(AEM)中建立內容架構的秘訣。 （提示——一切皆為內容）
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 內容架構{#content-architecture}

## 關注David的模型 {#follow-david-s-model}

David』s Model是David Nuescheler幾年前寫的，但其想法今天仍然成立。 David』s Model的主要原則如下：

* 資料先來，結構後來。 也許吧。
* 推動內容階層，別讓它發生。
* 工作區適 `clone()`用於 `merge()`、和 `update()`。
* 小心同名兄弟姐妹。
* 參照被認為有害。
* 檔案是檔案。
* 身份證是邪惡的。

David』s Model可在Jackrabbit wiki上找到，網址為 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)。

### 一切都是內容 {#everything-is-content}

所有內容都應儲存在儲存庫中，而不是依賴單獨的第三方資料源（如資料庫）。 這適用於製作內容、二進位資料（例如影像、程式碼、設定等）。 這可讓我們使用一組API來管理所有內容，並透過複製來管理此內容的促銷。 我們還獲得了單一備份、日誌記錄等源。

### 使用「內容模型優先」的設計原則 {#use-the-content-model-first-design-principle}

建立新功能時，請務必先設計JCR內容結構，然後使用預設的Sling servlet來閱讀和寫入內容。 這可讓您確保實作能順利運用現成可用的存取控制機制，並避免產生不必要的CRUD樣式servlet。

### REST風格 {#be-restful}

Servlet應根據resourceTypes而非路徑來定義。 這樣，您就可以使用JCR存取控制、遵循REST原則，以及使用在要求中提供給我們的資源和資源解析程式。 這也允許我們變更在伺服器端轉換URL的指令碼，而不需從用戶端變更任何URL，同時隱藏伺服器端實作詳細資訊，以增加安全性。

### 避免定義新節點類型 {#avoid-defining-new-node-types}

節點類型在基礎架構層的低層運作，而且大部分需求都可透過使用指派給nt:unstructured, oak:Unstructured, sling:Folder或cq:Page節點類型的sling:resourceType來滿足。 節點類型等於儲存庫中的模式，而更改節點類型在將來可能會非常昂貴。

### 遵循JCR中的命名慣例 {#adhere-to-naming-conventions-in-the-jcr}

遵循命名慣例可為程式碼庫增加一致性，降低缺陷發生率，並提高開發人員在系統中工作的速度。 Adobe在開發AEM時會使用下列慣例：

* 節點名稱

   * 全部小寫
   * 使用連字型大小分詞

* 屬性名稱

   * 駝峰大小寫，以小寫字母開始

* 元件(JSP/HTML)

   * 全部小寫
   * 使用連字型大小分詞

