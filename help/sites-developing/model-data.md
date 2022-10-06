---
title: 資料模型 — 大衛·紐謝勒的模型
seo-title: Data Modeling - David Nuescheler's Model
description: David Nuescheler的內容模型建議
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

# 資料模型 — 大衛·紐謝勒的模型{#data-modeling-david-nuescheler-s-model}

## 來源 {#source}

以下是David Nuescheler所表達的想法和評論。

Day Software AG是全球內容管理和內容基礎架構軟體的領先提供商，Day Software AG於2010年被Adobe收購。 他現在是Adobe企業技術部的資深副總裁，也領導了JSR-170，即Java Content Repository(JCR)應用程式寫程式介面(API)，即內容管理技術標準的開發。

您也可以在 [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## David簡介 {#introduction-from-david}

在各種討論中，我發現開發人員對JCR在內容建模方面所呈現的特性和功能有些不安。 關於如何在存放庫中建立內容模型，以及為何一個內容模型優於另一個內容模型，目前尚無相關指南和極少的體驗。

在關係世界中，軟體行業在如何對資料進行建模方面有著豐富的經驗，但是，對於內容儲存庫空間，我們還處於早期階段。

我希望通過表達我對如何建立內容模型的個人觀點來填補這一空白，希望有一天這能夠成為對開發人員群體更有意義的東西，這不僅僅是「我的意見」，而是更普遍的適用。 所以，考慮一下這是我快速演變的第一次嘗試。

>[!NOTE]
>
>免責聲明：這些准則表達了我的個人觀點，有時也帶有爭議。 我期待就這些准則展開辯論並加以完善。

## 七條簡單規則 {#seven-simple-rules}

### 規則#1:資料先，結構後。 也許吧。 {#rule-data-first-structure-later-maybe}

#### 說明 {#explanation-1}

我建議不要擔心ERD意義上的宣告資料結構。 一開始。

學習在開發中喜歡nt：非結構化（和朋友）。

我想斯蒂法諾差不多是這個。

我的底線是：結構很昂貴，在許多情況下完全不需要向基礎儲存顯式聲明結構。

您的應用程式固有使用的結構有隱含的契約。 假設我將部落格貼文的修改日期儲存在lastModified屬性中。 我的應用程式會自動知道要再次從相同屬性讀取修改日期，因此不需要明確宣告。

基於資料完整性原因，應僅在需要時套用其他資料限制，例如強制或類型和值限制。

#### 範例 {#example-1}

上述使用 `lastModified` 「部落格貼文」節點上的日期屬性，其實並不表示需要特殊的nodetype。 我肯定會用 `nt:unstructured` 至少最初是這樣。 因為在我的部落格應用程式中，我要做的就是顯示最後一個修改的日期（可能是「訂購」日期），我根本不在乎它是否是日期。 由於我暗中信任我的部落格撰寫應用程式，因此，實際上不需要宣佈存在 `lastModified` 以nodetype的a形式顯示日期。

### 規則#2:驅動內容階層，別讓它發生。 {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 說明 {#explanation-2}

內容階層是非常有價值的資產。 所以別讓它發生，設計它。 如果一個節點沒有「好」、人類看得懂的名稱，那麼你可能應該重新考慮。 武斷的數字從來就不是「好名字」。

雖然將現有的關係模型快速地放入分層模型可能非常容易，但應該在這個過程中考慮一些問題。

在我的經驗中，如果想到訪問控制和控制通常是內容層次結構的良好驅動因素。 把它想成是你的檔案系統。 甚至可以使用檔案和資料夾在本地磁碟上進行建模。

就個人而言，在很多情況下，我最初更喜歡等級制度慣例，而不是匿名輸入系統，然後在以後介紹這種類型。

>[!CAUTION]
>
>內容存放庫的結構方式也會影響效能。 為獲得最佳效能，內容儲存庫中連接到單個節點的子節點數通常不應超過1&#39;000。
>
>請參閱 [CRX可以處理多少資料？](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) 以取得更多資訊。

#### 範例 {#example-2}

我將建立一個簡單的部落格系統，如下所示。 請注意，一開始我甚至不關心目前使用的個別節點類型。

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

我認為一件顯而易見的事情是我們都理解了內容的結構基於這個例子而沒有任何進一步的解釋。

最初可能出人意料的是，為什麼我不會將「留言」與「貼文」一起儲存，這是因為我希望以合理的分層方式應用訪問控制。

使用上述內容模型，我可以輕鬆允許「匿名」使用者「建立」註解，但讓匿名使用者在工作區的其餘部分以唯讀方式保留。

### 規則#3:工作區適用於clone()、merge()和update()。 {#rule-workspaces-are-for-clone-merge-and-update}

#### 說明 {#explanation-3}

如果您不使用 `clone()`, `merge()` 或 `update()` 在您的應用程式中，使用單一工作區的方法可能是最理想的作法。

「對應節點」是JCR規範中定義的概念。 基本上，歸結為在不同所謂工作區中代表相同內容的節點。

JCR引入了Workspaces非常抽象的概念，這讓許多開發人員不清楚該如何使用它們。 我想建議將您對工作區的使用進行以下測試。

如果您在多個工作區中有相當大的「對應」節點重疊（本質上是具有相同UUID的節點），則您可能會將工作區放置到好處。

如果節點與相同UUID沒有重疊，則您可能會濫用工作區。

工作區不應用於存取控制。 特定使用者群組的內容可見性不是將項目分隔至不同工作區的好引數。 JCR在內容存放庫中提供「存取控制」功能，以提供此功能。

工作區是參照和查詢的邊界。

#### 範例 {#example-3}

將工作區用於下列項目：

* 專案的v1.2與專案的v1.3
* 「開發」、「QA」和「已發佈」的內容狀態

請勿將工作區用於下列項目：

* 用戶首目錄
* 不同目標對象的不同內容，例如公開、私人、本機、..
* 不同使用者的郵件收件匣

### 規則#4:請注意同名兄弟姐妹。 {#rule-beware-of-same-name-siblings}

#### 說明 {#explanation-4}

雖然在規範中引入了同名同級(SNS)，允許與專為XML設計並通過XML表示的資料結構相容，因此對JCR極有價值，但SNS對儲存庫帶來了巨大的開銷和複雜性。

進入其路徑段中包含SNS的內容儲存庫的任何路徑都會變得不穩定，如果刪除或重新排序SNS，則會影響其他所有SNS及其子項的路徑。

對於導入XML或與現有XML SNS進行交互，可能是必要和有用的，但我從未使用過SNS，而且從未在「綠色欄位」資料模型中使用過。

#### 範例 {#example-4}

使用

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

而非

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### 規則#5:被認為有害的參考。 {#rule-references-considered-harmful}

#### 說明 {#explanation-5}

引用意味著參照完整性。 我發現，重要的一點是要了解，參考不僅會為管理參考完整性的儲存庫增加額外成本，而且從內容靈活性的角度來看，這些參考也會帶來很大成本。

就個人而言，我確定只有在我真的無法處理懸掛參照時才使用參照，否則請使用路徑、名稱或字串UUID來參照其他節點。

#### 範例 {#example-5}

假設我允許將檔案(a)的「參考」引用到另一個檔案(b)。 如果我使用引用屬性來建模此關係，這表示兩個文檔在儲存庫級別上連結。 無法單獨導出/導入文檔(a)，因為引用屬性的目標可能不存在。 其他操作（如合併、更新、還原或克隆）也會受到影響。

因此，我要麼將這些參照建模為「弱參照」（在JCR v1.0中，這基本上可歸結為包含目標節點uuid的字串屬性），要麼只使用路徑。 有時從開始，路徑更有意義。

我認為，在一些使用案例中，一個系統如果一個引用被晃來晃去，就真的無法運作，但是，我無法從我的直接經驗中得出一個好的、「真實」但簡單的例子。

### 規則#6:檔案是檔案。 {#rule-files-are-files}

#### 說明 {#explanation-6}

如果內容模型公開的內容甚至遠程 *氣味* 就像我嘗試使用的檔案或資料夾（或從延伸） `nt:file`, `nt:folder` 和 `nt:resource`.

在我的經驗中，許多通用應用程式允許以隱式方式與nt:folder和nt:files交互，並且知道如果這些事件富含其他元資訊，如何處理和顯示這些事件。 例如，與檔案伺服器實施（如CIFS或WebDAV）的直接交互（位於JCR之上）變為隱式。

我認為，作為經驗法則，人們可以使用以下方法：如果您需要儲存檔案名稱和mime類型，則 `nt:file`/ `nt:resource` 是場很棒的比賽。 如果您可以有多個「檔案」，則nt:folder是儲存這些檔案的好地方。

如果您需要為資源新增中繼資訊，例如「作者」或「說明」屬性，請擴充 `nt:resource` 不是 `nt:file`. 我很少擴展nt:file，並經常擴展 `nt:resource`.

#### 範例 {#example-6}

假設有人想要將影像上傳至部落格項目：

```xml
/content/myblog/posts/iphone_shipping
```

也許最初的直覺反應是添加包含圖片的二進位屬性。

雖然有很好的使用案例只使用二進位屬性（假設名稱無關且mime類型隱含），但在此情況下，我會為部落格範例建議下列結構。

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 規則#7:身份是邪惡的。 {#rule-ids-are-evil}

#### 說明 {#explanation-7}

在關係資料庫中，ID是表達關係的必要手段，因此人們往往也會在內容模型中使用它們。 主要是因為錯誤的原因。

如果您的內容模型充滿以「Id」結尾的屬性，您可能未正確運用階層。

確實，某些節點在其整個生命週期中都需要穩定的識別。 但比你想的要少得多。 mix:referenceable提供內建在存放庫中的這類機制，因此確實不需要另外提供以穩定方式識別節點的方法。

還要記住，項目可以通過路徑來識別，而「symlinks」對於大多數用戶來說比在unix檔案系統中的硬連結更有意義，因此，路徑對於大多數應用程式來說都是可以引用目標節點的。

更重要的是， **混合**:referenceable，這表示當您實際需要參考節點時，可將其套用至節點。

因此，假設您想要能夠參考「Document」類型的節點，並不表示您的「Document」節點類型必須以靜態方式從mix:referenceable延伸，因為它可以動態地新增至「Document」的任何例項。

#### 範例 {#example-7}

使用:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

而非：

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
