---
title: 骨幹互動
seo-title: 骨幹互動
description: 在AEM Forms工作區中使用Backbone javaScript模型的概念性資訊。
seo-description: 在AEM Forms工作區中使用Backbone javaScript模型的概念性資訊。
uuid: 040f42cb-3b76-4657-ba05-9e52647efb12
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 538591fe-29e4-40c4-a045-06095cc0c6b8
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 骨幹互動{#backbone-interaction}

Backbone是一個資料庫，可協助在Web應用程式中建立和遵循MVC架構。 Backbone的基本思想是將您的介面組織成邏輯檢視，並以模型為後盾，當模型變更時，每個模型都可獨立更新，而不需重繪頁面。 有關Backbone的更多資訊，請參 [閱https://backbonejs.org](https://backbonejs.org/)。

主要概念如下：

**骨幹模型** ：包含資料，且大部分邏輯與此資料相關。

**骨幹視圖** （用於表示相應模型的狀態）。 骨幹檢視的運作方式實際上就像控制器一樣，會監聽使用者點按等使用者介面事件，或模擬事件（如資料變更），並視需要修改使用者介面。

**HTML範本** ：包裝函式範本，其預留位置由模型填入。

**AEM Forms工作區** 「包含數個個別元件」。 每個元件：

* 表示單個邏輯用戶介面元素。
* 可以是類似元件的集合。
* 由「骨幹」模型、「骨幹」檢視和HTML範本組成。
* 包含服務的參考。
* 包含對所需實用程式的引用。

初始化元件時，將建立以下對象：

* 將建立元件的新Backbone模型實例。 模型中注入了服務。
* 建立「主幹」視圖的新實例。
* 在視圖中插入相應模型、HTML模板和實用程式的實例。

在主幹視圖中，有一個事件映射，它映射由於用戶介面與相應處理程式交互而可能出現的各種事件。 在初始化元件後，將啟動此映射。

當視圖初始化時，該視圖調用其相應的模型以從伺服器獲取資料。 檢視所需的所有資料一經可用，檢視就會以HTML範本指定的格式呈現資料。 多個視圖可以共用同一模型以進行通信。

![](do-not-localize/aem_forms_workflow.png)

例如：

1. 用戶按一下任務清單中的任務模板。
1. 任務視圖監聽按一下，並調用任務模型上的渲染函式。
1. 任務模型隨後呼叫服務，此服務是與AEM Forms伺服器進行所有通訊的常用點。
1. 服務類別會透過ajax呼叫AEM Forms REST端點，以呈現方法。
1. 此Ajax呼叫的成功回呼是在任務模型中定義的。
1. 任務模型會將骨幹事件作為轉換呼叫完成的通知。
1. 另一個視圖，任務詳細資訊視圖從任務模型監聽此事件。
1. 然後，「任務詳細資訊」視圖將更改任務詳細資訊模板，以向用戶顯示所呈現的任務（表單、詳細資訊、附件、附註等）。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
