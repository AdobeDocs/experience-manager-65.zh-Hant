---
title: Markdown
description: 瞭解內容片段編輯器如何使用標籤語法來輕鬆建立無頭內容。
feature: Content Fragments
role: User
exl-id: e4340828-fe16-4edf-94c9-b0b145740e74
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 4%

---

# 馬爾克當 {#markdown}

當您 [創作](/help/assets/content-fragments/content-fragments-variations.md#authoring-your-content)，內容片段編輯器使用 *標籤* 語法，允許您輕鬆編寫無頭內容：

![標籤編輯器](/help/assets/content-fragments/assets/cfm-markdown-01.png)

您可以定義：

* [標題符號](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [段落和換行符](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [連結](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [影像](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [阻止引號](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [清單](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [強調](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [代碼塊](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [反斜線轉義](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## 標題符號 {#heading-notation}

通過在標題前面放置散列標籤(#)來建立標題。 一個散列標籤(#)用於H1，兩個散列標籤(##)用於H2等。 最多可使用6個哈希標籤。 例如：

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

或者，可以通過以等號對文本加下划線來建立H1，並通過以減號對文本加下划線來建立H2。 例如：

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落和換行符 {#paragraphs-and-line-breaks}

段落只是一行或多行文本，由一行或多行空白分隔。 空行是除空格或制表符之外不包含任何內容的行。 普通段落不應用空格或制表符縮進。

通過以兩個或兩個以上空格結尾的行，然後返回來建立換行符。

## 連結 {#links}

可以建立內聯連結和引用連結。

在這兩種樣式中，連結文本都由方括弧分隔 `[]`。

以下是內聯連結的示例：

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

引用連結具有以下語法：

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 影像 {#images}

影像的語法與連結類似。 可以建立內聯和引用的影像。

例如，內聯映像具有以下語法：

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

語法包括：

* 感嘆號：!;
* 後跟一組方括弧，其中包含影像的alt屬性文本；
* 後跟一組括弧，其中包含影像的URL或路徑，以及一個可選的標題屬性，用雙引號或單引號括起來。

引用樣式影像具有以下語法：

    `![Alt text][id]`

其中，「id」是已定義影像引用的名稱。 使用與連結引用相同的語法定義影像引用：

    `[id]: url/to/image "Optional title attribute"`

## 阻止引號 {#block-quotes}

可以通過在文本前添加>符號來引用文本。 例如：

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

可以有嵌套的塊引號。 例如：

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## 清單 {#lists}

您可以建立有序清單和未排序清單。

要建立未排序的清單，請使用&amp;ast;的子菜單。 例如：

    `* item in list`

    `* item in list`

    `* item in list`

要建立有序清單，請在清單中的每個項目前添加數字，然後添加句點。 例如：

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 強調 {#emphasis}

可以向文本添加斜體或粗體樣式。

要按如下方式添加斜體，請執行以下操作：

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

可以按如下方式加粗文本：

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

要指示代碼的跨度，請用反勾引號(&grave;)將其括起來。 與預格式化的代碼塊不同，代碼跨度表示普通段落中的代碼。

例如：

    ``Use the `printf()` function.``

## 代碼塊 {#code-blocks}

代碼塊通常用於說明原始碼。 可通過使用制表符或最少4個空格縮進代碼來建立代碼塊。 例如：

    `This is a normal paragraph.`

        `This is a code block.`

## 反斜線轉義 {#backslash-escapes}

可以使用反斜槓轉義生成文字字元，這些字元在格式語法中具有特殊含義。 例如，如果您想用文字星號(而不是HTML標籤)環繞單詞，可以在星號前使用反斜槓，如下所示：

    `\\*literal asterisks\\*`

反斜槓轉義可用於以下字元：

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
