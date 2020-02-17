---
title: 在AEM Sites單頁應用程式中內嵌最適化表單或互動式通訊
seo-title: 在AEM Sites頁面中內嵌最適化表單或互動式通訊
description: 在AEM Sites頁面中內嵌最適化表單或互動式通訊。 使用者可以填寫和提交表單，而不需離開「網站」頁面。
seo-description: 您可以在AEM Sites頁面中內嵌最適化表單或互動式通訊。 使用者可以填寫和提交表單，而不需離開「網站」頁面。
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: d12d35bf8355d3069071523427a7794b88c09b13

---


# 在AEM Sites單頁應用程式中內嵌最適化表單或互動式通訊{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概覽 {#overview}

AEM Forms可讓表單開發人員將調適性表單和互動式通訊順暢地內嵌在AEM Sites單頁應用程式(SPA)中。 內嵌的最適化表單和互動式通訊功能完整，使用者可填寫並提交表單，而不需離開頁面。 它可協助使用者在網頁上保留其他元素的上下文，並同時與最適化表單或互動式通訊互動。

在「AEM Sites單頁應用程式」中，您可以使用 [AEM Forms SPA容器元件新增最適化表單或互動式通訊](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[。](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) 它是AEM Sites SPA的AEM Forms元件，您可將其新增至「網站」頁面。

如需將最適化表單內嵌至非SPA AEM網站的詳細資訊，請參閱「在 [AEM網站中內嵌最適化表單或互動式通訊」頁面](/help/forms/using/embed-adaptive-form-aem-sites.md)。

## 必備條件 {#prerequisites}

若要使用AEM Forms SPA容器元件將最適化表單或互動式通訊內嵌在AEM網站SPA中，請確定您已安裝：

* Java SE Development Kit 8或更新版本
* Apache Maven 3.3.1或更新版本
* AEM作者實例
* [作者例項上的AEM Forms 6.4.2附加套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) (Add-on package on author instance)

## 安裝AEM Forms SPA容器元件 {#install-aem-forms-spa-container-component}

執行下列步驟，安裝AEM Forms SPA Container元件：

1. [複製或下載SPA的AEM Forms元件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa)。
1. 安裝SPA的AEM Forms元件。 README.md檔案中提供了安裝該組 [件的說明](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) 。

   該元件包括 [樣本React元件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) ，其可用於將SPA容器元件與基於React的SPA項目整合。

1. [仿製或下載React-based SPA專案](https://github.com/adobe/aem-sample-we-retail-journal)。
1. 使用 [README.md檔案中的說明，將SPA容器元件與基於React的SPA項目整合](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) 。

   在安裝AEM Forms SPA Container元件並將元件與React-based SPA專案整合後，您就可以在「AEM Sites」（AEM網站）頁面中內嵌最適化表單和互動式通訊。

## 內嵌最適化表單或互動式通訊 {#af-component}

若要使用AEM Forms for SPA Container元件嵌入最適化表單或互動式通訊：

1. 以編輯模式開啟AEM網站頁面，您要在其中內嵌最適化表單或互動式通訊。
1. 使用 **下列任一選項，將AEM Form for SPA** 元件插入頁面：

   * 點選「網站」頁面上的版面容器，點選 **+** ，然後選 **取AEM Form for SPA元件** 。

   * 從「元件瀏覽器」面板，將 **AEM Form for SPA元件拖放至頁面上** 。
   * 在「資產」瀏覽器中搜尋最適化表單或互動式通訊，並拖放至「網站」頁面。 它會將表單內嵌在AEM Forms for SPA元件容器中。
   >[!NOTE]
   >
   >不支援在頁面上呈現多個AEM Forms SPA容器元件。 您可以在頁面上擁有多個AEM Forms SPA容器，但一次只會呈現一個元件。 請確定頁面上只顯示一個元件，以避免不一致。

1. 在網站頁面中點選內嵌的AEM Forms SPA Container元件，然後點選動作列 ![上的settings_icon](assets/settings_icon.png) 。 「編 **輯AEM Forms SPA容器** 」對話方塊隨即開啟。
1. 在「編 **輯AEM Forms容器** 」對話方塊中，指定下列項目：

   * **** 資產類型：選取要內嵌的資產類型。 選項包括最適 **化表單** 和互 **動式通訊**

   * **資產路徑**:瀏覽並選取要內嵌的最適化表單或互動式通訊。 如果使用「資產」瀏覽器插入最適化表單或「互動式通訊」，則會自動填入欄位。
   * **頻道** （僅限互動式通訊）:選取要內嵌的互動式渠道類型。 選項包括網 **路頻道****和列印頻道**。

   * **主題**:選取一個主題，定義最適化表單或互動式通訊元件的樣式。 樣式包括外觀屬性，如字型樣式、背景顏色、尺寸和對齊方式。

1. 點選 ![](assets/done_icon.png) 以儲存設定。 最適化表單或互動式通訊現在內嵌在頁面中。

## 發佈內嵌的最適化表單與互動式通訊 {#publish-embedded-adaptive-form-and-interactive-communication}

請考慮下列案例，以便在AEM Sites頁面上發佈內嵌資產（最適化表單或互動式通訊）:

* 如果您是第一次發佈AEM Sites頁面，且其中包含內嵌的最適化表單或互動式通訊，請發佈「網站」頁面和內嵌資產。
* 如果您只修改發佈網站頁面中內嵌的最適化表單或互動式通訊，請發佈原始資產，而變更會反映在發佈的網站頁面中。 發佈的「網站」頁面包含資產的參考，不需要重新發佈頁面。
* 如果您修改了「網站」頁面和內嵌的最適化表單或互動式通訊，請重新發佈「網站」頁面和內嵌資產。

## 修改嵌入式自適應表單和互動式通信 {#modify-embedded-adaptive-form-and-interactive-communication}

AEM網站頁面會在AEM Forms容器中維護最適化表單和互動式通訊的參考。 因此，所有配置和屬性（例如以原始自適應形式配置的主題、樣式和提交操作）和互動式通信都保留在嵌入式自適應形式和互動式通信中。

要修改嵌入式自適應表單和互動式通信的任何配置或屬性，請執行以下操作之一。

* 以最適化表單或個別編輯器中的互動式通訊方式開啟原始表單，並加以修改。
* 在「網站」頁面中以編輯模式點選最適化表單或互動式通訊，然後在新視 **窗中點選「編輯」**。 原始表單在編輯模式下開啟。

## 考量事項和最佳實務 {#considerations-and-best-practices}

在AEM網站頁面中內嵌最適化表單時，請牢記以下幾點：

* 原始表單中的頁首和頁尾不包含在嵌入表單中。
* 支援使用者提交內嵌表單的草稿，並可在表單入口網站的「草稿」和「已提交表單」標籤中看到。
* 原始表單上設定的提交動作會保留在內嵌表單中。
* 在原始表單上設定的體驗定位和A/B測試無法在內嵌表單中運作。 不過，您可以使用「網站」頁面上的體驗定位功能，根據使用者設定檔顯示不同的表單。
* 如果您已針對原始表單設定Adobe Analytics，內嵌表單的分析資料會擷取到Adobe Analytics中。 不過，表單分析報表中不提供此選項。

