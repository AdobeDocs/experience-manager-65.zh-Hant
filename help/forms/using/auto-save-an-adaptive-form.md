---
title: 自動儲存最適化表單
seo-title: 自動儲存最適化表單
description: 您可以設定自適應表單，以根據事件或預先定義的時間間隔自動開始儲存內容
seo-description: 您可以設定自適應表單，以根據事件或預先定義的時間間隔自動開始儲存內容
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160

---


# 自動儲存最適化表單 {#auto-save-an-adaptive-form}

您可以設定自適應表單，以根據事件或預先定義的時間間隔自動開始儲存內容。 預設情況下，自適應表單的內容會保存在用戶操作上，例如按保存按鈕時。 自動儲存選項在下列項目中很實用：

* 自動儲存匿名和登入使用者的內容
* 儲存表單內容，毋需或最少的使用者干預
* 根據使用者事件開始儲存表格內容
* 在指定時間間隔後重複儲存表單內容

## 為最適化表單啟用自動儲存 {#enable-autosave-for-an-adaptive-form}

對於最適化表單，自動儲存選項不會立即啟用。 您可以在最適化表單的屬性中， **從「自動儲存** 」區段啟用自動儲存選項。 「自 **動保存** 」部分還提供了幾個其它配置選項。 執行以下步驟以啟用和配置最適化表單的自動保存選項：

1. 若要存取屬性中的自動儲存區段，請選取元件，然後點選欄 ![位層級](assets/field-level.png) > **[!UICONTROL 最適化表單容器]**，然後點選 ![cmppr](assets/cmppr.png)。
1. 在「自 **[!UICONTROL 動儲存]** 」區 **[!UICONTROL 段中]** ，啟用自動儲存選項。
1. 在「最 **[!UICONTROL 適化表單事件]** 」方塊中，指定1或TRUE，以在表單載入瀏覽器時自動開始儲存表單。 您也可以指定事件的條件運算式，當觸發並傳回true時，會開始儲存表單的內容。
1. 指定觸發器。 會根據您的設定觸發自動儲存。 您的選項包括：

   * **** 時間型：選擇根據特定時間間隔開始保存內容的選項。
   * **** 事件型：選取在觸發事件時開始儲存內容的選項。
   選擇觸發器時，將啟用「策略配置」框。 「策略配置」框可讓您：

   * 如果選擇基於時間的觸發器，請 **[!UICONTROL 指定時間間隔]** 。
   * 如果您選取事件型觸發器，請指 **[!UICONTROL 定事件]** 名稱。
   您也可以建立並新增自己的自訂策略至清單。 如需詳細資訊，請 [參閱實作自訂策略以自動儲存表單](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)。

1. （僅限基於時間的自動保存）執行以下步驟以配置基於時間的自動保存選項。

   1. 在「自 **[!UICONTROL 動儲存此間隔]** 」方塊中，以秒為單位指定時間間隔。 在間隔框中指定的秒數過後，會重複保存表單。

1. （僅限事件型自動儲存）執行下列步驟以設定事件型自動儲存的選項。

   1. 在「在此 **事件後自動儲存** 」方塊中，指定 [GuideBridge事件](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 。 每次運算式評估為TRUE時，都會儲存表格。

1. （可選）若要自動儲存匿名使用者的內容，請選取「啟用匿名使用者的自動 **儲存」選項** ，然後按一下「 **[!UICONTROL 確定」]**。

   >[!NOTE]
   >
   >若要自動儲存選項以供匿名使用者使用，請確定您已設定Forms Common Configuration Service，讓所有使用者都能預覽、驗證和簽署表格。
   >
   >若要設定服務，請前往AEM Web Console設定，位於 `https://[server]:[host]/system/console/configMgr` 並編輯 **[!UICONTROL Forms Common Configuration Service]** ，以在「允許 **[!UICONTROL 」欄位中選擇「所有使用者]****** 」選項，然後儲存設定。

## 實作自訂策略，以針對最適化表單啟用自動儲存 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

您可以實作自訂事件以觸發自動儲存功能。 執行下列步驟以建立並實作自訂事件：

1. 建立客戶端庫和客戶端庫資料夾。 如需詳細步驟，請參 [閱「使用用戶端程式庫」檔案](/help/sites-developing/clientlibs.md)。

   例如，下列指令碼使用自訂事件 `emailFocusChange`來觸發自動儲存功能：

   ```
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
   >在建立客戶端庫資料夾時定義了類別屬性。 讓指派給類別屬性的值保持方便。

1. 在作者模式中開啟最適化表單。

1. 在編輯模式中，選取元件，然後點選欄 ![位層級](assets/field-level.png) > **[!UICONTROL 最適化表單容器]**，然後點選 ![cmppr](assets/cmppr.png)。
1. 在屬性中，開啟「基 **[!UICONTROL 本]** 」區段。 在「客 **[!UICONTROL 戶端庫類別]** 」框中，輸入建立客戶端庫資料夾時定義的類別屬性的值。
1. 開啟「自動儲存」區段。 在「在此 **[!UICONTROL 事件後自動儲存]** 」方塊中，指定用戶端程式庫中已定義的自訂事件。 按一下 **[!UICONTROL 確定]**。

