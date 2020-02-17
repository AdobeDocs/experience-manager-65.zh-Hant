---
title: Markdown
seo-title: Markdown
description: 當您製作內容時，內容片段編輯器會使用標籤語法，讓您輕鬆編寫內容。
seo-description: 當您製作內容時，內容片段編輯器會使用標籤語法，讓您輕鬆編寫內容。
uuid: afcbf82f-3a75-4491-9172-706188db65bb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: b193f28c-46c2-4eab-bbb8-578530f80ba5
docset: aem65
translation-type: tm+mt
source-git-commit: eb36f8fe6b08e03eb25e96ed1c31957f7d5aff27

---


# Markdown{#markdown}

當您製作內 [容時](content-fragments-variations.md#authoring-your-content)，內容片段編輯器會使 *用Markdown語法* ，讓您輕鬆編寫內容：

![標籤下編輯器](/help/assets/assets/cfm-6420-08.png)

您可以定義：

* [標題符號](/help/assets/content-fragments-markdown.md#heading-notation)
* [段落和分行](/help/assets/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [連結](/help/assets/content-fragments-markdown.md#links)
* [影像](/help/assets/content-fragments-markdown.md#images)
* [塊引號](/help/assets/content-fragments-markdown.md#block-quotes)
* [清單](/help/assets/content-fragments-markdown.md#lists)
* [強調](/help/assets/content-fragments-markdown.md#emphasis)
* [程式碼區塊](/help/assets/content-fragments-markdown.md#code-blocks)
* [反斜線轉義](/help/assets/content-fragments-markdown.md#backslash-escapes)

## 標題符號 {#heading-notation}

若要建立標題，請在標題前面放置雜湊標籤(#)。 一個雜湊標籤(#)用於H1，兩個雜湊標籤(##)用於H2等。 最多可使用6個雜湊標籤。 例如：

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

或者，您可以以等號加上文字底線來建立H1，並以減號加上文字底線來建立H2。 例如：

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落和分行 {#paragraphs-and-line-breaks}

段落只是一或多行連續的文字，由一或多行空白行分隔。 空行是僅包含空格或制表符的行。 一般段落不應縮進空格或制表符。

分行符號的建立方法是：用兩個或兩個以上的空格結束行，然後返回。

## 連結 {#links}

您可以建立內嵌連結和參考連結。

在這兩種樣式中，連結文字都以方括弧分隔 `[]`。

以下是內嵌連結的範例：

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

參考連結具有下列語法：

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 影像 {#images}

影像的語法類似於連結。 您可以建立內嵌和參考影像。

例如，內嵌影像具有下列語法：

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

語法包括：

* 驚嘆號：!;
* 後面接著一組方括弧，其中包含影像的alt屬性文字；
* 後面接著一組括弧，其中包含影像的URL或路徑，以及以雙引號或單引號括住的選用標題屬性。

參考樣式影像具有下列語法：

    `![Alt text][id]`

其中，&quot;id&quot;是已定義影像參考的名稱。 影像參照的定義語法與連結參照的語法相同：

    `[id]: url/to/image "Optional title attribute"`

## 塊引號 {#block-quotes}

您可以在文字前加上>符號來引用文字。 例如：

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

您可以有巢狀的區塊引號。 例如：

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## 清單 {#lists}

您可以建立有序清單和無序清單。

要建立無序清單，請使用&amp;ast;符號。 例如：

    `* item in list`

    `* item in list`

    `* item in list`

若要建立有序清單，請在清單中每個項目之前新增數字，後面接著句號。 例如：

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 強調 {#emphasis}

您可以在文字中加入斜體或粗體樣式。

要添加斜體，請執行以下操作：

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

您可以按如下方式使用粗體文字：

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

若要指出程式碼的範圍，請以反勾號(`)來包住程式碼。 與預先格式化的程式碼區塊不同，程式碼範圍表示一般段落中的程式碼。

例如：

    ``Use the `printf()` function.``

## 程式碼區塊 {#code-blocks}

程式碼區塊通常用來說明原始碼。 您可以使用索引標籤來縮進代碼或至少4個空格來建立代碼塊。 例如：

    `This is a normal paragraph.`

        `This is a code block.`

## 反斜線轉義 {#backslash-escapes}

您可以使用反斜線轉義來產生文字字元，這些字元在格式語法中有特殊意義。 例如，如果您想用常值星號（而非HTML &lt;em>標籤）包圍單字，則可在星號前使用反斜線，例如：

    `\\*literal asterisks\\*`

反斜線轉義可用於以下字元：

    `\ backslash`

    「回轉」

    `* asterisk`

    `_ underscore`

    `{} curly braces`

    `[] square brackets`

    `() parentheses`

    `# hash mark`

    `+ plus sign`

    `- minus sign (hyphen)`

    `. dot`
