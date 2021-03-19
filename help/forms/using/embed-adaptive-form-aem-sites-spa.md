---
title: 在AEM Sites單頁應用程式中嵌入自適應表單或互動式通訊
seo-title: 將最適化表單或互動式通訊內嵌於AEM Sites頁面
description: 將最適化表單或互動式通訊內嵌在AEM Sites頁面。 使用者可以填寫和提交表單，而不需離開「網站」頁面。
seo-description: 您可以在AEM Sites頁面中嵌入最適化表單或互動式通訊。 使用者可以填寫和提交表單，而不需離開「網站」頁面。
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
feature: 適用性表單
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---


# 在AEM Sites單頁應用程式中內嵌最適化表單或互動式通訊{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 概覽 {#overview}

AEM Forms公司允許表單開發人員在AEM Sites單頁應用程式(SPA)中順暢地內嵌調適性表單和互動式通訊。 內嵌的最適化表單和互動式通訊功能完整，使用者可填寫並提交表單，而不需離開頁面。 它可協助使用者在網頁上保留其他元素的上下文，並同時與最適化表單或互動式通訊互動。

在「AEM Sites單頁應用程式」中，您可以使用[AEM Forms容器元件&lt;a1/SPA>新增最適化表單或互動式通訊。](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) 它是AEM Sites的AEM Forms元件，SPA您可以將其添加到「站點」頁面。

有關在非AEM Sites嵌入自適應表單的資訊，請參SPA閱[在AEM Sites頁](/help/forms/using/embed-adaptive-form-aem-sites.md)中嵌入自適應表單或交互通信。

## 必備條件 {#prerequisites}

若要使用「AEM Forms容器」元件將最適化表單或AEM互動SPA式通SPA訊內嵌在網站中，請確定您已安裝：

* Java SE Development Kit 8或更新版本
* Apache Maven 3.3.1或更新版本
* AEMauthor instance
* [AEM Forms6.4.2附加套件作](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 者實例

## 安裝AEM FormsSPA容器元件{#install-aem-forms-spa-container-component}

執行下列步驟安裝AEM FormsSPA容器元件：

1. [克隆或下載AEM Forms元件SPA](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa)。
1. 為安裝AEM Forms組SPA件。 有關安裝元件的說明，請參見[README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component)檔案。

   該元件包括[樣本反應元件](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component)，其可用於將容器元件SPA與基於反應的項SPA目整合。

1. [仿製或下載React-based專SPA案](https://github.com/adobe/aem-sample-we-retail-journal)。
1. 使用SPA[README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor)檔SPA案中的說明，將容器元件與React-based專案整合。

   在安裝AEM FormsSPA集裝箱元件並將元件與基於React的項目集SPA成後，您可以在AEM Sites頁面中嵌入自適應表單和互動式通信。

## 嵌入最適化表單或互動式通訊{#af-component}

若要使用「容器用AEM Forms」元件嵌入最適化表單或互SPA動式通訊：

1. 以編輯AEM模式開啟網站頁面，您要在其中內嵌最適化表單或互動式通訊。
1. 使用下列任一選AEM項將&lt;a0/SPA> Form for **元件插入頁面：**

   * 點選「Sites（網站）」頁面上的版面容器，點選&#x200B;**+**&#x200B;並選取「Form for AEM SPA **」元件。**

   * 從「元件瀏覽器」面板，拖放頁面上的AEM&lt;a0/SPA> Form for **元件。**
   * 在「資產」瀏覽器中搜尋最適化表單或互動式通訊，並拖放至「網站」頁面。 它將表格嵌入AEM Forms的元SPA件容器。

   >[!NOTE]
   >
   >不支援在SPA頁面上轉換多個AEM Forms容器元件。 頁面上可以有多SPA個AEM Forms容器，但一次只會呈現一個元件。 請確定頁面上只顯示一個元件，以避免不一致。

1. 點選網站頁SPA面中的內嵌AEM Forms容器元件，然後點選動作列上的![settings_icon](assets/settings_icon.png)。 **編輯AEM Forms容SPA器**&#x200B;對話框開啟。
1. 在&#x200B;**編輯AEM Forms容器**&#x200B;對話方塊中，指定下列項目：

   * **資產類型：** 選取要內嵌的資產類型。選項為&#x200B;**自適應表單**&#x200B;和&#x200B;**交互通信**

   * **資產路徑**:瀏覽並選取要內嵌的最適化表單或互動式通訊。如果使用「資產」瀏覽器插入最適化表單或「互動式通訊」，則會自動填入欄位。
   * **頻道** （僅限互動式通訊）:選取要內嵌的互動式渠道類型。選項為&#x200B;**Web通道**&#x200B;和&#x200B;**打印通道**。

   * **主題**:選取一個主題，定義最適化表單或互動式通訊元件的樣式。樣式包括外觀屬性，如字型樣式、背景顏色、尺寸和對齊方式。

1. 點選![done_icon](assets/done_icon.png)以儲存設定。 最適化表單或互動式通訊現在內嵌在頁面中。

## 發佈內嵌的最適化表單和互動式通訊{#publish-embedded-adaptive-form-and-interactive-communication}

請考慮以下情況，以便在AEM Sites頁面上發佈內嵌資產（最適化表單或互動式通訊）:

* 如果您是第一次發佈AEM Sites頁面，且其中包含內嵌的最適化表單或互動式通訊，請發佈網站頁面和內嵌資產。
* 如果您只修改發佈網站頁面中內嵌的最適化表單或互動式通訊，請發佈原始資產，而變更會反映在發佈的網站頁面中。 發佈的「網站」頁面包含資產的參考，不需要重新發佈頁面。
* 如果您修改了「網站」頁面和內嵌的最適化表單或互動式通訊，請重新發佈「網站」頁面和內嵌資產。

## 修改嵌入式自適應表單和互動式通信{#modify-embedded-adaptive-form-and-interactive-communication}

網站頁AEM面會在「AEM Forms容器」中保留對最適化表單和互動式通訊的參考。 因此，所有配置和屬性（例如以原始自適應形式配置的主題、樣式和提交操作）和互動式通信都保留在嵌入式自適應形式和互動式通信中。

要修改嵌入式自適應表單和互動式通信的任何配置或屬性，請執行以下操作之一。

* 以最適化表單或個別編輯器中的互動式通訊方式開啟原始表單，並加以修改。
* 以編輯模式從「網站」頁麵點選最適化表單或互動式通訊，然後點選「在新視窗中編輯」****。 原始表單在編輯模式下開啟。

## 注意事項和最佳做法{#considerations-and-best-practices}

在網站頁面中內嵌最適化表單時，請牢記以AEM下幾點：

* 原始表單中的頁首和頁尾不包含在嵌入表單中。
* 在表單入口網站的「草稿」和「已提交」Forms標籤中，支援並顯示內嵌表單的使用者草稿和提交。
* 原始表單上設定的提交動作會保留在內嵌表單中。
* 在原始表單上設定的體驗定位和A/B測試無法在內嵌表單中運作。 不過，您可以使用「網站」頁面上的體驗定位功能，根據使用者設定檔顯示不同的表單。
* 如果您已為原始表單設定Adobe Analytics，內嵌表單的分析資料會在Adobe Analytics擷取。 不過，表單分析報表中不提供此選項。

