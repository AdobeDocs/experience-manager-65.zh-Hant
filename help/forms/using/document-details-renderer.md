---
title: 轉譯器的檔案詳細資訊
seo-title: 轉譯器的檔案詳細資訊
description: 有關如何在AEM Forms工作區中轉換工作的概念性資訊，以轉換各種支援的表單和檔案類型。
seo-description: 有關如何在AEM Forms工作區中轉換工作的概念性資訊，以轉換各種支援的表單和檔案類型。
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 轉譯器的檔案詳細資訊 {#document-details-for-renderer}

## 簡介 {#introduction}

在AEM Forms工作區中，可順暢地支援多種表單類型。 其中包括：

* PDF表單（XDP / Acroform /平面PDF）
* 新的HTML表格
* 影像
* 協力廠商應用程式（例如，通信管理）

本文從語義自訂／元件復用的角度來說明這些轉譯器的工作，以便滿足客戶需求而不會中斷任何轉譯。 雖然AEM Forms工作區允許任何使用者介面／語義變更，但建議不要變更不同表單類型的轉換邏輯，否則結果可能無法預測。 本檔案旨在提供指導／知識，以支援轉換相同表單、在不同入口網站中使用相同的工作區元件，而非修改轉換邏輯本身。

## PDF表格 {#pdf-forms}

PDF表格由轉換 `PdfTaskForm View`。

當XDP表單轉譯為PDF時，FormsAugmenter服務會新增 `FormBridge` JavaScript™。 此JavaScript™（位於PDF表單內）可協助您執行表單提交、表單儲存或離線表單等動作。

在AEM Forms工作區中，PDFTaskForm檢視會透過 `FormBridge`位於的中介HTML與javascript通訊 `/lc/libs/ws/libs/ws/pdf.html`。 流程是：

**PDFTaskForm檢視- pdf.html**

使用 `window.postMessage` / `window.attachEvent('message')`

此方法是父幀和iframe之間通信的標準方式。 從先前開啟的PDF表格移除現有事件監聽器後，再新增一個。 此清除還考慮在任務詳細資訊視圖中在表單頁籤和歷史記錄頁籤之間切換。

**pdf.html —— 轉譯`FormBridge`的PDF中的javascript**

使用 `pdfObject.postMessage` / `pdfObject.messageHandler`

此方法是從HTML與PDF javascript通訊的標準方式。 PdfTaskForm檢視也會處理平面PDF，並清晰呈現。

>[!NOTE]
>
>不建議修改PdfTaskForm檢視的pdf.html /內容。

## 新的HTML表格 {#new-html-forms}

新的HTML表格由NewHTMLTaskForm檢視轉譯。

當使用部署在CRX上的行動表單套件將XDP表單轉譯為HTML時，它也會新增額外的 `FormBridge` javascript至表單，以提供儲存和送出表單資料的不同方法。

此javascript與上述「PDF表單」中提及的Javascript不同，但其用途類似。

>[!NOTE]
>
>不建議修改NewHTMLTaskForm檢視的內容。

## Flex表單和指南 {#flex-forms-and-guides}

Flex表格由SwfTaskForm轉譯，參考線則由HtmlTaskForm檢視轉譯。

在AEM Forms工作區中，這些檢視會與實際的SWF通訊，而實際的SWF會使用介面SWF(位於 `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

通訊是使用 `swfObject.postMessage` / `window.flexMessageHandler`。

此協定由定義 `WsNextAdapter.swf`。 在新增 `flexMessageHandlers`視窗物件之前，會先移除先前開啟之SWF表單的現有視窗物件。 邏輯還考慮在任務詳細資訊視圖中的表單頁籤和歷史記錄頁籤之間切換。 `WsNextAdapter.swf` 用於執行各種表單動作，例如儲存或送出。

>[!NOTE]
>
>不建議修改SwfTaskForm `WSNextAdapter.swf` / htmlTaskForm視圖的內容。

## 協力廠商應用程式（例如，通信管理） {#third-party-applications-for-example-correspondence-management}

協力廠商應用程式會使用ExtAppTaskForm檢視來轉譯。

**協力廠商應用程式與AEM Forms工作區通訊**

AEM Forms工作區監聽 `window.global.postMessage([Message],[Payload])`

[]`SubmitMessage``CancelMessage`消息`ErrorMessage` 可以是指定為||| `actionEnabledMessage`在 `runtimeMap`。 協力廠商應用程式必須使用此介面，才能視需要通知AEM Forms工作區。 使用此介面是必備的，因為AEM Forms工作區必須知道何時提交工作，以便清除工作視窗。

**AEM Forms工作區與協力廠商應用程式通訊**

如果AEM Forms工作區的直接動作按鈕可見，則會呼叫 `window.[External-App-Name].getMessage([Action])`，其中[ `Action]` 會從中讀取 `routeActionMap`。 協力廠商應用程式必須監聽此介面，然後透過 `postMessage ()` API通知AEM Forms工作區。

例如，Flex應用程式可定義以 `ExternalInterface.addCallback('getMessage', listener)` 支援此通訊。 如果第三方應用程式希望通過其自己的按鈕處理表單提交，則您應指定 `hideDirectActions = true() in the runtimeMap` 並可跳過此偵聽程式。 因此，此構造是可選的。

您可以在「AEM Forms工作區中整合通信管理」中，閱讀有關協力廠商應用程 [式整合與通信管理的更多資訊](/help/forms/using/integrating-correspondence-management-html-workspace.md)。


[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
