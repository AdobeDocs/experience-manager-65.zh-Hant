---
title: 資料建模 — 大衛·紐謝勒模型
seo-title: Data Modeling - David Nuescheler's Model
description: 大衛·紐謝勒的內容建模建議
seo-description: David Nuescheler's content modelling recommendations
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 0%

---

# 資料建模 — 大衛·紐謝勒模型{#data-modeling-david-nuescheler-s-model}

## 來源 {#source}

以下是David Nuescheler所表達的觀點和評論。

David是Day Software AG的聯合創始人兼首席技術官，Day Software AG是全球內容管理和內容基礎架構軟體的領先提供商，於2010年被Adobe收購。 他現在是企業技術部Adobe部的資深和副總裁，還領導著JSR-170的開發，JSR-170是Java內容儲存庫(JCR)應用程式寫程式介面(API)，這是內容管理的技術標準。

還可以在 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)。

## David簡介 {#introduction-from-david}

在各種討論中，我發現，在內容建模方面，開發人員對JCR提供的特性和功能有些不安。 在如何對儲存庫中的內容建模以及為什麼一個內容模型比其他內容模型更好方面，目前尚無指南和極少的經驗。

雖然在關係世界中，軟體行業在如何建模資料方面有許多經驗，但我們仍然處於內容儲存庫空間的早期階段。

我想開始填補這個空白，通過表達我對內容應如何建模的個人意見，希望有一天，這能成為對開發人員社區更有意義的東西，這不僅是&quot;我的意見&quot;，而是更普遍適用的東西。 所以請考慮一下我快速進化的第一次嘗試。

>[!NOTE]
>
>免責聲明：這些准則表達了我個人的、有時還有爭議的觀點。 我期待著就這些准則進行辯論並加以完善。

## 七條簡單規則 {#seven-simple-rules}

### 規則#1:資料先，結構後。 也許吧。 {#rule-data-first-structure-later-maybe}

#### 解釋 {#explanation-1}

我建議不要擔心ERD意義上的聲明資料結構。 最初。

學習在開發中喜歡nt：非結構化（和朋友）。

我認為斯特凡諾差不多是這個結論。

我的底線是：結構非常昂貴，在很多情況下完全沒有必要向基礎儲存明確聲明結構。

對於應用程式本身使用的結構，有一種隱含的約定。 假設我將部落格帖子的修改日期儲存在lastModified屬性中。 My App將自動知道從同一屬性再次讀取修改日期，因此實際上不需要明確聲明該日期。

只有在出於資料完整性原因需要時才應應用其他資料約束，如強制約束或類型約束和值約束。

#### 範例 {#example-1}

上面的示例使用 `lastModified` 例如，「部落格帖子」節點上的Date屬性並不表示需要特殊的nodetype。 我肯定會用 `nt:unstructured` 至少最初是為我的部落格帖子節點。 因為在我的部落格應用程式中，我要做的就是顯示上次修改的日期（可能是「訂購日期」），我幾乎不在乎它是否是日期。 由於我暗中信任我的部落格寫作應用程式在上面寫一個「日期」，因此實際上沒有必要聲明 `lastModified` 日期。

### 規則#2:驅動內容層次結構，不要讓它發生。 {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 解釋 {#explanation-2}

內容層次結構是一項非常有價值的資產。 所以，不要讓它發生，設計它。 如果你沒有一個「好」的、可以讀取的節點名稱，那麼你可能應該重新考慮。 武斷的數字從來都不是「好名字」。

雖然將現有關係模型快速放入分層模型可能非常容易，但在此過程中應該考慮一些問題。

根據我的經驗，如果人們認為訪問控制和控制通常是內容層次結構的良好驅動因素。 把它想成是你的檔案系統。 甚至可以使用檔案和資料夾在本地磁碟上對其進行建模。

我個人比較喜歡在最初的很多情況下採用等級慣例，而不是鍵入系統，並在以後引入鍵入。

>[!CAUTION]
>
>內容儲存庫的結構方式也會影響效能。 為獲得最佳效能，連接到內容儲存庫中各個節點的子節點數通常不應超過1&#39;00。
>
>請參閱 [CRX可以處理多少資料？](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) 的子菜單。

#### 範例 {#example-2}

我會給一個簡單的部落格系統建模如下。 請注意，最初我甚至不關心在此時使用的各個節點類型。

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

我認為一個顯而易見的事實是我們都理解內容的結構基於這個例子而沒有任何進一步的解釋

最初可能出乎意料的是，我為什麼不將「注釋」與「post」一起儲存，這是由於訪問控制，我希望以合理的分層方式應用訪問控制。

使用上述內容模型，我可以輕鬆地允許「匿名」用戶「建立」注釋，但保留匿名用戶在工作區的其餘部分為只讀狀態。

### 規則#3:工作區用於clone()、merge()和update()。 {#rule-workspaces-are-for-clone-merge-and-update}

#### 解釋 {#explanation-3}

如果你不用 `clone()`。 `merge()` 或 `update()` 方法在應用程式中使用單個工作區可能是一種方法。

「對應節點」是JCR規範中定義的概念。 本質上，它歸結為表示不同所謂工作區中相同內容的節點。

JCR引入了Workspaces非常抽象的概念，這使得許多開發人員不清楚如何處理它們。 我建議將工作區的使用放在下面進行test。

如果多個工作區中「對應」節點（實際上是具有相同UUID的節點）有相當大的重疊，則您可能會使工作區得到充分利用。

如果沒有具有相同UUID的節點重疊，則您可能正在濫用工作區。

工作區不應用於訪問控制。 特定用戶組的內容可見性不是將內容分離到不同工作區的好參數。 JCR在內容儲存庫中提供「訪問控制」功能。

工作區是參照和查詢的邊界。

#### 範例 {#example-3}

將工作區用於以下內容：

* 項目v1.2與項目v1.3
* &quot;開發&quot;、&quot;QA&quot;和&quot;已發佈&quot;的內容狀態

不要將工作區用於以下內容：

* 用戶主目錄
* 針對不同目標受眾的不同內容，如公共、私有、本地……
* 不同用戶的郵箱

### 規則#4:小心同名兄弟姐妹。 {#rule-beware-of-same-name-siblings}

#### 解釋 {#explanation-4}

雖然同名同級(SNS)已引入規範中，以允許與為XML設計並通過XML表示的資料結構相容，因此對JCR極為有價值，但SNS對儲存庫而言具有巨大的開銷和複雜性。

進入內容儲存庫的任何路徑在其路徑段中包含SNS都會變得不那麼穩定，如果刪除或重新排序了SNS，它會影響所有其他SNS及其子代的路徑。

對於導入XML或與現有XML SNS的交互，可能是必要且有用的，但我從未使用過SNS，並且永遠不會在我的「綠色欄位」資料模型中使用。

#### 範例 {#example-4}

使用

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

而不是

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### 規則#5:被認為有害的參考。 {#rule-references-considered-harmful}

#### 解釋 {#explanation-5}

引用暗示參照完整性。 我發現，重要的是要瞭解，引用不僅為管理引用完整性的儲存庫增加了額外成本，而且從內容靈活性的角度來說，這些引用還成本高昂。

就個人而言，我確保只有在我真的無法處理懸掛引用時才使用引用，否則，請使用路徑、名稱或字串UUID來引用另一個節點。

#### 範例 {#example-5}

假設我允許從文檔(a)到另一文檔(b)的&quot;引用&quot;。 如果我使用引用屬性對此關係建模，則意味著兩個文檔在儲存庫級別上連結。 無法單獨導出/導入文檔(a)，因為引用屬性的目標可能不存在。 其他操作（如合併、更新、恢復或克隆）也會受到影響。

因此，我要麼將這些引用建模為「弱引用」（在JCR v1.0中，這基本上可以歸結為字串屬性，這些屬性包含目標節點的uuid），要麼只是使用路徑。 有時，這條路會更有意義。

我認為有些使用例子，如果一個參照物懸著，一個系統真的無法工作，但我無法從我的直接經驗中得出一個好的「真實」而簡單的例子。

### 規則#6:檔案是檔案。 {#rule-files-are-files}

#### 解釋 {#explanation-6}

如果內容模型公開的內容甚至遠程 *聞聞* 例如我嘗試使用（或從中擴展）的檔案或資料夾 `nt:file`。 `nt:folder` 和 `nt:resource`。

根據我的經驗，許多通用應用程式都允許與nt:folder和nt:files隱式交互，並且知道如何處理和顯示這些事件（如果這些事件被附加的元資訊所豐富）。 例如，與位於JCR頂部的CIFS或WebDAV等檔案伺服器實現的直接交互變為隱式。

我認為，作為一個好的經驗法則，你可以使用以下方法：如果需要儲存檔案名和mime類型， `nt:file`/ `nt:resource` 很配。 如果可以有多個「檔案」，則nt:folder是儲存這些檔案的好地方。

如果需要為資源添加元資訊，例如「作者」或「描述」屬性，請擴展 `nt:resource` 不是 `nt:file`。 我很少擴展nt：檔案，並且經常擴展 `nt:resource`。

#### 範例 {#example-6}

假設有人希望將影像上載到部落格條目：

```xml
/content/myblog/posts/iphone_shipping
```

也許最初的腸胃反應是添加一個包含圖片的二進位屬性。

雖然在這種情況下，當然有很好的使用案例，只使用二進位屬性（假設名稱不相關且mime類型是隱式的），但我建議為我的部落格示例使用以下結構。

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 規則#7:身份證是邪惡的。 {#rule-ids-are-evil}

#### 解釋 {#explanation-7}

在關係資料庫中，ID是表達關係的必要手段，因此人們也傾向於在內容模型中使用它們。 主要是因為錯誤的原因。

如果內容模型包含以「ID」結尾的屬性，則可能未正確利用層次結構。

確實，某些節點在其整個生命週期中都需要穩定的識別。 比你想的要少。 mix:referenceable提供了內置到儲存庫中的這樣一種機制，因此實際上不需要以穩定的方式提供其他標識節點的方法。

還要記住，項目可以通過路徑進行標識，而且對於大多數用戶來說，「符號連結」比unix檔案系統中的硬連結更有意義，因此，對於大多數應用程式來說，路徑是指目標節點的。

更重要的是 **混合**:referenceable，這意味著它可以應用到實際需要引用它的時間點。

因此，假設您希望能夠潛在地引用「文檔」類型的節點，並不意味著您的「文檔」節點類型必須從mix:referenceable以靜態方式擴展，因為它可以動態地添加到「文檔」的任何實例。

#### 範例 {#example-7}

使用:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

而不是：

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```
