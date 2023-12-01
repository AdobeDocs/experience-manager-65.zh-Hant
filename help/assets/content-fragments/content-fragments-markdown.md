---
title: Markdown
description: 瞭解內容片段編輯器如何使用Markdown語法，讓您輕鬆建立Headless內容。
feature: Content Fragments
role: User
exl-id: e4340828-fe16-4edf-94c9-b0b145740e74
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 4%

---

# Markdown {#markdown}

當您 [製作](/help/assets/content-fragments/content-fragments-variations.md#authoring-your-content)，內容片段編輯器會使用 *markdown* 語法讓您輕鬆撰寫Headless內容：

![Markdown編輯器](/help/assets/content-fragments/assets/cfm-markdown-01.png)

您可以定義：

* [標題標籤法](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [段落和分行符號](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [連結](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [影像](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [區塊引號](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [清單](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [強調](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [程式碼片段](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [反斜線逸出](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## 標題標籤法 {#heading-notation}

若要建立標題，請在標題前面放置雜湊標籤(#)。 一個雜湊標籤(#)用於H1，兩個雜湊標籤(##)用於H2，以此類推。 您最多可以使用6個雜湊標籤。 例如：

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

或者，您可以等號加底線來建立H1，減號加底線來建立H2。 例如：

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落和分行符號 {#paragraphs-and-line-breaks}

段落只是一行或多行連續的文字，以一行或多行空白行分隔。 空白行是隻包含空格或定位字元的行。 不應以空格或定位點縮排一般段落。

換行符號的建立方式，是先以兩個或多個空格結束一行，然後再返回一行。

## 連結 {#links}

您可以建立內嵌和參照連結。

在這兩種樣式中，連結文字會以方括弧分隔 `[]`.

以下是內嵌連結的範例：

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

參照連結的語法如下：

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 影像 {#images}

影像的語法與連結類似。 您可以建立內嵌和參照的影像。

例如，內嵌影像的語法如下：

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

語法包括：

* 驚歎號：！；
* 後面接著一組方括弧，其中包含影像的alt屬性文字；
* 後面接著一組括弧（包含影像的URL或路徑），以及一個以雙引號或單引號括起來的選用標題屬性。

參照樣式影像的語法如下：

    `![Alt text][id]`

其中「id」是定義的影像參考的名稱。 影像參照是使用與連結參照相同的語法來定義：

    `[id]: url/to/image "Optional title attribute"`

## 區塊引號 {#block-quotes}

您可以在文字前新增>符號來引用文字。 例如：

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

您可以有巢狀區塊引號。 例如：

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## 清單 {#lists}

您可以建立已排序和未排序清單。

若要建立未排序清單，請使用清單中專案前的&amp;ast；符號。 例如：

    `* item in list`

    `* item in list`

    `* item in list`

若要建立有序清單，請在清單中的每個專案前新增數字，然後加上句點。 例如：

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 強調 {#emphasis}

您可以新增斜體或粗體樣式至文字。

若要新增斜體，如下所示：

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

您可以依照下列方式顯示粗體文字：

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

若要指出程式碼跨度，請用反勾號(&amp;grave；)括住程式碼。 和預先格式化的程式碼區塊不同，程式碼範圍表示一般段落中的程式碼。

例如：

    ``Use the `printf()` function.``

## 程式碼片段 {#code-blocks}

程式碼區塊通常用於說明原始程式碼。 您可以使用索引標籤縮排程式碼，或最少4個空格來建立程式碼區塊。 例如：

    `This is a normal paragraph.`

        `This is a code block.`

## 反斜線逸出 {#backslash-escapes}

您可以使用反斜線逸出產生在格式語法中具有特殊意義的常值字元。 例如，如果您想在文字周圍加上星號(而非HTML標籤)，則可以在星號前使用反斜線，如下所示：

    `\\*literal asterisks\\*`

反斜線逸出適用於下列字元：

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
