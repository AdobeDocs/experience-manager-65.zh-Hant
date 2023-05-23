---
title: 編碼提示
seo-title: Coding Tips
description: 編碼提AEM示
seo-description: Tips for coding for AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 編碼提示{#coding-tips}

## 盡可能使用taglib或HTL {#use-taglibs-or-htl-as-much-as-possible}

在JSP中包含scriptlet使得很難調試代碼中的問題。 另外，在JSP中加入Scriptlet，很難將業務邏輯與視圖層分離，這違反了單責原則和MVC設計模式。

### 寫入可讀代碼 {#write-readable-code}

代碼只寫一次，但讀多次。 花點時間清理我們編寫的代碼會在將來派發紅利，因為我們和其他開發商需要以後再讀它。

### 選擇意圖揭示名稱 {#choose-intention-revealing-names}

理想情況下，另一個程式設計師不必開啟一個模組來瞭解其功能。 同樣，他們應該能夠在不閱讀的情況下判斷某個方法的作用。 我們越能訂閱這些想法，就越容易閱讀我們的代碼，我們越能夠編寫和更改代碼。

在代AEM碼庫中，使用以下約定：


* 介面的單個實現稱為 `<Interface>Impl`，即 `ReaderImpl`。
* 介面的多個實現被命名 `<Variant><Interface>`，即 `JcrReader` 和 `FileSystemReader`。
* 抽象基類被命名 `Abstract<Interface>` 或 `Abstract<Variant><Interface>`。
* 已命名包 `com.adobe.product.module`。  每個Maven藏物或OSGi捆綁包必須有其自己的包。
* Java實現放置在其API下的impl包中。


請注意，這些約定不一定需要適用於客戶實施，但必須定義並遵守約定，以便代碼能夠保持可維護性。

理想情況下，名字應該表明自己的意圖。 當名稱不像應該那樣清晰時，常見的代碼test是提供說明變數或方法的用途的注釋：

<table>
 <tbody>
  <tr>
   <td><p><strong>不清</strong></p> </td>
   <td><p><strong>清除</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d;//已用時間（天）</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>/獲取標籤影像<br /> 公共清單getItems(){}</p> </td>
   <td><p>公共清單getTaggedImages(){}</p> </td>
  </tr>
 </tbody>
</table>

### 別再重複  {#don-t-repeat-yourself}

DRY指出，不應複製同一組代碼。 這也適用於字串文字之類的內容。 每當有事情需要改變，需要尋找和消除時，代碼複製就會為缺陷開啟大門。

### 避免裸CSS規則 {#avoid-naked-css-rules}

CSS規則應特定於應用程式上下文中的目標元素。 例如，應用於 *.cont.center* 將過於廣泛，最終可能會影響整個系統中的大量內容，要求其他人在將來覆蓋此樣式。 *.myapp中心文本* 將是更具體的規則，因為它指定居中 *文本* 的子菜單。

### 消除過時API的使用 {#eliminate-usage-of-deprecated-apis}

當API被棄用時，總是最好找到新的推薦方法，而不是依賴棄用的API。 這將確保將來更順利的升級。

### 寫入可本地化代碼 {#write-localizable-code}

不由作者提供的任何字串都應通過i18n字典的調AEM用包裝 *I18n.get()* 在JSP/Java和 *CQ.I18n.get()* 中。 如果未找到實現，此實現將返回傳遞給它的字串，因此在以主要語言實現這些功能後，這提供了實現本地化的靈活性。

### 為安全而轉義資源路徑 {#escape-resource-paths-for-safety}

雖然JCR中的路徑不應包含空格，但是它們的存在不應導致代碼中斷。 Jackrabbit提供Text實用程式類 *轉義()* 和 *轉義路徑()* 的雙曲餘切值。 對於JSP,Granite UI會顯示 *花崗岩：encodeURIPath()EL* 的子菜單。

### 使用XSS API和/或HTL防止跨站點指令碼攻擊 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

提AEM供XSS API以便於清除參數並確保跨站點指令碼攻擊的安全性。 此外，HTL還將這些保護直接內置到模板語言中。 API作弊表可在下載 [開發 — 指南和最佳做法](/help/sites-developing/dev-guidelines-bestpractices.md)。

### 實施適當的日誌記錄 {#implement-appropriate-logging}

對於Java代碼AEM，支援slf4j作為記錄消息的標準API，並應與通過OSGi控制台提供的配置一起使用，以便在管理中保持一致。 SLF4j顯示五個不同的日誌記錄級別。 我們建議在選擇在以下位置記錄消息的級別時使用以下准則：

* 錯誤：當代碼中的某些內容已損壞，處理無法繼續。 這通常是意外異常的結果。 通常，將這些堆棧跟蹤包括在這些場景中會有所幫助。
* 警告：當某個東西沒有正常工作，但處理可以繼續。 這通常是我們預期的一個例外的結果，例如 *PathNotFoundException*。
* 資訊：在監視系統時有用的資訊。 請記住，這是預設值，大多數客戶都會在其環境中保留此值。 所以，不要過度使用。
* 調試：有關處理的較低級別資訊。 在調試支援問題時非常有用。
* TRACE:最低級別資訊，如輸入/退出方法。 通常只供開發人員使用。

對於JavaScript, *控制台.log* 只應在開發過程中使用，所有日誌語句都應在發佈前刪除。

### 避免貨物崇拜寫程式 {#avoid-cargo-cult-programming}

避免在不瞭解代碼功能的情況下複製代碼。 在有疑問時，最好詢問對您不清楚的模組或API有更多經驗的人。
