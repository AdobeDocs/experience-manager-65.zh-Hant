---
title: 在AEM網站頁面中內嵌最適化表單或互動式通訊
seo-title: 在AEM網站頁面中內嵌最適化表單或互動式通訊
description: 您可以在AEM網站頁面中內嵌最適化表單。 使用者可以填寫和提交表單，而不需離開網站頁面。
seo-description: 您可以在AEM網站頁面中內嵌最適化表單。 使用者可以填寫和提交表單，而不需離開網站頁面。
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在AEM網站頁面中內嵌最適化表單或互動式通訊 {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## 概覽 {#overview}

AEM Forms可讓表單開發人員將最適化表單和互動式通訊順暢地內嵌在AEM網站頁面或AEM以外代管的網頁中。 嵌入式自適應表單與互動式通訊功能完整，使用者可填寫並提交表單，而不需離開頁面。 它可協助使用者在網頁上保留其他元素的內容，並同時與表單或互動式通訊互動。

如需在外部網頁中內嵌最適化表單的詳細資訊，請參閱 [在外部網頁中內嵌最適化表單](/help/forms/using/embed-adaptive-form-external-web-page.md)。

在「AEM網站」頁面中，您可以使用下列方式新增最適化表單或互動式通訊：

* **[AEM Forms Container元件](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**AEM Forms提供可新增至網站頁面的元件。 AEM Forms Container元件可讓您內嵌最適化表單和互動式通訊。

* **[資產瀏覽](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**器您建立的所有表單和互動式通訊都可在「資產」下取用。 您可以將表單拖放為頁面上的資產。

## 必備條件 {#prerequisites}

若要在使用可編輯範本的AEM網站頁面中內嵌最適化表單或互動式通訊，請確定AEM表單元件已設定為相關範本中允許的元件。 如需詳細資訊，請參 **閱「建立頁面範本」中的「原則與屬性（版面容器）**[」一節](/help/sites-authoring/templates.md)。

若是使用靜態範本的「網站」頁面，您必須在網站頁面的段落系統中加以設定。 如需詳 [細資訊，請參閱在設計模式中設定元件](/help/sites-authoring/default-components-designmode.md) 。

## 嵌入自適應表單或互動式通信 {#af-component}

若要使用AEM Forms Container元件嵌入最適化表單或互動式通訊：

1. 以編輯模式開啟AEM網站頁面，您要在其中內嵌最適化表單或互動式通訊。
1. 從「元件瀏覽器」面板，將AEM Forms Container元件拖放至頁面上。

   或者，您也可以在「資產」瀏覽器中搜尋最適化表單或互動式通訊，並將它拖放至「網站」頁面。 它會將表單內嵌在AEM Forms容器中。

   >[!NOTE]
   >
   >不支援頁面上的多個AEM Forms Container元件。

1. 在網站頁面中點選內嵌的AEM Forms Container元件，然後點選動 ![作列上的settings_icon](assets/settings_icon.png) 。 「編 **[!UICONTROL 輯AEM Forms容器]** 」對話方塊隨即開啟。
1. 在「編輯AEM Forms容器」對話方塊中，指定下列項目。

   * **** 資產類型：選取要內嵌的資產類型。 選項包括可調式表單和互動式通訊
   * **資產路徑**:瀏覽並選擇要嵌入的最適化表單或互動式通訊。 如果您從「資產」瀏覽器中刪除，則會自動填入。
   * （僅限最適化表單）貼 **文提交**:選擇表單提交時要觸發的動作。 您可以選擇顯示感謝訊息或感謝頁面。

      * **感謝訊息**:使用Rich Text編輯器撰寫訊息，以在表單提交時顯示。 只有當您選擇顯示感謝訊息時，才可使用此選項。
      * **感謝頁面**:瀏覽並選取要在表單提交時顯示的頁面。 只有在您選擇顯示感謝頁面時，此選項才可用。
      * **提交時刷新頁**:啟用以重新整理包含內嵌最適化表單的頁面，以顯示感謝頁面。 否則，感謝頁面會取代AEM Forms容器中的最適化表單，而不會重新整理頁面。 只有在您選擇顯示感謝頁面時，此選項才可用。
   * **主題**:選取主題，以定義最適化表單或互動式通訊元件的樣式。 樣式包括外觀屬性，如字型樣式、背景顏色、尺寸和對齊方式。
   * **高度**:指定容器的高度。 保留為空白，以自動調整容器大小。
   * **CSS用戶端程式庫**:指定CSS用戶端程式庫的路徑。


1. 儲存設定。 最適化表單或互動式通訊現在內嵌在頁面中。

## 發佈內嵌的最適化表單和互動式通訊 {#publishing-embedded-adaptive-form-and-interactive-communication}

讓我們考慮以下案例，以便在AEM網站頁面中發佈內嵌資產（最適化表單或互動式通訊）:

* 如果您是第一次發佈AEM網站頁面，且其中包含內嵌的最適化表單或互動式通訊，請發佈網站頁面和內嵌資產。
* 如果您只修改發佈網站頁面中內嵌的最適化表單或互動式通訊，請發佈原始資產，而變更會反映在發佈的網站頁面中。 發佈的網站頁面包含資產的參考，不需要重新發佈頁面。
* 如果您修改了網站頁面和內嵌的最適化表單或互動式通訊，請重新發佈網站頁面和內嵌資產。

## 修改嵌入式自適應表單和互動式通信 {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM網站頁面會在AEM Forms Container中維護最適化表單和互動式通訊的參考。 因此，所有配置和屬性（如主題、樣式和提交動作）都保留在嵌入式自適應形式和互動式通信中，這些配置和屬性在原始自適應形式和互動式通信中配置。

要修改嵌入式自適應表單和互動式通信的任何配置或屬性，請執行下列操作之一。

* 以最適化表單或個別編輯器中的互動式通訊方式開啟原始表單，並加以修改。
* 以編輯模式從網站頁麵點選最適化表單或互動式通訊，然後在新視 **[!UICONTROL 窗中點選編輯]**。 原始表單會以可修改的編輯模式開啟。

>[!NOTE]
>
>原始自適應表單或互動式通訊所做的變更會自動反映在內嵌表單中。 不過，請重新發佈最適化表單、互動式通訊或網站頁面，以反映已發佈頁面中的變更。

## 考量事項和最佳實務 {#considerations-and-best-practices}

在AEM網站頁面中內嵌最適化表單時，請牢記以下幾點：

* 原始表單中的頁首和頁尾不包含在嵌入表單中。
* 支援使用者提交內嵌表單的草稿，並可在表單入口網站的「草稿」和「已提交表單」標籤中看到。
* 原始表單上設定的提交動作會保留在內嵌表單中。
* 在原始表單上設定的體驗定位和A/B測試無法在內嵌表單中運作。 不過，您可以使用網站頁面上的體驗定位功能，根據使用者個人檔案呈現不同的表單。
* 如果您已針對原始表單設定Adobe Analytics，內嵌表單的分析資料會擷取到Adobe Analytics中。 不過，表單分析報表中不提供此選項。

