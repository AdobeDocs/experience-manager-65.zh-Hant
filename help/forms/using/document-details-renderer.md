---
title: 呈現器的文檔詳細資訊
seo-title: Document details for renderer
description: 關於如何在AEM Forms工作區中呈現工作以呈現各種受支援的表單和檔案類型的概念性資訊。
seo-description: Conceptual information on how renders work in AEM Forms workspace to render the various supported form and file types.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# 呈現器的文檔詳細資訊 {#document-details-for-renderer}

## 簡介 {#introduction}

在AEM Forms工作區中，可無縫支援多種表單類型。 這些類別包括：

* PDF forms(XDP / Acroform /平面PDF)
* 新HTML表
* 影像
* 第三方應用程式（例如，Tergement Management）

本文從語義定制/元件重用的角度解釋了這些投遞者的工作，這樣客戶的需求就可以得到滿足，而不會中斷任何格式副本。 儘管AEM Forms工作區允許任何用戶介面/語義更改，但建議不要更改不同表單類型的呈現邏輯，否則結果可能不可預知。 本文檔旨在提供指導/知識，以支援繪製相同的表單，使用不同入口中的相同工作區元件，而不是修改渲染邏輯本身。

## PDF forms {#pdf-forms}

PDF forms由 `PdfTaskForm View`。

當XDP表單呈現為PDF時， `FormBridge` JavaScript™由FormsAugmenter服務添加。 此JavaScript™(在PDF表單內)有助於執行表單提交、表單保存或表單離線等操作。

在AEM Forms工作區中，PDFTaskForm視圖與 `FormBridge`javascript，通過介質HTML `/lc/libs/ws/libs/ws/pdf.html`。 流是：

**PDFTaskForm視圖 — pdf.html**

使用 `window.postMessage` / `window.attachEvent('message')`

該方法是父幀和iframe之間的標準通信方式。 在添加新事件偵聽器之前，將刪除先前開啟的PDF forms中的現有事件偵聽器。 此清除還考慮在任務詳細資訊視圖中在表單頁籤和歷史記錄頁籤之間進行切換。

**pdf.html - `FormBridge`呈現的PDF中的javascript**

使用 `pdfObject.postMessage` / `pdfObject.messageHandler`

此方法是從HTML與PDFJavaScript進行通信的標準方法。 PdfTaskForm視圖還會處理平面PDF，並將其顯式呈現。

>[!NOTE]
>
>建議不要修改PdfTaskForm視圖的pdf.html /內容。

## 新HTMLForms {#new-html-forms}

新HTML表單由NewHTMLTaskForm視圖呈現。

當使用部署在CRX上的移動表單包將XDP表單呈現為HTML時，它還會添加其他 `FormBridge`JavaScript到表單，它公開了保存和提交表單資料的不同方法。

此JavaScript與上述PDF forms中提到的JavaScript不同，但其用途類似。

>[!NOTE]
>
>建議不要修改NewHTMLTaskForm視圖的內容。

## Flex·Forms和《嚮導》 {#flex-forms-and-guides}

Flex·Forms由SwfTaskForm呈現，輔助線分別由HtmlTaskForm視圖呈現。

在AEM Forms工作區中，這些視圖與實際SWF通信，該SWF使用當前存在的中介組成靈活表單/指南 `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

通信使用 `swfObject.postMessage` / `window.flexMessageHandler`。

此協定由 `WsNextAdapter.swf`。 現有 `flexMessageHandlers`在window對象上，在添加新SWF窗體之前，會先從先前開啟的窗體中刪除該窗體。 該邏輯還考慮在任務詳細資訊視圖中表單頁籤和歷史記錄頁籤之間的切換。 `WsNextAdapter.swf` 用於執行保存或提交等各種表單操作。

>[!NOTE]
>
>不建議修改 `WSNextAdapter.swf` 或SwfTaskForm / HtmlTaskForm視圖的內容。

## 第三方應用程式（例如，Tergement Management） {#third-party-applications-for-example-correspondence-management}

使用ExtAppTaskForm視圖呈現第三方應用程式。

**第三方應用於AEM Forms工作區通信**

AEM Forms工作區監聽 `window.global.postMessage([Message],[Payload])`

[消息] 可以是指定為的字串 `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`的 `runtimeMap`。 第三方應用程式必須使用此介面根據需要通知AEM Forms工作區。 使用此介面是必需的，因為AEM Forms工作區必須知道提交任務時可以清除任務窗口。

**AEM Forms工作區到第三方應用程式通信**

如果AEM Forms工作區的直接操作按鈕可見，它將調用 `window.[External-App-Name].getMessage([Action])`，也請參見Wiki頁。 `[Action]` 從 `routeActionMap`。 第三方應用程式必須偵聽此介面，然後通過 `postMessage ()` API。

例如，Flex應用程式可以 `ExternalInterface.addCallback('getMessage', listener)` 來支援此通信。 如果第三方應用程式希望通過其自己的按鈕處理表單提交，則應指定 `hideDirectActions = true() in the runtimeMap` 你可以跳過這個監聽器。 因此，此構造是可選的。

您可以在以下網站閱讀有關第三方應用程式整合的更多資訊： [整合AEM Forms工作區的函電管理](/help/forms/using/integrating-correspondence-management-html-workspace.md)。
