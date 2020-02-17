---
title: 資料建模- David Nuescheler的模型
seo-title: 資料建模- David Nuescheler的模型
description: David Nuescheler的內容模型建議
seo-description: David Nuescheler的內容模型建議
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 資料建模- David Nuescheler的模型{#data-modeling-david-nuescheler-s-model}

## 來源 {#source}

以下是David Nuescheler所表達的想法和評論。

David是Day Software AG的共同創辦人暨技術長，Day Software AG是全球內容管理和內容基礎架構軟體的領先供應商，Adobe於2010年收購此軟體。 他目前是Adobe企業技術部門的資深副總裁，也負責JSR-170(Java Content Repository(JCR)應用程式設計介面(API)，內容管理的技術標準)的開發。

如需更新資訊，請造訪https://wiki.apache.org/jackrabbit/DavidsModel [](https://wiki.apache.org/jackrabbit/DavidsModel)。

## David簡介 {#introduction-from-david}

在各種討論中，我發現開發人員對JCR在內容建模方面所呈現的特性和功能有些不安。 關於如何在儲存庫中建立內容模型，以及為什麼一個內容模型比另一個模型更好，目前還沒有指南和很少的經驗。

雖然在關係世界中，軟體產業在如何建立資料模型方面有許多經驗，但內容存放庫空間尚處於早期階段。

我想開始填補這個空白，就內容的模型化表達我個人的意見，希望有朝一日，它可以成為對開發人員社群更有意義的東西，這不僅是「我的意見」，而是更普遍適用的內容。 因此，請考慮這個，我快速演變的第一次嘗試。

>[!NOTE]
>
>免責聲明：這些准則表達了我的個人觀點，有時也引起了爭議。 我期待著就這些准則進行辯論並加以完善。

## 7個簡單規則 {#seven-simple-rules}

### 規則#1:資料先，結構後。 也許吧。 {#rule-data-first-structure-later-maybe}

#### 說明 {#explanation-1}

我建議您不要擔心在ERD意義上宣佈的資料結構。 最初。

瞭解在開發中喜歡nt:sutranculed（和朋友）。

我覺得斯特法諾差不多是這個意思。

我的底線是：結構昂貴，在很多情況下完全不需要向底層儲存明確聲明結構。

您的應用程式本身就使用結構，這裡有一個隱含的合約。 假設我將部落格貼文的修改日期儲存在lastModified屬性中。 我的應用程式會自動知道再次從同一個屬性讀取修改日期，因此不需要明確宣告。

基於資料完整性原因，應僅在需要時應用強制或類型和值約束等進一步資料約束。

#### 例如 {#example-1}

上述在例如「部落格貼文」節點上使用 `lastModified` Date屬性的範例，並不表示需要特殊nodetype。 至少一開始，我 `nt:unstructured` 一定會用於我的部落格貼文節點。 因為在我的部落格應用程式中，我只要顯示最後一個修改日期（可能是「依順序」），我幾乎不在乎它是否為日期。 由於我隱含地相信我的部落格撰寫應用程式會將「日期」放在那裡，因此，我不需要以nodetype的形式宣 `lastModified` 告日期的存在。

### 規則#2:推動內容階層，別讓它發生。 {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### 說明 {#explanation-2}

內容階層是非常有價值的資產。 所以，別讓它發生，去設計它。 如果您沒有一個「好」、人類可讀的節點名稱，那麼，您可能應該重新考慮這個問題。 武斷的數字從來都不是「好名字」。

雖然將現有的關係模型快速放入階層式模型非常容易，但在這個過程中，我們應該思考一下。

根據我的經驗，如果人們想到存取控制和限制通常是內容階層的好驅動因素。 將它想成是您的檔案系統。 甚至可以使用檔案和檔案夾，在本機磁碟上建立模型。

我個人認為，在很多情況下，我更喜歡等級慣例，而不是輸入系統，然後在以後引入輸入。

>[!CAUTION]
>
>內容儲存庫的結構方式也會影響效能。 為獲得最佳效能，內容儲存庫中連接到單個節點的子節點數通常不應超過1&#39;000。
>
>瞭解 [CRX可處理多少資料？](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) 的上界。

#### 例如 {#example-2}

我會給一個簡單的部落格系統建模如下。 請注意，一開始我甚至不關心我目前使用的個別節點類型。

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

我認為一個顯而易見的事實是我們都理解內容的結構基於範例而沒有任何進一步的解釋

一開始可能意想不到的是，我不會將「留言」儲存在「貼文」中，這是因為存取控制，我想以合理的階層方式套用。

使用上述內容模型，我可輕鬆允許「匿名」使用者「建立」註解，但是讓匿名使用者在工作區的其餘部分保持唯讀狀態。

### 規則#3:工作區是用於clone()、merge()和update()。 {#rule-workspaces-are-for-clone-merge-and-update}

#### 說明 {#explanation-3}

如果您未在應用程 `clone()`式中 `merge()` 使用 `update()` 或方法，則可能需要單一工作區。

「對應節點」是JCR規範中定義的概念。 基本上，這可歸結為在不同的所謂工作區中代表相同內容的節點。

JCR引入了非常抽象的Workspaces概念，這使得許多開發人員不清楚如何使用Workspaces。 我建議將您對工作區的使用置於以下位置進行測試。

如果多個工作區中「對應」節點（實際上是具有相同UUID的節點）有相當大的重疊，則您可能會將工作區放在好處。

如果使用相同UUID的節點沒有重疊，則您可能濫用工作區。

工作區不應用於存取控制。 對於特定使用者群組而言，可見性並不是將內容分離到不同工作區的好理由。 JCR在內容儲存庫中提供「存取控制」功能。

工作區是參照和查詢的邊界。

#### 例如 {#example-3}

使用工作區進行下列工作：

* 您專案的v1.2與專案v1.3
* 「開發」、「QA」和「已發佈」的內容狀態

請勿將工作區用於下列項目：

* 用戶主目錄
* 針對不同目標對象(例如公開、私用、本機、...
* 不同使用者的郵箱

### 規則#4:小心同名兄弟姐妹。 {#rule-beware-of-same-name-siblings}

#### 說明 {#explanation-4}

雖然在規範中引入了同名同級(SNS)，以允許與為XML設計並通過JCR表示的資料結構相容，因此對JCR非常有價值，但SNS對儲存庫來說具有巨大的開銷和複雜性。

進入內容儲存庫的任何路徑在其路徑段中包含SNS都變得不那麼穩定，如果SNS被刪除或重新排序，則會對所有其他SNS及其子代的路徑產生影響。

要導入XML或與現有XML SNS進行交互，可能既必要又有用，但我從未使用過SNS，也從未在「綠色域」資料模型中使用過。

#### 例如 {#example-4}

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

### 規則#5:參照被認為有害。 {#rule-references-considered-harmful}

#### 說明 {#explanation-5}

參照暗示參照完整性。 我發現，必須瞭解的是，引用不僅會為管理引用完整性的儲存庫增加額外成本，而且從內容靈活性的角度來說，它們也會帶來高昂的成本。

我個人會確保我只在無法處理懸掛參照時使用參照，否則請使用路徑、名稱或字串UUID來參照其他節點。

#### 例如 {#example-5}

假設我允許從檔案(a)到另一檔案(b)的「參照」。 如果我使用引用屬性對此關係建模，這表示兩個文檔在儲存庫級別上連結。 我無法個別匯出／匯入檔案(a)，因為參考屬性的目標可能不存在。 其他操作（如合併、更新、恢復或克隆）也會受到影響。

因此，我要麼將這些參照建模為「弱參照」（在JCR v1.0中，這基本上可歸結為包含目標節點uuid的字串屬性），要麼只使用路徑。 有時，路徑的開頭更有意義。

我認為，有些使用案例中，如果某個參考物懸垂，系統真的無法運作，但我無法從我的直接體驗中得出一個好的「真實」但簡單的例子。

### 規則#6:檔案是檔案。 {#rule-files-are-files}

#### 說明 {#explanation-6}

如果內容模型暴露出某些氣味 ** ，甚至像我嘗試使用（或從中延伸）的檔案或資料夾 `nt:file`, `nt:folder` 以及 `nt:resource`。

在我的經驗中，許多通用應用程式都允許與nt:folder和nt:files進行互動，並且知道如何處理和顯示這些事件（如果這些事件包含了額外的中繼資訊）。 例如，與位於JCR之上的CIFS或WebDAV等檔案伺服器實施的直接交互變為隱式。

我認為，作為一個好的經驗法則，人們可以用下列方法：如果您需要儲存檔案名稱和mime類型，則 `nt:file`/ `nt:resource` 非常符合。 如果您可以有多個「檔案」，則nt:folder是儲存檔案的好地方。

如果您需要為資源新增中繼資訊，例如「作者」或「描述」屬性，請延伸而 `nt:resource` 非 `nt:file`。 我很少延伸nt:file，而且經常延伸 `nt:resource`。

#### 例如 {#example-6}

假設有人想要將影像上傳至部落格項目，網址為：

```xml
/content/myblog/posts/iphone_shipping
```

也許最初的腸胃反應是添加包含圖片的二進位屬性。

雖然在此案例中，確實有使用二進位屬性的好用案例（假設名稱不相關，而mime類型是隱式的），但我建議使用下列部落格範例結構。

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### 規則#7:身份證是邪惡的。 {#rule-ids-are-evil}

#### 說明 {#explanation-7}

在關係式資料庫中，ID是表達關係的必要方式，因此人們也傾向於在內容模型中使用ID。 主要是因為錯誤的原因。

如果您的內容模型包含結尾為&quot;Id&quot;的屬性，您可能無法正確運用階層。

確實，某些節點在其整個生命週期中都需要穩定的標識。 但比你想像的要少很多。 mix:referenceable提供了內置在儲存庫中的這種機制，因此，確實不需要另外提供以穩定方式標識節點的方法。

請記住，項目可以通過路徑進行標識，而且「symlinks」對大多數用戶來說比UNIX檔案系統中的硬連結更有意義，因此，路徑對大多數應用程式來說都是指目標節點。

更重要的是，它是 **mix**:referencable，這表示它可在您實際需要參考時套用至節點。

因此，假設您想要能夠參考「檔案」類型的節點，並不表示您的「檔案」節點類型必須從mix:reference以靜態方式延伸，因為它可以動態地新增至「檔案」的任何例項。

#### 例如 {#example-7}

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

