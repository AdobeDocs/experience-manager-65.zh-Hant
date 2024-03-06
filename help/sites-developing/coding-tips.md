---
title: 編碼提示
description: 瞭解在Adobe Experience Manager中編碼最佳實務的一些提示。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 編碼提示{#coding-tips}

## 儘可能使用taglibs或HTL {#use-taglibs-or-htl-as-much-as-possible}

在JSP中包含Scriptlet會使得在程式碼中偵錯問題變得困難。 此外，若在JSP中加入Scriptlet，就很難將商業邏輯與檢視層分開，這違反了單一職責原則和MVC設計模式。

### 寫入可讀取的程式碼 {#write-readable-code}

程式碼只會寫入一次，但會讀取許多次。 您和其他開發人員稍後會閱讀程式碼，預先花一些時間清除程式碼會支付後續的紅利。

### 選擇揭示意向的名稱 {#choose-intention-revealing-names}

理想情況下，另一個程式設計師不必開啟模組來瞭解它的功能。 同樣地，他們應該能夠在不閱讀方法的情況下判斷方法的作用。 您訂閱這些想法的能力越強，程式碼就越容易閱讀，而且編寫和變更程式碼的速度也會越快。

在AEM程式碼基底中，使用下列慣例：


* 介面的單一實作命名為 `<Interface>Impl`，也就是 `ReaderImpl`.
* 介面的多個實作已命名 `<Variant><Interface>`，也就是 `JcrReader` 和 `FileSystemReader`.
* 抽象基底類別已命名 `Abstract<Interface>` 或 `Abstract<Variant><Interface>`.
* 封裝已命名 `com.adobe.product.module`. 每個Maven成品或OSGi套件組合都必須有自己的套件。
* Java™實作會放置在其API下方的實作套件中。


這些慣例不一定適用於客戶實作，但請務必定義並遵守慣例，才能讓程式碼持續可供維護。

理想情況下，名稱應該顯示其意圖。 當名稱不夠清楚時，常見的程式碼測試是存在說明變數或方法用途的註解：

<table>
 <tbody>
  <tr>
   <td><p><strong>不清楚</strong></p> </td>
   <td><p><strong>清除</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d； //經過的時間（以天為單位）</p> </td>
   <td><p>int elapsedTimeInDays；</p> </td>
  </tr>
  <tr>
   <td><p>//取得標籤的影像<br /> 公用清單getItems() {}</p> </td>
   <td><p>公用清單getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### 不要重複您自己的動作  {#don-t-repeat-yourself}

DRY表示同一組程式碼絕不應重複。 這也適用於字串常值等。 程式碼複製會開啟任何必須變更的瑕疵之門，而且應該尋找並消除瑕疵。

### 避免使用裸露的CSS規則 {#avoid-naked-css-rules}

CSS規則應為應用程式內容中目標元素的特定規則。 例如，套用至 *.content .center* 過於廣泛，最終可能會影響您系統中的許多內容，導致其他人日後需要覆寫此風格。 然而， *.myapp-centertext* 將會是更明確的規則，因為它會指定「置中」 *文字* （在應用程式的內容中）。

### 避免使用過時的API {#eliminate-usage-of-deprecated-apis}

API一經棄用，最好尋找新的建議方法，而非依賴已棄用的API。 這將確保未來能更順利地升級。

### 撰寫可當地語系化的程式碼 {#write-localizable-code}

任何不是由作者提供的字串，都應包裝在AEM i18n字典的呼叫中，透過 *I18n.get()* 在JSP/Java和 *CQ.I18n.get()* 在JavaScript中。 如果找不到實作，此實作會傳回傳遞至它的字串，因此在使用主要語言實作功能後，如此可提供實作本地化的彈性。

### 為安全逸出資源路徑 {#escape-resource-paths-for-safety}

雖然JCR中的路徑不應包含空格，但它們的存在不應導致程式碼中斷。 Jackrabbit提供的文字公用程式類別包含 *escape()* 和 *escapePath()* 方法。 若為JSP，Granite UI會公開 *granite：encodeURIPath() EL* 函式。

### 使用XSS API和/或HTL來抵禦跨網站指令碼攻擊 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM提供的XSS API可輕鬆清除引數，並確保安全性不受跨網站指令碼攻擊。 此外，HTL也將這些保護功能直接內建在範本語言中。 API速查表可於以下網址下載： [開發 — 指導方針與最佳作法](/help/sites-developing/dev-guidelines-bestpractices.md).

### 實作適當的記錄 {#implement-appropriate-logging}

對於Java™程式碼，AEM支援slf4j作為記錄訊息的標準API，並且應該與透過OSGi主控台提供的設定一起使用，以確保管理的一致性。 Slf4j會公開五個不同的記錄層級。 Adobe建議在選擇要在哪個層級記錄訊息時遵循下列准則：

* 錯誤：當程式碼中的某些專案中斷時，處理無法繼續。 這通常會發生於非預期的例外狀況。 在這些情況下包含棧疊追蹤會很有幫助。
* 警告：當某些專案未正常運作，但處理作業可以繼續進行。 這通常是我們所預期的例外狀況的結果，例如 *PathNotFoundException*.
* INFO：監視系統時有用的資訊。 請記住，這是預設值，並且大多數客戶會在他們的環境中保留此設定。 因此，請勿過度使用。
* DEBUG：處理的低階資訊。 對具有支援的問題進行偵錯時很有用。
* TRACE：最低層級的資訊，例如輸入/結束方法。 這通常僅供開發人員使用。

如果有JavaScript， *console.log* 應僅在開發期間使用，且應在發行之前移除所有記錄陳述式。

### 避免狂熱的貨運程式設計 {#avoid-cargo-cult-programming}

避免復製程式碼而不瞭解其功能。 如有疑問，最好是詢問對模組或API有較豐富經驗，但您未詳加瞭解的人。
