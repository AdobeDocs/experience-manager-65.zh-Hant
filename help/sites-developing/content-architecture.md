---
title: 內容架構
description: 設計內容架構的秘訣（提示 — 一切都是內容）
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# 內容架構{#content-architecture}

## 遵循David的模式 {#follow-david-s-model}

David&#39;s Model是David Nuescheler多年前所寫的，但今天仍然適用。 David模型的主要原則如下：

* 先取得資料，再建構。 也許吧。
* 推動內容階層，不要讓它發生。
* 工作區用於 `clone()`， `merge()`、和 `update()`.
* 注意同名的同層級。
* 參照會被視為有害。
* 檔案是檔案。
* ID是邪惡的。

David的模型可在Jackrabbit wiki上找到，網址為 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### 一切都是內容 {#everything-is-content}

所有資料都應儲存在存放庫中，而非依賴獨立的第三方資料來源，例如資料庫。 這會套用至編寫的內容、二進位資料，例如影像、程式碼和設定。 這可讓我們使用一組API來管理所有內容，並透過復寫管理此內容的促銷活動。 您還能取得備份、記錄等的單一來源。

### 使用「內容模型優先」設計原則 {#use-the-content-model-first-design-principle}

建立新功能時，請一律先設計JCR內容結構，然後考慮使用預設的Sling servlet來讀取和寫入內容。 這可讓您確保實作可搭配現成的存取控制機制運作，並避免產生不必要的CRUD式servlet。

### 成為RESTful {#be-restful}

Servlet應該根據resourceTypes而不是路徑來定義。 這可讓您使用JCR存取控制、遵守REST原則，並使用在請求中提供給我們的資源和資源解析器。 這也讓我們能夠變更在伺服器端轉譯URL的指令碼，而不需要變更使用者端的URL，同時隱藏使用者端的伺服器端實作詳細資料，以提升安全性。

### 避免定義新的節點型別 {#avoid-defining-new-node-types}

節點型別在基礎結構層的低層級運作，且大多數需求都可透過使用指派給nt：unstructured、oak：Unstructured、sling：Folder或cq：Page節點型別的sling：resourceType來滿足。 節點型別等同於存放庫中的結構描述，並且之後變更節點型別可能會很昂貴。

### 遵守JCR中的命名慣例 {#adhere-to-naming-conventions-in-the-jcr}

遵循命名慣例可為程式碼庫增加一致性，降低缺陷的發生率，並提升開發人員在系統中工作的速度。 Adobe在開發AEM時會使用下列慣例：

* 節點名稱

   * 全部小寫
   * 使用連字型大小分隔文字

* 屬性名稱

   * 駝峰式大小寫，以小寫字母開頭

* 元件(JSP/HTML)

   * 全部小寫
   * 使用連字型大小分隔文字
