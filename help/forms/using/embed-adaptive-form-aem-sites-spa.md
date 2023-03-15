---
title: 在AEM Sites單頁應用程式中內嵌最適化表單或互動式通訊
seo-title: Embed adaptive forms or Interactive Communications in AEM Sites pages
description: 在AEM Sites頁面中內嵌最適化表單或互動式通訊。 使用者無需離開「網站」頁面即可填寫及提交表單。
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

# 在AEM Sites單頁應用程式中內嵌最適化表單或互動式通訊{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概觀 {#overview}

AEM Forms可讓表單開發人員將最適化表單和互動式通訊順暢地嵌入AEM Sites單頁應用程式(SPA)。 內嵌的最適化表單和互動式通訊功能完整，使用者無需離開頁面即可填寫及提交表單。 它可協助使用者停留在網頁上的其他元素上，並同時與最適化表單或互動式通訊互動。

在AEM Sites單頁應用程式中，您可以使用 [AEM Forms SPA容器元件](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) 這是AEM Sites SPA的AEM Forms元件，您可將其新增至您的Sites頁面。

如需將最適化表單嵌入非SPA AEM Sites的詳細資訊，請參閱 [在AEM Sites頁面中內嵌最適化表單或互動式通訊](/help/forms/using/embed-adaptive-form-aem-sites.md).

## 必備條件 {#prerequisites}

若要使用AEM Forms SPA容器元件將最適化表單或互動式通訊內嵌至AEM sites SPA，請確定您已安裝：

* Java SE Development Kit 8或更高版本
* Apache Maven 3.3.1或更新版本
* AEM製作例項
* [AEM Forms 6.4.2附加元件套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 在作者例項上

## 安裝AEM Forms SPA容器元件 {#install-aem-forms-spa-container-component}

執行下列步驟，安裝AEM Forms SPA容器元件：

1. [原地複製或下載適用於SPA的AEM Forms元件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. 安裝SPA適用的AEM Forms元件。 安裝元件的說明位於 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) 檔案。

   該元件包括 [樣品反應組分](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) 可用來整合SPA容器元件與React型SPA專案。

1. [複製或下載React型SPA專案](https://github.com/adobe/aem-sample-we-retail-journal).
1. 依照 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) 檔案。

   安裝AEM Forms SPA容器元件並將元件與React型SPA專案整合後，您可以在AEM Sites頁面中內嵌最適化表單和互動式通訊。

## 內嵌最適化表單或互動式通訊 {#af-component}

若要使用AEM Forms for SPA容器元件內嵌最適化表單或互動式通訊：

1. 以編輯模式開啟AEM網站頁面，您要在其中嵌入最適化表單或互動式通訊。
1. 插入 **AEM for SPA** 元件（使用下列任一選項）:

   * 點選「網站」頁面上的版面容器，點選 **+** ，然後選取 **AEM for SPA** 元件。

   * 從「元件」瀏覽器面板，拖放 **AEM for SPA** 元件。
   * 在「資產」瀏覽器中搜尋最適化表單或互動式通訊，並將其拖放至「網站」頁面。 它會將表單內嵌在AEM Forms for SPA元件容器中。

   >[!NOTE]
   >
   >不支援在頁面上呈現多個AEM Forms SPA容器元件。 一個頁面上可以有多個AEM Forms SPA容器，但一次只轉譯一個元件。 請確定頁面上只顯示一個元件，以避免不一致。

1. 在網站頁面中點選內嵌的AEM Forms SPA容器元件，然後點選 ![settings_icon](assets/settings_icon.png) 在動作列上。 此 **編輯AEM Forms SPA容器** 對話框開啟。
1. 在 **編輯AEM Forms容器** 對話框中，請指定以下內容：

   * **資產類型：** 選取要內嵌的資產類型。 選項包括 **適用性表單** 和 **互動式通訊**

   * **資產路徑**:瀏覽並選取要內嵌的最適化表單或互動式通訊。 如果使用Assets瀏覽器插入最適化表單或互動式通訊，則會自動填入欄位。
   * **管道** （僅限互動式通訊）:選取要內嵌的互動式管道類型。 選項包括 **Web頻道** 和 **列印管道**.

   * **主題**:選取定義最適化表單或互動式通訊元件樣式的主題。 樣式包括外觀屬性，如字型樣式、背景顏色、尺寸和對齊方式。

1. 點選 ![done_icon](assets/done_icon.png) 以儲存設定。 最適化表單或互動式通訊現已內嵌於頁面中。

## 發佈內嵌最適化表單與互動式通訊 {#publish-embedded-adaptive-form-and-interactive-communication}

在AEM Sites頁面上發佈內嵌資產（最適化表單或互動式通訊）時，請考量下列案例：

* 如果您是首次發佈AEM Sites頁面，且頁面包含內嵌的最適化表單或互動式通訊，請發佈Sites頁面和內嵌資產。
* 如果您只修改了已發佈網站頁面中的內嵌適用性表單或互動式通訊，請發佈原始資產，而變更會反映在已發佈的網站頁面中。 已發佈的網站頁面包含對資產的參考，不需要重新發佈頁面。
* 如果您修改了「網站」頁面和內嵌的最適化表單或互動式通訊，請重新發佈「網站」頁面和內嵌資產。

## 修改嵌入式自適應表單和互動式通信 {#modify-embedded-adaptive-form-and-interactive-communication}

AEM網站頁面會在AEM Forms容器中維護最適化表單和互動式通訊的參考。 因此，在原始最適化表單和互動式通信中配置的所有配置和屬性（如主題、樣式和提交操作）都將保留在嵌入的最適化表單和互動式通信中。

要修改嵌入式最適化表單和互動式通信的任何配置或屬性，請執行以下操作之一。

* 在個別編輯器中以最適化表單或互動式通訊開啟原始表單，並加以修改。
* 以編輯模式從「網站」頁麵點選最適化表單或互動式通訊，然後點選 **在新視窗中編輯**. 原始表單會以編輯模式開啟。

## 考量事項和最佳實務 {#considerations-and-best-practices}

將最適化表單內嵌至AEM網站頁面時，請謹記以下幾點：

* 原始表單中的頁首和頁尾不包含在嵌入表單中。
* 支援使用者草稿和提交內嵌表單，且可顯示在表單入口網站的「草稿」和「已提交Forms」標籤中。
* 原始表單上配置的提交操作將保留在嵌入式表單中。
* 在原始表單上設定的體驗鎖定目標和A/B測試在內嵌表單中無法運作。 不過，您可以使用網站頁面上的體驗鎖定目標，根據使用者設定檔呈現不同的表單。
* 如果您已為原始表單設定Adobe Analytics，則內嵌表單的分析資料會在Adobe Analytics中擷取。 不過，表單分析報表中無法使用。
