---
title: 自動儲存最適化表單
seo-title: Auto-save an adaptive form
description: 您可以設定最適化表單，以根據事件或預先定義的時間間隔自動開始儲存內容
seo-description: You can configure an adaptive form to automatically start saving the content based on an event or a pre-defined time-interval
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Adaptive Forms
exl-id: 948b2c12-895d-49e3-a943-d8fe87174fc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# 自動儲存最適化表單 {#auto-save-an-adaptive-form}

您可以設定最適化表單，以根據事件或預先定義的時間間隔自動開始儲存內容。 依預設，適用性表單的內容會儲存在使用者動作上，例如按下「儲存」按鈕時。 自動儲存選項在下列項目中很實用：

* 自動為匿名和登入的使用者儲存內容
* 不用或最少的用戶干預保存表單的內容
* 開始根據使用者事件儲存表單的內容
* 在指定的時間間隔後重複保存表單的內容

## 啟用最適化表單的自動儲存 {#enable-autosave-for-an-adaptive-form}

對於適用性表單，自動儲存選項不會立即啟用。 您可以從 **自動儲存** 區段（適用性表單的屬性）。 此 **自動儲存** 一節也提供其他數個設定選項。 執行下列步驟來啟用和設定最適化表單的自動儲存選項：

1. 若要存取屬性中的自動儲存區段，請選取元件，然後點選 ![欄位層級](assets/field-level.png) > **[!UICONTROL 適用性表單容器]**，然後點選 ![cppr](assets/cmppr.png).
1. 在 **[!UICONTROL 自動儲存]** 部分， **[!UICONTROL 啟用]** 自動儲存選項。
1. 在 **[!UICONTROL 適用性表單事件]** 框中，指定1或TRUE以在瀏覽器中載入表單時自動開始保存表單。 您也可以為事件指定條件式運算式，當觸發並傳回true時，就會開始儲存表單的內容。
1. 指定觸發器。 會根據您的設定觸發自動儲存。 您的選項為：

   * **[!UICONTROL 時間型：]** 選取根據特定時間間隔開始儲存內容的選項。
   * **[!UICONTROL 事件型：]** 選取要在觸發事件時開始儲存內容的選項。

   選取觸發器時，會啟用「策略配置」框。 「策略配置」框允許您：

   * 如果您選取 **[!UICONTROL 時間型]** 觸發。
   * 如果您選取「 」，請指定事件名稱 **[!UICONTROL 事件型]** 觸發。

   您也可以建立自訂策略，並新增至清單。 如需詳細資訊，請參閱 [實作自訂策略以自動儲存表單](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. （僅限基於時間的自動保存）執行以下步驟來配置基於時間的自動保存的選項。

   1. 在 **[!UICONTROL 在此間隔自動儲存]** 框中，以秒為單位指定時間間隔。 在間隔框中指定的秒數過後，將重複保存該表單。

1. （僅限事件型自動儲存）執行下列步驟來設定事件型自動儲存的選項。

   1. 在 **在此事件後自動儲存** 框，指定 [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 事件。 每次運算式評估為TRUE時，都會儲存表單。

1. （可選）若要自動儲存匿名使用者的內容，請選取 **為匿名用戶啟用自動保存** ，然後按一下 **[!UICONTROL 確定]**.

   >[!NOTE]
   >
   >若要讓自動儲存選項可供匿名使用者使用，請確定您已設定Forms通用設定服務，讓所有使用者都能預覽、驗證和簽署表單。
   >
   >若要設定服務，請前往AEM Web Console設定： `https://server:port/system/console/configMgr` 和編輯 **[!UICONTROL Forms Common Configuration Service]** 來選擇 **[!UICONTROL 所有使用者]** 選項 **[!UICONTROL 允許]** 欄位，並儲存設定。

## 實作自訂策略，以啟用最適化表單的自動儲存 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

您可以實作自訂事件以觸發自動儲存功能。 執行下列步驟以建立和實作自訂事件：

1. 建立客戶端庫和客戶端庫資料夾。 如需詳細步驟，請參閱 [使用用戶端程式庫檔案](/help/sites-developing/clientlibs.md).

   例如，下列指令碼使用自訂 `emailFocusChange`觸發自動儲存功能的事件：

   ```javascript
   window.addEventListener("bridgeInitializeStart", function (){
       guideBridge.connect(function () { guideBridge.on("elementFocusChanged", function (event,data) {
           if(data.target.name === 'Email') {
               guideBridge.trigger("emailFocusChange");
           }
       });
      });
   });
   ```

   >[!NOTE]
   >
   >建立客戶端庫資料夾時定義了類別屬性。 讓指派給類別屬性的值保持實用。

1. 在製作模式中開啟最適化表單。

1. 在編輯模式中，選取元件，然後點選 ![欄位層級](assets/field-level.png) > **[!UICONTROL 適用性表單容器]**，然後點選 ![cppr](assets/cmppr.png).
1. 在屬性中，開啟 **[!UICONTROL 基本]** 區段。 在 **[!UICONTROL 客戶端庫類別]** 框中，輸入建立客戶端庫資料夾時定義的類別屬性的值。
1. 開啟「自動儲存」區段。 在 **[!UICONTROL 在此事件後自動儲存]** 框中，指定已在客戶端庫中定義的自定義事件。 按一下&#x200B;**[!UICONTROL 「確定」]**。
