---
title: 在站點頁中嵌入自適應表單或交AEM互通信
seo-title: Embed an adaptive form or interactive communication in AEM sites page
description: 您可以在網站頁中嵌AEM入自適應表單。 用戶可以填寫和提交表單，而無需離開網站頁面。
seo-description: You can embed adaptive forms in AEM sites pages. Users can fill and submit forms without leaving the site pages.
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
feature: Adaptive Forms
exl-id: 00ee7929-649f-4cbb-be79-ba13ac73a16d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# 在站點頁中嵌入自適應表單或交AEM互通信 {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## 概觀 {#overview}

AEM Forms允許表單開發者將自適應表單和交互通信無縫嵌入AEM Sites頁面或外部托管的網AEM頁。 嵌入式自適應表單和交互通信功能完全，用戶無需離開頁面即可填寫和提交表單。 它幫助用戶保持在網頁上其他元素的上下文中，並同時與表單或互動式通信進行交互。

有關在外部網頁中嵌入自適應表單的資訊，請參見 [在外部網頁中嵌入自適應表單](/help/forms/using/embed-adaptive-form-external-web-page.md)。

在「AEM Sites」頁中，可以使用以下方式添加自適應表單或互動式通信：

* **[AEM Forms集裝箱元件](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms提供了可添加到網站頁面的元件。 AEM Forms集裝箱元件允許您嵌入自適應表單和互動式通信。

* **[資產瀏覽器](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
您建立的所有表單和互動式通信都可在「資產」下使用。 您可以將表單作為資產拖放到頁面上。

## 必備條件 {#prerequisites}

要在使用可編輯模板的站點頁中嵌入AEM自適應表單或互動式通信，請確保AEMForm元件在關聯模板中配置為允許的元件。 有關詳細資訊，請參見 **策略和屬性（佈局容器）** 部分 [建立頁面模板](/help/sites-authoring/templates.md)。

如果「站點」頁使用靜態模板，則需要在站點頁的段落系統中配置它。 請參閱 [在設計模式下配置元件](/help/sites-authoring/default-components-designmode.md) 的子菜單。

## 嵌入自適應形式或交互通信 {#af-component}

要使用AEM Forms容器元件嵌入自適應表單或交互通信，請執行以下操作：

1. 在編AEM輯模式下開啟站點頁，您要在其中嵌入自適應表單或互動式通信。
1. 在「元件」瀏覽器面板中，拖放頁面上的「AEM Forms容器」元件。

   或者，可以在「資產」瀏覽器中搜索自適應表單或互動式通信，然後將其拖放到「站點」頁。 它把形狀嵌在AEM Forms集裝箱裡。

   >[!NOTE]
   >
   >不支援頁面上的多個AEM Forms容器元件。

1. 在站點頁面中按一下嵌入的AEM Forms集裝箱元件，然後按一下 ![設定表徵圖](assets/settings_icon.png) 按鈕。 的 **[!UICONTROL 編輯AEM Forms容器]** 對話框。
1. 在「編輯AEM Forms容器」對話框中，指定以下內容。

   * **資產類型：** 選擇要嵌入的資產類型。 這些選項是自適應形式和互動式通信
   * **資產路徑**:瀏覽並選擇要嵌入的自適應表單或互動式通信。 如果從「資產」瀏覽器中刪除它，則會自動填充它。
   * （僅限自適應窗體） **提交後**:選擇要在表單提交時觸發的操作。 您可以選擇顯示感謝信或感謝頁。

      * **謝謝留言**:使用富格文本編輯器編寫消息，以便在提交表單時顯示。 此選項僅在您選擇顯示感謝信時可用。
      * **謝謝頁**:瀏覽並選擇要在表單提交時顯示的頁面。 此選項僅在您選擇顯示感謝頁時可用。
      * **提交時刷新頁面**:啟用以刷新包含嵌入式自適應表單的頁面以顯示感謝頁。 否則，「感謝」頁面將替換AEM Forms容器中的自適應表單，而不刷新頁面。 此選項僅在您選擇顯示感謝頁時可用。
   * **主題**:選擇一個主題，該主題為自適應表單或互動式通信的元件定義樣式。 樣式包括外觀屬性，如字型樣式、背景顏色、尺寸和對齊方式。
   * **高度**:指定容器的高度。 將其留空，以自動調整容器大小。
   * **CSS客戶端庫**:指定CSS客戶端庫的路徑。


1. 保存設定。 自適應表單或互動式通信現在嵌入到頁面中。

## 發佈嵌入式自適應表單和交互通信 {#publishing-embedded-adaptive-form-and-interactive-communication}

讓我們考慮在網站頁中發佈嵌入式資產（自適應表單或互動式通信）的以AEM下情形：

* 如果您是首次發AEM布站點頁面，並且它包含嵌入的自適應表單或互動式通信，則發佈站點頁面和嵌入的資產。
* 如果您僅修改了已發佈網站頁中嵌入的自適應表單或互動式通信，請發佈原始資產，並將更改反映在已發佈網站頁中。 發佈的網站頁面包括對資產的引用，並且不需要重新發佈該頁面。
* 如果修改了站點頁面和嵌入的自適應表單或互動式通信，請重新發佈站點頁面和嵌入的資產。

## 修改嵌入式自適應格式和互動式通信 {#modifying-embedded-adaptive-form-and-interactive-communication}

站點AEM頁面在AEM Forms集裝箱中維護對自適應表單和互動式通信的引用。 因此，所有配置和屬性（如主題、樣式和提交操作）都保留在嵌入式自適應形式和互動式通信中，這些配置和屬性在原始自適應形式和互動式通信中配置。

要修改嵌入式自適應表單和互動式通信的任何配置或屬性，請執行以下操作之一。

* 以自適應表單或各編輯器中的互動式通信方式開啟原始表單並修改它們。
* 以編輯模式從站點頁面中點擊自適應表單或互動式通信，然後點擊 **[!UICONTROL 在新窗口中編輯]**。 原始窗體在可修改的編輯模式下開啟。

>[!NOTE]
>
>原始自適應形式或互動式通信中所做的更改自動反映在嵌入式形式中。 但是，重新發佈自適應表單、互動式通信或網站頁以反映已發佈頁面中的更改。

## 考慮事項和最佳做法 {#considerations-and-best-practices}

在站點頁面中嵌入自適應表單時，請牢記AEM以下幾點：

* 原始表單中的頁眉和頁腳不包括在嵌入表單中。
* 在表單門戶的「草稿」和「已提交」Forms頁籤中，支援並可看到嵌入表單的用戶草稿和提交。
* 原始表單上配置的提交操作將保留在嵌入表單中。
* 在原始表單上配置的體驗目標和A/Btest在嵌入式表單中不起作用。 但是，您可以使用站點頁面上的體驗目標根據用戶配置檔案顯示不同的表單。
* 如果您為原始表單配置了Adobe Analytics，則嵌入表單的分析資料將在Adobe Analytics捕獲。 但是，表單分析報表中不提供它。
