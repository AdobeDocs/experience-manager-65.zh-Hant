---
title: 轉譯器的檔案詳細資訊
description: 有關轉譯器如何在AEM Forms工作區中運作，以轉譯各種支援的表單和檔案型別的概念資訊。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# 轉譯器的檔案詳細資訊 {#document-details-for-renderer}

## 簡介 {#introduction}

在AEM Forms工作區中，可順暢地支援多種表單型別。 這些類別包括：

* PDF forms(XDP / Acroform /一般PDF)
* 新HTML表單
* 影像
* 協力廠商應用程式（例如，通訊管理）

本檔案會從語意自訂/元件重複使用的角度來說明這些轉譯器的運作方式，以便在不中斷任何轉譯的情況下符合客戶需求。 雖然AEM Forms工作區允許任何使用者介面/語意變更，但建議您不要變更不同表單型別的轉譯邏輯，否則結果可能會無法預測。 本檔案旨在提供指導/知識，以支援在不同入口網站中使用相同工作區元件來轉譯相同表單，而非用於修改轉譯邏輯本身。

## PDF forms {#pdf-forms}

PDF forms由`PdfTaskForm View`轉譯。

XDP表單轉譯為PDF時，FormsAugmenter服務會新增`FormBridge`JavaScript™。 此JavaScript™ (位於PDF表單內)有助於執行表單提交、表單儲存或離線建立表單等動作。

在AEM Forms工作區中，PDFTaskForm檢視會透過位於`/lc/libs/ws/libs/ws/pdf.html`的中介HTML與`FormBridge`JavaScript通訊。 流程為：

**PDFTaskForm檢視 — pdf.html**

使用`window.postMessage` / `window.attachEvent('message')`通訊

此方法為父框架與iframe之間的標準通訊方式。 先前開啟的事件中現有的事件接聽程式會在新增新的PDF forms之前移除。 此永久刪除也會考量在任務詳細資料檢視中的表單標籤和歷史記錄標籤之間切換。

**pdf.html - `FormBridge`已轉譯PDF內的JavaScript**

使用`pdfObject.postMessage` / `pdfObject.messageHandler`通訊

此方法是與來自HTML的PDFJavaScript通訊的標準方式。 PdfTaskForm檢視也會處理一般PDF並加以呈現。

>[!NOTE]
>
>不建議編輯PdfTaskForm檢視的pdf.html /內容。

## 新HTMLForms {#new-html-forms}

新的HTML表單由NewHTMLTaskForm檢視轉譯。

使用部署在CRX上的行動表單套件將XDP表單轉譯為HTML時，也會將額外的`FormBridge`JavaScript新增至表單，這會公開儲存和提交表單資料的不同方法。

此JavaScript與上述PDF forms中提到的不同，但其用途類似。

>[!NOTE]
>
>Adobe不建議編輯NewHTMLTaskForm檢視的內容。

## Flex Forms與指南 {#flex-forms-and-guides}

Flex Forms會分別以SwfTaskForm和HtmlTaskForm檢視來轉譯。

在AEM Forms工作區中，這些檢視會使用出現在`/lc/libs/ws/libs/ws/WSNextAdapter.swf`的中介SWF，與構成Flex®表單/指南的實際SWF通訊

使用`swfObject.postMessage` / `window.flexMessageHandler`進行通訊。

此通訊協定由`WsNextAdapter.swf`定義。 視窗物件上的現有`flexMessageHandlers`在新增新的表單之前，會先從先前開啟的SWF表單中移除。 此邏輯也會考量在任務詳細資料檢視中的表單標籤和歷程記錄標籤之間切換。 `WsNextAdapter.swf`用於執行各種表單動作，例如儲存或提交。

>[!NOTE]
>
>不建議修改`WSNextAdapter.swf`或SwfTaskForm / HtmlTaskForm檢視的內容。

## 協力廠商應用程式（例如，通訊管理） {#third-party-applications-for-example-correspondence-management}

協力廠商應用程式是使用ExtAppTaskForm檢視呈現。

**協力廠商應用程式到AEM Forms工作區通訊**

AEM Forms工作區監聽`window.global.postMessage([Message],[Payload])`

[訊息]可以是指定為`SubmitMessage`的字串| `CancelMessage`| `ErrorMessage`| `runtimeMap`中的`actionEnabledMessage`。 協力廠商應用程式必須使用此介面，視需要通知AEM Forms工作區。 使用此介面是強制性的，因為AEM Forms工作區必須知道何時提交任務，才能清除任務視窗。

**AEM Forms工作區與協力廠商應用程式通訊**

如果AEM Forms工作區的直接動作按鈕可見，它會呼叫`window.[External-App-Name].getMessage([Action])`，其中會從`routeActionMap`讀取`[Action]`。 協力廠商應用程式必須接聽此介面，然後透過`postMessage ()` API通知AEM Forms工作區。

例如，Flex應用程式可定義`ExternalInterface.addCallback('getMessage', listener)`以支援此通訊。 如果協力廠商應用程式想要透過自己的按鈕處理表單提交，則您應該指定`hideDirectActions = true() in the runtimeMap`，而且您可以略過此接聽程式。 因此，此建構為選用。

您可以在[在AEM Forms工作區中整合通訊管理](/help/forms/using/integrating-correspondence-management-html-workspace.md)，瞭解有關通訊管理的第三方應用程式整合的更多資訊。
