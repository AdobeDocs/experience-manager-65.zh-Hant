---
title: 編碼提示
seo-title: 編碼提示
description: AEM的編碼秘訣
seo-description: AEM的編碼秘訣
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 編碼提示{#coding-tips}

## 請盡量使用標語或HTL {#use-taglibs-or-htl-as-much-as-possible}

在JSP中加入scriptlet，讓程式碼中的問題難以除錯。 此外，在JSP中加入scriptlet，將商業邏輯與檢視層分離很困難，這違反了「單一責任原則」和MVC設計模式。

### 編寫可讀代碼 {#write-readable-code}

程式碼只寫一次，但會讀多次。 花點時間清理我們編寫的程式碼，將可派上用場，因為我們和其他開發人員日後需要閱讀它。

### 選擇意圖揭示名稱 {#choose-intention-revealing-names}

理想情況下，另一個程式設計師不必開啟一個模組來瞭解它的功能。 同樣，他們應該能夠在不閱讀的情況下分辨方法的作用。 我們訂閱這些概念越好，閱讀程式碼就越容易，撰寫和變更程式碼的速度就越快。

在AEM程式碼庫中，會使用下列慣例：


* 一個介面的單個實現被命名 `<Interface>Impl`為，即： `ReaderImpl`。
* 命名介面的多個實 `<Variant><Interface>`施，即 `JcrReader` 和 `FileSystemReader`。
* 抽象基類是指 `Abstract<Interface>` 定或 `Abstract<Variant><Interface>`。
* 包的名稱 `com.adobe.product.module`。  每個Maven藏物或OSGi包裹都必須有其專屬的套件。
* Java實作會放在其API下方的實施套件中。


請注意，這些慣例不一定需要套用至客戶實作，但必須定義並遵循這些慣例，如此才能維持程式碼的可維護性。

理想情況下，名字應該能夠顯示其意圖。 當名稱不如應該清楚時，常見的程式碼測試是有注釋，說明變數或方法的用途：

<table>
 <tbody>
  <tr>
   <td><p><strong>不清楚</strong></p> </td>
   <td><p><strong>清除</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d;//已用時間（天數）</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get tagged images<br /> public List getItems(){}</p> </td>
   <td><p>public List getTaggedImages(){}</p> </td>
  </tr>
 </tbody>
</table>

### 別再重複一遍 {#don-t-repeat-yourself}

DRY指出，不應複製相同的程式碼集。 這也適用於字串文字之類的項目。 當有需要改變、需要尋找和消除的情況時，程式碼複製會為缺陷開啟大門。

### 避免裸體CSS規則 {#avoid-naked-css-rules}

CSS規則應該是應用程式內容中特定的目標元素。 例如，套用至 *.content.center的CSS規則會過於廣泛* ，而且可能會影響您系統內的許多內容，讓其他人在未來覆寫此樣式。 *.myapp-centertext會是更特定的規則* ，因為它會在應用程式的內容中 *指定置中文* 。

### 免除淘汰API的使用 {#eliminate-usage-of-deprecated-apis}

當API已停用時，最好尋找新的建議方法，而不是依賴已停用的API。 這可確保未來升級更順暢。

### 編寫可本地化代碼 {#write-localizable-code}

任何非由作者提供的字串，都應以JSP/Java中的 *I18n.get()* 、 ** CQ.I18n.get()JavaScript中對AEM i18n字典的呼叫包住。 如果找不到實作，此實作會傳回傳遞給它的字串，因此，在以主要語言實作功能後，這可提供實作本地化的彈性。

### 為安全而逸出資源路徑 {#escape-resource-paths-for-safety}

雖然JCR中的路徑不應包含空格，但路徑的存在不應造成程式碼中斷。 Jackrabbit提供Text公用程式類 *別及escape()**和escapePath()* 方法。 對於JSP,Granite UI會公開 *granite:encodeURIPath()EL函式* 。

### 使用XSS API和／或HTL來防止跨網站指令碼攻擊 {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM提供XSS API，可輕鬆清除參數，並確保避免跨網站指令碼攻擊。 此外，HTL也直接在範本語言中內建這些保護。 您可在「開發——准則與最佳實務」中 [下載API快速參考表](/help/sites-developing/dev-guidelines-bestpractices.md)。

### 實作適當的記錄 {#implement-appropriate-logging}

對於Java程式碼，AEM支援slf4j做為記錄訊息的標準API，而且應與透過OSGi主控台提供的組態搭配使用，以利於管理的一致性。 Slf4j暴露了5種不同的記錄級別。 建議您在選擇要在哪個級別上記錄消息時使用以下准則：

* 錯誤：當程式碼中有任何內容中斷，處理無法繼續。 這通常會因為意外的例外而發生。 在這些案例中加入堆疊追蹤通常很有幫助。
* 警告：當某個項目無法正常運作時，但處理仍可繼續。 這通常是我們預期的例外結果，例如 *PathNotFoundException*。
* 資訊：在監視系統時有用的資訊。 請記住，這是預設值，大部分客戶都會在其環境中保留此值。 因此，請勿過度使用。
* 除錯：關於處理的較低層級資訊。 在除錯支援問題時很有用。
* 跟蹤：最低層資訊，例如輸入／退出方法。 這通常僅供開發人員使用。

在JavaScript的情況下， *僅應在開發期間使用console.log* ，所有記錄陳述式應在發行前移除。

### 避免貨物崇拜程式設計 {#avoid-cargo-cult-programming}

毋需復製程式碼，而不需瞭解其功能。 在有疑問時，最好詢問您對模組或API有較多經驗且不清楚的人。
