---
title: 在AEM網站頁面中內嵌最適化表單或互動式通訊
seo-title: Embed an adaptive form or interactive communication in AEM sites page
description: 您可以在AEM網站頁面中內嵌最適化表單。 使用者無需離開網站頁面即可填寫及提交表單。
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

# 在AEM網站頁面中內嵌最適化表單或互動式通訊 {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## 總覽 {#overview}

AEM Forms可讓表單開發人員將最適化表單和互動式通訊流暢內嵌至AEM Sites頁面或AEM以外托管的網頁。 內嵌的最適化表單和互動式通訊功能完整，使用者無需離開頁面即可填寫及提交表單。 它可協助使用者停留在網頁上其他元素的內容中，並同時與表單或互動式通訊互動。

如需將最適化表單嵌入外部網頁的相關資訊，請參閱 [在外部網頁中內嵌最適化表單](/help/forms/using/embed-adaptive-form-external-web-page.md).

在AEM Sites頁面中，您可以使用下列方式新增最適化表單或互動式通訊：

* **[AEM Forms容器元件](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms提供可新增至網站頁面的元件。 AEM Forms容器元件可讓您內嵌最適化表單和互動式通訊。

* **[資產瀏覽器](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
您建立的所有表單和互動式通訊都可在「資產」下取得。 您可以拖放表單為頁面上的資產。

## 必備條件 {#prerequisites}

若要在使用可編輯範本的AEM網站頁面中嵌入最適化表單或互動式通訊，請確定AEM表單元件已在相關範本中設定為允許的元件。 如需詳細資訊，請參閱 **策略和屬性（佈局容器）** 區段 [建立頁面範本](/help/sites-authoring/templates.md).

若「網站」頁面使用靜態範本，則需在網站頁面的段落系統中進行設定。 請參閱 [在設計模式中配置元件](/help/sites-authoring/default-components-designmode.md) 以取得更多資訊。

## 內嵌最適化表單或互動式通訊 {#af-component}

若要使用AEM Forms容器元件內嵌最適化表單或互動式通訊：

1. 以編輯模式開啟AEM網站頁面，您要在其中嵌入最適化表單或互動式通訊。
1. 從「元件」瀏覽器面板，將「AEM Forms容器」元件拖放至頁面上。

   或者，您也可以在Assets瀏覽器中搜尋最適化表單或互動式通訊，並將其拖放至Sites頁面。 它會將表單嵌入AEM Forms容器中。

   >[!NOTE]
   >
   >頁面上不支援多個AEM Forms容器元件。

1. 點選網站頁面中的內嵌AEM Forms容器元件，然後點選 ![settings_icon](assets/settings_icon.png) 在動作列上。 此 **[!UICONTROL 編輯AEM Forms容器]** 對話框開啟。
1. 在「編輯AEM Forms容器」對話方塊中，指定下列項目。

   * **資產類型：** 選取要內嵌的資產類型。 選項包括最適化表單和互動式通訊
   * **資產路徑**:瀏覽並選取要內嵌的最適化表單或互動式通訊。 如果您從「資產」瀏覽器中拖放，則會自動填入。
   * （僅限適用性表單） **貼文提交**:選取要在表單提交時觸發的動作。 您可以選擇顯示感謝訊息或感謝頁面。

      * **感謝訊息**:使用RTF編輯器撰寫訊息，以在表單提交時顯示。 只有在您選擇顯示感謝訊息時，才可使用此選項。
      * **感謝頁面**:瀏覽並選取要在表單提交時顯示的頁面。 只有在您選擇顯示感謝頁面時，才可使用此選項。
      * **提交時重新整理頁面**:啟用以重新整理包含內嵌適用性表單的頁面，以顯示感謝頁面。 否則，感謝頁面會取代AEM Forms容器中的最適化表單，而不會重新整理頁面。 只有在您選擇顯示感謝頁面時，才可使用此選項。
   * **主題**:選取定義最適化表單或互動式通訊元件樣式的主題。 樣式包括外觀屬性，如字型樣式、背景顏色、尺寸和對齊方式。
   * **高度**:指定容器的高度。 保留為空白以自動調整容器大小。
   * **CSS用戶端程式庫**:指定CSS用戶端程式庫的路徑。


1. 儲存設定。 最適化表單或互動式通訊現已內嵌於頁面中。

## 發佈內嵌的最適化表單和互動式通訊 {#publishing-embedded-adaptive-form-and-interactive-communication}

在AEM網站頁面中發佈內嵌資產（最適化表單或互動式通訊）時，請考量下列案例：

* 如果您是首次發佈AEM網站頁面，且頁面包含內嵌的最適化表單或互動式通訊，請發佈網站頁面和內嵌資產。
* 如果您只修改了已發佈網站頁面中的內嵌適用性表單或互動式通訊，請發佈原始資產，而變更會反映在已發佈的網站頁面中。 已發佈的網站頁面包含對資產的參考，不需要重新發佈頁面。
* 如果您修改了網站頁面和內嵌的最適化表單或互動式通訊，請重新發佈網站頁面和內嵌資產。

## 修改嵌入式自適應表單和交互通信 {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM網站頁面會在AEM Forms容器中維護最適化表單和互動式通訊的參考。 因此，在原始自適應表單中配置的所有配置和屬性（如主題、樣式和提交操作）和交互通信都保留在嵌入的自適應表單和交互通信中。

要修改嵌入式自適應表單和互動式通信的任何配置或屬性，請執行以下操作之一。

* 以最適化表單開啟原始表單，或在個別編輯器中進行互動式通訊，並加以修改。
* 以編輯模式從網站頁面內點選最適化表單或互動式通訊，然後點選 **[!UICONTROL 在新視窗中編輯]**. 原始表單會以可修改的編輯模式開啟。

>[!NOTE]
>
>原始最適化表單或互動式通訊中所做的變更會自動反映在內嵌表單中。 不過，重新發佈最適化表單、互動式通訊或網站頁面，以反映已發佈頁面中的變更。

## 考量事項和最佳實務 {#considerations-and-best-practices}

將最適化表單內嵌至AEM網站頁面時，請謹記以下幾點：

* 原始表單中的頁首和頁尾不包含在嵌入表單中。
* 支援使用者草稿和提交內嵌表單，且可顯示在表單入口網站的「草稿」和「已提交Forms」標籤中。
* 原始表單上配置的提交操作將保留在嵌入式表單中。
* 在原始表單上設定的體驗鎖定目標和A/B測試在內嵌表單中無法運作。 不過，您可以使用網站頁面上的體驗鎖定目標，根據使用者設定檔呈現不同的表單。
* 如果您已為原始表單設定Adobe Analytics，則內嵌表單的分析資料會在Adobe Analytics中擷取。 不過，表單分析報表中無法使用。
