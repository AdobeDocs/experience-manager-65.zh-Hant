---
title: 資料模型 — David Nuescheler模型
description: David Nuescheler的內容模型建議
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 6ce6a204-db59-4ed2-8383-00c6afba82b4
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# 資料模型 — David Nuescheler模型{#data-modeling-david-nuescheler-s-model}

## 來源 {#source}

以下是David Nuescheler所表達的構想和意見。

David是Day Software AG的聯合創始人和CTO，該公司是全球內容管理和內容基礎架構軟體的領先供應商，於2010年被Adobe收購。 David現在是Adobe的企業技術副總裁，同時也領導JSR-170的開發工作，這是Java™ Content Repository (JCR)應用程式設計介面(API)，這是內容管理的技術標準。

您也可以在以下網址檢視進一步更新： [https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel](https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel).

## 來自David的簡介 {#introduction-from-david}

在各種討論中，我發現開發人員在內容模型化時對JCR呈現的特性和功能有點不安。 目前尚無指南，也鮮有經驗說明如何為存放庫中的內容建立模型，以及為什麼一種內容模型優於另一種內容模型。

雖然在關聯式世界中，軟體產業在如何模型化資料方面擁有經驗，但內容存放庫空間的建立仍處於早期階段。

我想透過表達我對於內容應如何模型化的意見來開始填補這個空白。 我希望這有一天能成長為對開發人員社群更有意義的事物，不僅是「我的意見」，而是更普遍適用的事物。 所以試想一下這個我快速進化的第一個步驟。

>[!NOTE]
>
>免責宣告：這些准則表達了我個人的、有時有爭議的觀點。 我期待就這些准則進行辯論，並加以完善。

## 七個簡單規則 {#seven-simple-rules}

### 規則#1：資料優先，結構優先。 也許吧。 {#rule-data-first-structure-later-maybe}

#### 解釋 {#explanation-1}

我建議您不要擔心ERD意義上的宣告資料結構。 最初。

瞭解如何在開發中喜歡nt：unstructured (&amp; friends)。

我的底線：結構昂貴，通常完全不需要明確宣告結構給基礎儲存體。

您的應用程式本身會使用的結構有隱含的合約。 假設我把部落格的修改日期儲存在lastModified屬性中。 我的應用程式會自動知道要再次從相同屬性讀取修改日期，其實不需要明確宣告。

強制或型別和值限制之類的進一步資料限制應僅在資料完整性原因需要時套用。

#### 範例 {#example-1}

上述使用 `lastModified` 日期屬性（例如「部落格」節點）並不表示需要特殊的節點型別。 我一定會使用 `nt:unstructured` 至少剛開始是針對我的部落格節點。 由於在我的部落格應用程式中，我只要顯示lastModified日期即可（可能會「排序依據」），因此我一點也不在乎它是否為Date。 由於我隱含信任我的部落格撰寫應用程式，所以不需要宣告存在 `lastModified` 日期，採用節點型別的形式。

### 規則#2：驅動內容階層；不要讓它發生。 {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 解釋 {#explanation-2}

內容階層是寶貴的資產。 不要讓它發生；請設計它。 如果您沒有適合節點的「良好」、人類看得懂的名稱，建議您重新考慮。 任意數字很難算是「好名稱」。

雖然將現有的關聯式模型快速放入階層式模型可能很容易，但在此過程中應該多加思考。

根據我的經驗，如果有人認為存取控制和內含物是內容階層的良好驅動因素。 將其視為您的檔案系統。 甚至可能使用檔案和資料夾，在您的本機磁碟上進行模型化。

就我個人而言，我一開始偏好使用階層慣例，而不偏好節點輸入系統，之後會引入輸入功能。

>[!CAUTION]
>
>內容存放庫的結構方式也會影響效能。 為獲得最佳效能，附加至內容存放庫中個別節點的子節點數量不應超過1,000個。
>
>另請參閱 [CRX可以處理多少資料？](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html)

#### 範例 {#example-2}

我會建立一個簡單的部落格系統模型，如下所示。 起初，我甚至不在乎目前使用的個別節點型別。

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

我認為顯而易見的一點是，內容結構是根據範例理解的，沒有任何進一步的解釋。

一開始可能出乎意料的是，為什麼我不願意將「註解」與「貼文」一起儲存，這是因為我想以合理的分層式方式套用存取控制。

使用上述內容模型，我可以輕鬆允許「匿名」使用者「建立」評論，但工作區其餘部分仍將以唯讀方式保留匿名使用者。

### 規則#3：工作區用於clone()、merge()和update()。 {#rule-workspaces-are-for-clone-merge-and-update}

#### 解釋 {#explanation-3}

如果您不使用 `clone()`， `merge()` 或 `update()` 在您的應用程式中，單一工作區可能是可行的方式。

「對應節點」是JCR規格中定義的概念。 基本上，它會歸結為代表不同所謂工作區中相同內容的節點。

JCR引進了工作區的抽象概念，讓許多開發人員不知道如何處理這些工作區。 我建議您將工作區使用提交到以下專案進行測試。

如果在多個工作區中出現「對應」節點（基本上是具有相同UUID的節點）的大量重疊，您可能會善用工作區。

如果具有相同UUID的節點沒有重疊，則可能是濫用工作區。

請勿使用工作區進行存取控制。 特定使用者群組的內容可見度不是將專案分隔至不同工作區的好引數。 JCR在內容存放庫中提供「存取控制」功能，以供您使用。

工作區是參照和查詢的邊界。

#### 範例 {#example-3}

將工作區用於下列事項：

* 專案的v1.2與專案的v1.3
* 「開發」、「QA」和內容的「已發佈」狀態

請勿將工作區用於下列事項：

* 使用者主目錄
* 不同目標對象的不同內容，例如公用、私用、本機……
* 不同使用者的郵件收件匣

### 規則#4：注意同名的同層級。 {#rule-beware-of-same-name-siblings}

#### 解釋 {#explanation-4}

規格中引入了相同名稱同層級(SNS)，以便與專為XML設計並透過XML表示的資料結構相容，因此對JCR很有價值。 但是，SNS帶來了管理費用和存放庫的複雜性。

在其中一個路徑區段中包含SNS的內容存放庫的任何路徑都會變得不穩定許多。 如果SNS被移除或重新排序，則會影響其他所有SNS及其子項的路徑。

對於匯入XML或與現有XML的互動，SNS可能是必要且有用的，但我從未在我的「綠色欄位」資料模型中使用SNS （也從未打算使用）。

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

### 規則#5：參照被視為有害。 {#rule-references-considered-harmful}

#### 解釋 {#explanation-5}

參照表示參照完整性。 請務必瞭解，參考不僅會為存放庫管理參考完整性增加額外成本，但從內容彈性的角度來看，成本也很高昂。

就個人而言，我只有在我真的無法處理懸置參照時，才使用參照，否則請使用路徑、名稱或字串UUID來參照其他節點。

#### 範例 {#example-5}

假設我允許從檔案(a)到另一個檔案(b)的「參照」。 如果我使用參照屬性來模型化此關係，這表示這兩個檔案是在存放庫層級上連結的。 我無法個別匯出/匯入檔案(a)，因為參考屬性的目標可能不存在。 合併、更新、還原或原地複製等其他作業也會受到影響。

因此，我會將這些參考建模為「弱參考」（在JCR v1.0中，這基本上歸結為包含目標節點的uuid的字串屬性），或只是使用路徑。 有時候，路徑在開頭會更有意義。

我認為在使用案例中，當參考懸掛時，系統真的無法運作，但我無法從我的直接體驗中想出好的「真實」但簡單的範例。

### 規則#6：檔案是檔案。 {#rule-files-are-files}

#### 解釋 {#explanation-6}

如果內容模型揭露的東西甚至在遠端都聞起來像檔案或資料夾，我就會嘗試使用（或延伸） `nt:file`， `nt:folder`、和 `nt:resource`.

根據我的經驗，許多通用應用程式允許與nt：folder和nt：files進行隱含的互動，而且如果事件富含其他中繼資訊，它們也能知道如何處理和顯示這些事件。 例如，與JCR上方的檔案伺服器實作(如CIF或WebDAV)的直接互動會變成隱含。

我認為根據經驗法則，您可以使用以下內容：如果您必須儲存檔案名稱和mime型別，則 `nt:file`/ `nt:resource` 非常符合。 如果您可以有多個「檔案」，則nt：folder是儲存這些檔案的好地方。

如果您必須為資源新增中繼資訊，可以說「作者」或「說明」屬性，請擴展 `nt:resource` 不是 `nt:file`. 我很少擴充nt：file，而且經常擴充 `nt:resource`.

#### 範例 {#example-6}

假設某人想要將影像上傳至部落格專案，網址：

```xml
/content/myblog/posts/iphone_shipping
```

也許最初的內臟反應是加入包含圖片的二進位屬性。

雖然有些很好的使用案例只使用二進位屬性（比方說，名稱不相關且mime型別為隱含），但在此案例中，我建議為部落格範例使用下列結構。

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 規則#7：ID是邪惡的。 {#rule-ids-are-evil}

#### 解釋 {#explanation-7}

在關聯式資料庫中，ID是表示關係的必要方式，因此人們也傾向於在內容模型中使用它們。 多半是出於錯誤的原因。

如果內容模型中有許多以「Id」結尾的屬性，表示您可能未正確使用階層。

誠然，某些節點在其整個即時週期中都需要穩定的身分識別，實際數量可能比您想象的還少。 但是 `mix:referenceable` 存放庫中內建了此類機制，因此無需提供額外方法來以穩定方式識別節點。

也請記住，專案可透過路徑識別。 此外，由於「symlink」對於大多數使用者來說比UNIX®檔案系統中的硬連結更合理，因此對於大多數應用程式而言，路徑是指向目標節點也是合理的。

更重要的是 **mix**：referenceable，表示它可以在您實際必須參考節點的時間點套用至節點。

因此，僅僅因為您想要可能參考「檔案」型別的節點並不表示您的「檔案」節點型別必須從擴充 `mix:referenceable` 以靜態方式。 這是因為可將其動態新增至「檔案」的任何執行個體。

#### 範例 {#example-7}

使用：

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
