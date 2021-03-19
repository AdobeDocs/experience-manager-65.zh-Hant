---
title: 使用塗鴉簽名將電子簽名套用至表格
seo-title: 使用塗鴉簽名將電子簽名套用至表格
description: 使用塗鴉簽署表格
seo-description: 使用塗鴉簽署表格
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: 適用性表單
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 使用塗鴉簽名將電子簽名套用至表格{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

您可以使用&#x200B;**Scribble Signature**&#x200B;元件和&#x200B;**Signature Step**&#x200B;元件，在最適化表單上繪製(Scribble)簽名。 「簽名」步驟元件會顯示最適化表單的PDF版本。 您需要啟用記錄檔案選項或以表單範本為基礎的最適化表單，才能使用簽名步驟元件。

這兩個元件都提供一個視窗，如下所示，可簽署表格。 您也可以按一下地理位置圖示![aem_6_3_geolocation](assets/aem_6_3_geolocation.png)，將地理位置新增至簽名。

![塗鴉符號對話方塊](assets/scribble-signature.png)

## 設定最適化表單以使用塗鴉簽名{#configure-an-adaptive-form-to-use-scribble-signature}

1. 啟用「記錄檔案」選項或以表單範本為基礎的最適化表單。 有關逐步資訊，請參見[建立自適應表單](../../forms/using/creating-adaptive-form.md)。
1. 將&#x200B;**Scribble Signature**&#x200B;元件從元件瀏覽器拖放至最適化表單。
1. 點選「**設定** ![設定](assets/configure.png)」圖示。 它會開啟屬性瀏覽器並顯示「塗鴉簽名」元件的屬性。 設定Scribble Signature元件的屬性。
1. 將「簽名步驟」元件從元件瀏覽器拖放至最適化表單。

   >[!NOTE]
   >
   >「簽名步驟」元件會佔用表單的全寬。 建議在包含「簽名步驟」元件的部分上不使用任何其他元件。

1. 在「內容」瀏覽器中，點選「表單容器」，然後點選「設定」圖示。 ********![](/help/forms/using/assets/configure.png)它會開啟屬性瀏覽器並顯示最適化表單容器屬性。 導覽至&#x200B;**最適化表單容器** > **電子簽名**&#x200B;並取消選取「啟用Adobe Sign **」選項。**&#x200B;點選「完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」圖示以儲存變更。

   >[!NOTE]
   >
   >將「簽名步驟」元件添加到最適化表單時，會自動選擇「啟用Adobe Sign」選項。

1. 點選「**設定** ![設定](assets/configure.png)」圖示。 它會開啟屬性瀏覽器並顯示「簽名」步驟屬性。 設定下列屬性：

   * **元素名稱**:指定元件的名稱。

   * **標題：** 指定元件的唯一標題。
   * **範本訊息：** 指定在載入簽名PDF時要顯示的訊息。Adobe Sign服務需要一些時間來準備和載入簽名PDF。
   * **簽署服務：** 選取「 **Scribble** Signature」選項。

   * **CSS類別**:指定用戶端程式庫的CSS類別（如果有）。建議使用[主題](../../forms/using/themes.md)和[行內樣式](../../forms/using/inline-style-adaptive-forms.md)來取代CSS類別。

   點選「完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」圖示以儲存變更。 簽名已成功配置。

   現在，當您填寫表格時，會顯示PDF版的最適化表格，並提供簽署PDF檔案的選項。 如需詳細資訊，請參閱[使用塗鴉簽名簽署最適化表單](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)。

## 使用塗鴉簽名{#sign-an-adaptive-form-using-scribble-signature}簽署最適化表單

1. 填寫最適化表單並進入「簽名步驟」頁面後，會顯示簽名畫面。

   ![EchoSign頁面的簽名畫面](assets/esignscribblesign.jpg)

1. 按一下&#x200B;**[!UICONTROL Sign]**。 出現「Scribble sign（塗鴉符號）」對話框。 簽署表單，然後按一下「完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」圖示以儲存簽名。

   ![塗鴉符號對話方塊](assets/scribblewidget.jpg)

1. 按一下「完成」以完成簽署程式。

   ![完成簽署程式](assets/scribblecomplete.jpg)

簽名會新增至表格，表格控制項會移至下一個面板。

