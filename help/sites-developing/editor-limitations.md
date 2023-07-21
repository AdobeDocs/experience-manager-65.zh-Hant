---
title: 編輯器限制
description: 觸控式UI中的編輯器會使用覆蓋來與限制在iframe中的內容互動。 這個互動會對編輯器的使用以及開發人員造成一些限制。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 11%

---

# 編輯器限制{#editor-limitations}

觸控式UI中的編輯器會使用覆蓋來與限制在iframe中的內容互動。 這個互動會對編輯器的使用以及開發人員造成一些限制。本頁面會概述這些限制，並儘可能提供解決方案或因應措施。

## 功能限制 {#functional-limitations}

使用編輯器編寫頁面時，作者可能會遇到下列功能限制。

### 連結未啟用 {#links-not-active}

時間 [編輯頁面](/help/sites-authoring/editing-content.md)，連結未啟用。

* [切換至 **預覽** 模式](/help/sites-authoring/editing-content.md#preview-mode) 以使用內容中的連結進行導覽。

### 結構頁面 {#structure-pages}

頁面無法命名 `structure`. 已命名的頁面 `structure` 在頁面編輯器中不可編輯。

## CSS限制 {#css-limitations}

開發人員在編輯器與CSS的互動中可能會遇到下列限制。

### 絕對定位的元素 {#absolutely-positioned-elements}

絕對定位的元素可能會導致其覆蓋的位置出現問題。

* 如果發生此情況，請確定絕對定位元素的維度正確無誤，因為編輯器會使用完全相同的維度建立覆蓋。

### vh單位 {#vh-units}

`vh` 不支援單位，因為iframe高度必須由Adobe Experience Manager (AEM)自動調整。

### 固定背景影像 {#fixed-background-images}

固定背景影像可能無法在捲動時顯示為固定，因為它內嵌在iframe中。

* 選取 **以發佈的形式檢視頁面** 標題列動作可正確顯示頁面。

### 100%高度 {#height}

頁面的內文元素不支援100%高度。

* 解決方法是透過「拉伸」body元素來實作全熒幕主體，如下所示：

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 邊界收合 {#margin-collapsing}

如果body元素的第一個子元素有邊界，則會出現邊界收合問題。

* 解決方案是在主體元素層級新增clearfix，如下所示：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
