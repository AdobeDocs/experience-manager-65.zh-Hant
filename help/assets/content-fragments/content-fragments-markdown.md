---
title: Markdown
seo-title: Markdown
description: 您編寫內容時，內容片段編輯器會使用Markdown語法，讓您輕鬆撰寫內容。
seo-description: 您編寫內容時，內容片段編輯器會使用Markdown語法，讓您輕鬆撰寫內容。
uuid: afcbf82f-3a75-4491-9172-706188db65bb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: b193f28c-46c2-4eab-bbb8-578530f80ba5
docset: aem65
feature: 內容片段
role: User, Admin
exl-id: 28e1052f-62b5-47bc-9bc8-f2d92f0254f6
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 4%

---

# Markdown{#markdown}

當您是[authoring](content-fragments-variations.md#authoring-your-content)時，內容片段編輯器會使用&#x200B;*markdown*&#x200B;語法，讓您輕鬆撰寫內容：

![markdown編輯器](/help/assets/content-fragments/assets/cfm-6420-08.png)

您可以定義：

* [標題標籤法](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [段落和分行](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [連結](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [影像](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [塊引號](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [清單](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [強調](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [程式碼區塊](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [反斜線逸出](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## 標題標籤法 {#heading-notation}

若要建立標題，請將雜湊標籤(#)放在標題前面。 一個雜湊標籤(#)用於H1，兩個雜湊標籤(##)用於H2等。 您最多可以使用6個雜湊標籤。 例如：

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

或者，您可以通過以等號加下划線來建立H1，並通過以減號加下划線來建立H2。 例如：

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落和分行 {#paragraphs-and-line-breaks}

段落只是一行或多行連續文本，用一行或多行空白行分隔。 空白行是不含空格或制表符的行。 普通段落不應縮進空格或制表符。

分行符號的建立方式是先將包含兩個或更多空格的行結尾再返回。

## 連結 {#links}

您可以建立內嵌連結和參考連結。

在這兩種樣式中，連結文字會以方括弧`[]`分隔。

以下是內嵌連結的範例：

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

參考連結的語法如下：

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 影像 {#images}

影像的語法類似於連結。 您可以建立內嵌和參考的影像。

例如，內嵌影像的語法如下：

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

語法包括：

* 感嘆號：!;
* 後面接著一組方括弧，包含影像的alt屬性文本；
* 後面接著一組括弧，包含影像的URL或路徑，以及以雙引號或單引號括住的選用標題屬性。

參照樣式影像具有下列語法：

    `![Alt text][id]`

其中，「id」是定義的影像參考的名稱。 影像參考是使用與連結參考相同的語法來定義：

    `[id]: url/to/image "Optional title attribute"`

## 塊引號 {#block-quotes}

您可以在文字前面新增>符號，以引用文字。 例如：

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

您可以建立已排序和未排序的清單。

若要建立無序清單，請使用&amp;ast;符號。 例如：

    `* item in list`

    `* item in list`

    `* item in list`

若要建立已排序的清單，請在清單中的每個項目前面新增數字，後面加上句號。 例如：

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 強調 {#emphasis}

您可以將斜體或粗體樣式新增至文字。

若要新增斜體，如下所示：

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

您可以依照下列方式使用粗體文字：

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

若要指出程式碼的範圍，請以反勾號括住(&amp;grave;)。 與預格式化的代碼塊不同，代碼範圍指示正常段落中的代碼。

例如：

    ``Use the `printf()` function.``

## 程式碼區塊 {#code-blocks}

代碼塊通常用於說明原始碼。 您可以使用索引標籤縮進程式碼，或至少縮進4個空格，以建立程式碼區塊。 例如：

    `This is a normal paragraph.`

        `This is a code block.`

## 反斜線逸出 {#backslash-escapes}

您可以使用反斜線逸出來產生文字字元，這些字元在格式語法中有特殊意義。 例如，如果您想要以常值星號括住單字（而非HTML &lt;em>標籤），您可以在星號前使用反斜線，例如：

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
