---
title: 轉譯器的檔案詳細資訊
seo-title: 轉譯器的檔案詳細資訊
description: 關於如何在AEM Forms工作區中轉譯以轉譯各種支援的表單和檔案類型的概念資訊。
seo-description: 關於如何在AEM Forms工作區中轉譯以轉譯各種支援的表單和檔案類型的概念資訊。
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# 渲染器{#document-details-for-renderer}的文檔詳細資訊

## 簡介 {#introduction}

在AEM Forms工作區中，可順暢地支援多種表單類型。 這些包括：

* PDF forms（XDP / Acroform /一般PDF）
* 新HTML表單
* 影像
* 第三方應用程式（例如通信管理）

本檔案從語義自訂/元件重複使用的角度，說明這些轉譯者的工作方式，以便在不破壞任何轉譯的情況下滿足客戶需求。 雖然AEM Forms工作區允許任何使用者介面/語意變更，但建議不要變更不同表單類型的轉譯邏輯，否則結果可能無法預測。 本檔案旨在提供指引/知識，以支援轉譯相同的表單、在不同入口中使用相同的工作區元件，而非修改轉譯邏輯本身。

## PDF forms{#pdf-forms}

PDF forms由`PdfTaskForm View`呈現。

將XDP表單轉譯為PDF時，FormsAugmenter服務會新增`FormBridge` JavaScript™。 此JavaScript™（在PDF表單內）有助於執行表單提交、表單儲存或離線表單等動作。

在AEM Forms工作區中，PDFTaskForm檢視會透過`/lc/libs/ws/libs/ws/pdf.html`處的中介HTML與`FormBridge`javascript通訊。 流量為：

**PDFTaskForm檢視 — pdf.html**

使用`window.postMessage` / `window.attachEvent('message')`進行通訊

此方法是上層框架與iframe之間通訊的標準方式。 新增事件監聽器之前，會先移除先前開啟之PDF forms中的現有事件監聽器。 此清除還考慮在任務詳細資訊視圖中的表單頁簽和歷史記錄頁簽之間進行切換。

**pdf.html — 轉 `FormBridge`譯的PDF內的javascript**

使用`pdfObject.postMessage` / `pdfObject.messageHandler`進行通訊

此方法是從HTML與PDFJavaScript通訊的標準方式。 PdfTaskForm檢視也能處理平面PDF，並直接呈現。

>[!NOTE]
>
>不建議修改PdfTaskForm視圖的pdf.html /內容。

## 新HTML Forms {#new-html-forms}

新的HTML表單會由NewHTMLTaskForm檢視呈現。

使用部署在CRX上的行動表單套件將XDP表單轉譯為HTML時，它也會將額外的`FormBridge`JavaScript新增至表單，這會顯示儲存和提交表單資料的不同方法。

此JavaScript與上述PDF forms中所述的不同，但有類似的用途。

>[!NOTE]
>
>不建議修改NewHTMLTaskForm檢視的內容。

## Flex Forms與指南{#flex-forms-and-guides}

Flex Forms由SwfTaskForm呈現，而參考線由HtmlTaskForm檢視分別呈現。

在AEM Forms工作區中，這些檢視會與實際SWF通訊，實際SWF會使用`/lc/libs/ws/libs/ws/WSNextAdapter.swf`處的中介SWF組成Flex表單/指南

通訊會使用`swfObject.postMessage` / `window.flexMessageHandler`進行。

此協定由`WsNextAdapter.swf`定義。 在添加新表單之前，會刪除先前開啟的SWF表單中窗口對象上的現有`flexMessageHandlers`。 此邏輯也會考慮在任務詳細資訊檢視中的表單標籤和歷史記錄標籤之間進行切換。 `WsNextAdapter.swf` 用於執行儲存或提交等各種表單動作。

>[!NOTE]
>
>不建議修改`WSNextAdapter.swf`或SwfTaskForm / HtmlTaskForm視圖的內容。

## 第三方應用程式（例如通信管理）{#third-party-applications-for-example-correspondence-management}

使用ExtAppTaskForm視圖呈現第三方應用程式。

**協力廠商應用程式與AEM Forms工作區通訊**

AEM Forms workspace監聽`window.global.postMessage([Message],[Payload])`

[] Messagecan是指定為  `SubmitMessage`|  `CancelMessage`|  `ErrorMessage`| `actionEnabledMessage`中 `runtimeMap`。協力廠商應用程式必須使用此介面，才能視需要通知AEM Forms工作區。 必須使用此介面，因為AEM Forms工作區必須知道提交任務時，以便清除任務窗口。

**AEM Forms工作區與協力廠商應用程式通訊**

如果AEM Forms工作區的直接動作按鈕可見，則會呼叫`window.[External-App-Name].getMessage([Action])`，其中從`routeActionMap`讀取`[Action]`。 協力廠商應用程式必須監聽此介面，然後透過`postMessage ()` API通知AEM Forms工作區。

例如，Flex應用程式可定義`ExternalInterface.addCallback('getMessage', listener)`以支援此通訊。 如果第三方應用程式希望通過其自己的按鈕處理表單提交，則應指定`hideDirectActions = true() in the runtimeMap`，並可跳過此監聽程式。 因此，此結構為選用。

您可以前往[整合AEM Forms工作區中的通信管理](/help/forms/using/integrating-correspondence-management-html-workspace.md)，深入了解與通信管理相關的第三方應用程式整合。
