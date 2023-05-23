---
title: 在AEM Sites單頁應用中嵌入自適應表單或交互通信
seo-title: Embed adaptive forms or Interactive Communications in AEM Sites pages
description: 在AEM Sites頁中嵌入自適應表單或交互通信。 用戶可以填寫和提交表單，而無需離開「站點」頁面。
seo-description: You can embed adaptive forms or Interactive Communication in AEM Sites pages. Users can fill and submit forms without leaving the Sites page.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: Adaptive Forms
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---

# 在AEM Sites單頁應用中嵌入自適應表單或交互通信{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概觀 {#overview}

AEM Forms公司允許表單開發商在AEM Sites單頁應用程式(SPA)中無縫嵌入自適應表單和交SPA互通信。 嵌入式自適應表單和交互通信功能完全，用戶無需離開頁面即可填寫和提交表單。 它幫助用戶保持在網頁上其他元素的上下文中，並同時與自適應表單或交互通信進行交互。

在AEM Sites單頁應用程式中，可以使用 [AEM FormsSPA集裝箱元件](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[。](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) 它是AEM Sites的一個AEM Forms組SPA件，您可以將其添加到「站點」頁面。

有關在非AEM Sites中嵌入自適應表單的SPA資訊，請參見 [在AEM Sites頁中嵌入自適應表單或互動式通信](/help/forms/using/embed-adaptive-form-aem-sites.md)。

## 必備條件 {#prerequisites}

要使用AEM Forms容器元件在AEM站點SPA中嵌入自適應表SPA單或交互通信，請確保已安裝：

* Java SE開發工具包8或更高版本
* Apache Maven 3.3.1或更高版本
* AEM作者實例
* [AEM Forms6.4.2附加軟體包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 關於作者實例

## 安裝AEM FormsSPA集裝箱元件 {#install-aem-forms-spa-container-component}

執行以下步驟安裝AEM FormsSPA容器元件：

1. [克隆或下載AEM Forms組SPA件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa)。
1. 為安裝AEM Forms組SPA件。 有關安裝元件的說明，請參見 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) 的子菜單。

   該元件包括 [樣品反應組分](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) 可用於將容器元件SPA與基於React的項目集SPA成。

1. [克隆或下載基於反應的項SPA目](https://github.com/adobe/aem-sample-we-retail-journal)。
1. 使SPA用中提供的指SPA令將容器元件與基於React的項目整合 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) 的子菜單。

   安裝AEM FormsSPA集裝箱元件並將元件與基於React的項SPA目整合後，可以在AEM Sites頁中嵌入自適應表單和交互通信。

## 嵌入自適應表單或交互通信 {#af-component}

要使用「用於容器的AEM Forms」元件嵌入自適應表單或交SPA互通信：

1. 在編AEM輯模式下開啟站點頁，您要在其中嵌入自適應表單或互動式通信。
1. 插入 **AEM窗體SPA** 的元件：

   * 在「站點」頁面上按一下佈局容器，按一下 **+** 的 **AEM窗體SPA** 元件。

   * 在「元件」瀏覽器面板中，拖放 **AEM窗體SPA** 元件。
   * 在「資產」瀏覽器中搜索自適應表單或互動式通信，然後將其拖放到「站點」頁。 它將形狀嵌在AEM Forms中，用於SPA元件容器。

   >[!NOTE]
   >
   >不支援在SPA頁上呈現多個AEM Forms容器元件。 您可以在一頁上SPA具有多個AEM Forms容器，但一次只呈現一個元件。 確保頁面上只顯示一個元件以避免出現差異。

1. 在站點頁SPA面中按一下嵌入的AEM Forms容器元件，然後按一下 ![設定表徵圖](assets/settings_icon.png) 按鈕。 的 **編輯AEM FormsSPA容器** 對話框。
1. 在 **編輯AEM Forms容器** 對話框，指定以下內容：

   * **資產類型：** 選擇要嵌入的資產類型。 選項包括 **自適應窗體** 和 **互動式通信**

   * **資產路徑**:瀏覽並選擇要嵌入的自適應表單或互動式通信。 如果使用「資產」瀏覽器插入了自適應表單或互動式通信，則自動填充該欄位。
   * **頻道** （僅限互動式通信）:選擇要嵌入的互動式通道類型。 選項包括 **Web通道** 和 **打印通道**。

   * **主題**:選擇一個主題，該主題為自適應窗體或互動式通信的元件定義樣式。 樣式包括外觀屬性，如字型樣式、背景顏色、尺寸和對齊方式。

1. 點擊 ![完成表徵圖](assets/done_icon.png) 按鈕。 自適應表單或互動式通信現在嵌入到頁面中。

## 發佈嵌入式自適應表單與交互通信 {#publish-embedded-adaptive-form-and-interactive-communication}

請考慮以下方案，在AEM Sites頁上發佈嵌入式資產（自適應表單或互動式通信）:

* 如果您是首次發佈AEM Sites頁面，並且該頁面包含嵌入式自適應表單或互動式通信，請發佈「站點」頁面和嵌入式資產。
* 如果僅在已發佈的「站點」頁中修改了嵌入的自適應表單或互動式通信，請發佈原始資產，更改將反映在已發佈的「站點」頁中。 「已發佈的站點」頁面包含對資產的引用，不需要重新發佈該頁面。
* 如果修改了「站點」頁和嵌入式自適應表單或互動式通信，請重新發佈「站點」頁和嵌入式資產。

## 修改嵌入式自適應表單與交互通信 {#modify-embedded-adaptive-form-and-interactive-communication}

站點AEM頁維護對AEM Forms容器中自適應表單和交互通信的引用。 因此，所有配置和屬性（如以原始自適應形式配置的主題、樣式和提交操作）和交互通信都保留在嵌入式自適應形式和交互通信中。

要修改嵌入式自適應表單和互動式通信的任何配置或屬性，請執行以下操作之一。

* 在各自的編輯器中以自適應表單或互動式通信方式開啟原始表單並修改它們。
* 在「站點」頁面中以編輯模式按一下自適應表單或互動式通信，然後按一下 **在新窗口中編輯**。 原始窗體在編輯模式下開啟。

## 考慮事項和最佳做法 {#considerations-and-best-practices}

在站點頁面中嵌入自適應表單時，請牢記AEM以下幾點：

* 原始表單中的頁眉和頁腳不包括在嵌入表單中。
* 在表單門戶的「草稿」和「已提交」Forms頁籤中，支援並可看到嵌入表單的用戶草稿和提交。
* 原始表單上配置的提交操作將保留在嵌入表單中。
* 在原始表單上配置的體驗目標和A/Btest在嵌入式表單中不起作用。 但是，您可以使用「站點」頁上的體驗目標根據用戶配置檔案顯示不同的表單。
* 如果您為原始表單配置了Adobe Analytics，則嵌入表單的分析資料將在Adobe Analytics捕獲。 但是，表單分析報表中不提供它。
