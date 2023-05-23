---
title: 骨幹交互
seo-title: Backbone interaction
description: 有關在AEM Forms工作區中使用Backbone JavaScript模型的概念性資訊。
seo-description: Conceptual information about use of Backbone JavaScript models in AEM Forms workspace.
uuid: 040f42cb-3b76-4657-ba05-9e52647efb12
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 538591fe-29e4-40c4-a045-06095cc0c6b8
docset: aem65
exl-id: 8fd9770b-6ec4-4b09-b6b2-47a5e5d40f79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 骨幹交互{#backbone-interaction}

Backbone是一個庫，它幫助在Web應用程式中建立和遵循MVC體系結構。 Backbone的基本思想是將介面組織成由模型支援的邏輯視圖，每個視圖在模型更改時都可獨立更新，而無需重繪頁面。 有關Backbone的詳細資訊，請參見 [https://backbonejs.org](https://backbonejs.org/)。

主要概念如下：

**骨幹模型** 包含資料，以及與此資料相關的大部分邏輯。

**主幹視圖** 用於表示相應模型的狀態。 骨幹視圖實際上像控制器一樣工作，偵聽用戶點擊等用戶介面事件或建模事件（如資料更改），並根據需要修改用戶介面。

**HTML模板** 包裝模板，該模板具有由模型填充的佔位符。

**AEM Forms工作區** 包含幾個單獨的元件。 每個元件：

* 表示單個邏輯用戶介面元素。
* 可以是類似元件的集合。
* 由Backbone模型、Backbone視圖和HTML模板組成。
* 包含對服務的引用。
* 包含對所需實用程式的引用。

初始化元件時，將建立以下對象：

* 將為元件建立新的Backbone模型實例。 在模型中注入服務。
* 將建立Backbone視圖的新實例。
* 在視圖中注入相應模型、HTML模板和實用程式的實例。

在「主幹」視圖中，存在一個事件映射，該事件映射映射由於用戶介面與相應處理程式交互而可能產生的各種事件。 初始化元件後將啟動此映射。

初始化視圖時，視圖調用其相應的模型從伺服器獲取資料。 一旦視圖所需的所有資料都可用，視圖將以HTML模板指定的格式呈現資料。 多個視圖可以共用同一模型進行通信。

![](do-not-localize/aem_forms_workflow.png)

例如：

1. 用戶按一下任務清單中的任務模板。
1. 任務視圖偵聽按一下，並調用任務模型上的呈現函式。
1. 任務模型隨後調用服務，該服務是與AEM Forms伺服器進行所有通信的公共點。
1. Service類通過ajax調用呈現方法的AEM FormsREST終結點。
1. 此Ajax調用的成功回調是在任務模型中定義的。
1. 任務模型將骨幹事件作為呈現呼叫已完成的通知引發。
1. 另一個視圖，任務詳細資訊視圖從任務模型偵聽此事件。
1. 然後，任務詳細資訊視圖將更改任務詳細資訊模板，以向用戶顯示已呈現的任務（表單、詳細資訊、附件、附註等）。
