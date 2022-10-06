---
title: 編碼提示
seo-title: Coding Tips
description: AEM的編碼提示
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

## 請盡可能使用talib或HTL {#use-taglibs-or-htl-as-much-as-possible}

JSP中包含指令碼，使得在程式碼中對問題進行除錯變得困難。 另外，由於JSP中包含了指令碼，很難將業務邏輯與視圖層分離，這違反了單責原則和MVC設計模式。

### 寫入可讀代碼 {#write-readable-code}

程式碼只寫一次，但讀了很多次。 在前面花些時間清理我們編寫的代碼，會在將來支付紅利，因為我們和其他開發商需要稍後讀它。

### 選擇意圖顯示名稱 {#choose-intention-revealing-names}

理想情況下，另一個程式設計師不應該開啟一個模組來了解它的作用。 同樣，他們應該能夠在不閱讀方法的情況下分辨方法的作用。 訂閱這些想法越好，閱讀代碼就越容易，編寫和更改代碼的速度就越快。

在AEM程式碼基底中，會使用下列慣例：


* 介面的單一實作已命名為 `<Interface>Impl`，即 `ReaderImpl`.
* 介面的多個實施已命名 `<Variant><Interface>`，即 `JcrReader` 和 `FileSystemReader`.
* 抽象基類已命名 `Abstract<Interface>` 或 `Abstract<Variant><Interface>`.
* 已命名套件 `com.adobe.product.module`.  每個Maven工件或OSGi捆綁包必須有其自己的包。
* Java實作會放在其API下方的實作套件中。


請注意，這些慣例不一定需要套用至客戶實作，但請務必定義並遵守慣例，讓程式碼可持續維護。

理想情況下，名字應該顯示其意圖。 當名稱不如應有的清楚時，常見的程式碼測試是是否有說明變數或方法用途的註解：

<table>
 <tbody>
  <tr>
   <td><p><strong>不明</strong></p> </td>
   <td><p><strong>清除</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d;//間隔天數</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//獲取標籤的影像<br /> public list getItems(){}</p> </td>
   <td><p>public list getTaggedImages(){}</p> </td>
  </tr>
 </tbody>
</table>

### 別重複自己  {#don-t-repeat-yourself}

DRY指出，同一組程式碼絕不應重複。 這也適用於字串文字之類的項目。 每當有東西需要改變，需要尋找並消除時，代碼重複就會開啟缺陷的大門。

### 避免裸CSS規則 {#avoid-naked-css-rules}

CSS規則應該是應用程式內容中您的目標元素專屬。 例如，套用至的CSS規則 *.content.center* 會過於廣泛，並且可能最終影響到整個系統中的許多內容，要求其他人在未來覆蓋此樣式。 *.myapp-centertext* 會是更具體的規則，因為它指定了 *文字* 在應用程式的內容中。

### 避免使用已棄用的API {#eliminate-usage-of-deprecated-apis}

API遭取代時，最好找到新建議的方法，而非依賴已遭取代的API。 這將確保將來更順利的升級。

### 編寫可本地化的代碼 {#write-localizable-code}

任何非作者提供的字串，都應透過以下章節包裝在對AEM i18n字典的呼叫中： *I18n.get()* 在JSP/Java和 *CQ.I18n.get()* 在JavaScript中。 如果找不到實作，此實作會傳回傳遞至它的字串，因此在以主要語言實作功能後，這可提供實作本地化的彈性。

### 為安全而逸出資源路徑 {#escape-resource-paths-for-safety}

JCR中的路徑不應包含空格，但若路徑存在，則不應導致程式碼中斷。 Jackrabbit提供Text實用程式類別，其中 *escape()* 和 *escapePath()* 方法。 若為JSP,Granite UI會公開 *granite:encodeURIPath()EL* 函式。

### 使用XSS API和/或HTL來防止跨網站指令碼攻擊 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM提供XSS API，可輕鬆清除參數，並確保免受跨網站指令碼攻擊的安全性。 此外，HTL也直接在範本語言中內建這些保護功能。 API速查表可於下載 [開發 — 准則和最佳實務](/help/sites-developing/dev-guidelines-bestpractices.md).

### 實作適當的記錄 {#implement-appropriate-logging}

針對Java程式碼，AEM支援slf4j作為記錄訊息的標準API，且應與透過OSGi主控台提供的設定搭配使用，以便在管理上保持一致。 Slf4j會公開五個不同的記錄層級。 選擇要記錄訊息的層級時，建議您使用下列准則：

* 錯誤：當程式碼中斷時，處理無法繼續。 這通常會因為意外的例外而發生。 在這些案例中加入堆疊追蹤通常會很有幫助。
* 警告：當某個項目未正常運作時，但處理可繼續。 這通常會是我們預期的例外結果，例如 *PathNotFoundException*.
* 資訊：監視系統時有用的資訊。 請記住，這是預設值，大部分客戶都會在其環境中保留此設定。 因此，請勿過度使用。
* 調試：關於處理的較低層級資訊。 在偵錯支援問題時很實用。
* TRACE:最低層級資訊，例如輸入/退出方法。 這通常僅供開發人員使用。

在JavaScript的案例中， *console.log* 只應在開發期間使用，且應在發行前移除所有記錄陳述式。

### 避免貨物崇拜程式設計 {#avoid-cargo-cult-programming}

若不了解程式碼的功能，請避免復製程式碼。 有疑問時，最好詢問對您不清楚的模組或API有更多經驗的人。
