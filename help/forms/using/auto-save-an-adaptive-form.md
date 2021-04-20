---
title: 自動儲存最適化表單
seo-title: 自動儲存最適化表單
description: 您可以設定自適應表單，以根據事件或預先定義的時間間隔自動開始儲存內容
seo-description: 您可以設定自適應表單，以根據事件或預先定義的時間間隔自動開始儲存內容
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---


# 自動保存最適化表單{#auto-save-an-adaptive-form}

您可以設定自適應表單，以根據事件或預先定義的時間間隔自動開始儲存內容。 預設情況下，自適應表單的內容會保存在用戶操作上，例如按保存按鈕時。 自動儲存選項在下列項目中很實用：

* 自動儲存匿名和登入使用者的內容
* 儲存表單內容，毋需或最少的使用者干預
* 根據使用者事件開始儲存表格內容
* 在指定時間間隔後重複儲存表單內容

## 為最適化表單{#enable-autosave-for-an-adaptive-form}啟用自動儲存

對於最適化表單，自動儲存選項不會立即啟用。 可以從最適化表單屬性的&#x200B;**自動保存**&#x200B;部分啟用自動保存選項。 **自動保存**&#x200B;部分還提供了其他幾個配置選項。 執行以下步驟以啟用和配置最適化表單的自動保存選項：

1. 若要存取屬性中的自動儲存區段，請選取元件，然後點選![field-level](assets/field-level.png) > **[!UICONTROL 最適化表單容器]**，然後點選![cmppr](assets/cmppr.png)。
1. 在&#x200B;**[!UICONTROL 自動儲存]**&#x200B;區段中，**[!UICONTROL 啟用自動儲存選項。]**
1. 在&#x200B;**[!UICONTROL 最適化表單事件]**&#x200B;方塊中，指定1或TRUE，以在表單載入瀏覽器時自動開始儲存表單。 您也可以指定事件的條件運算式，當觸發並傳回true時，會開始儲存表單的內容。
1. 指定觸發器。 會根據您的設定觸發自動儲存。 您的選項包括：

   * **[!UICONTROL 基於時間：]** 選擇根據特定時間間隔開始保存內容的選項。
   * **[!UICONTROL 事件型：選]** 取在觸發事件時開始儲存內容的選項。

   選擇觸發器時，將啟用「策略配置」框。 「策略配置」框可讓您：

   * 如果選擇&#x200B;**[!UICONTROL 基於時間的]**&#x200B;觸發器，請指定時間間隔。
   * 如果您選擇&#x200B;**[!UICONTROL Event based]**&#x200B;觸發器，請指定事件名稱。

   您也可以建立並新增自己的自訂策略至清單。 如需詳細資訊，請參閱[實作自訂策略以自動儲存表單](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)。

1. （僅限基於時間的自動保存）執行以下步驟以配置基於時間的自動保存選項。

   1. 在&#x200B;**[!UICONTROL 自動儲存此間隔]**&#x200B;方塊中，指定以秒為單位的時間間隔。 在間隔框中指定的秒數過後，會重複保存表單。

1. （僅限事件型自動儲存）執行下列步驟以設定事件型自動儲存的選項。

   1. 在&#x200B;**Auto save after this event**&#x200B;方塊中，指定[GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)事件。 每次運算式評估為TRUE時，都會儲存表格。

1. （可選）要自動為匿名用戶保存內容，請選擇&#x200B;**啟用匿名用戶自動保存選項，然後按一下**[!UICONTROL &#x200B;確定&#x200B;]**。**

   >[!NOTE]
   >
   >若要自動儲存選項以供匿名使用者使用，請確定您已設定「Forms通用組態服務」，讓所有使用者都能預覽、驗證和簽署表格。
   >
   >要配置服務，請轉至位於`https://server:port/system/console/configMgr`的AEMWeb控制台配置並編輯&#x200B;**[!UICONTROL Forms公共配置服務]**，以在&#x200B;**[!UICONTROL 允許]**&#x200B;欄位中選擇&#x200B;**[!UICONTROL 所有用戶]**&#x200B;選項，並保存配置。

## 實作自訂策略以啟用最適化表單的自動儲存{#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

您可以實作自訂事件以觸發自動儲存功能。 執行下列步驟以建立並實作自訂事件：

1. 建立客戶端庫和客戶端庫資料夾。 如需詳細步驟，請參閱[使用用戶端程式庫檔案](/help/sites-developing/clientlibs.md)。

   例如，下列指令碼使用自訂`emailFocusChange`事件來觸發自動儲存功能：

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
   >在建立客戶端庫資料夾時定義了類別屬性。 讓指派給類別屬性的值保持方便。

1. 在作者模式中開啟最適化表單。

1. 在編輯模式中，選擇元件，然後點選![field-level](assets/field-level.png) > **[!UICONTROL 最適化表單容器]**，然後點選![cmppr](assets/cmppr.png)。
1. 在屬性中，開啟&#x200B;**[!UICONTROL Basic]**&#x200B;部分。 在&#x200B;**[!UICONTROL 客戶端庫類別]**&#x200B;框中，輸入建立客戶端庫資料夾時定義的類別屬性的值。
1. 開啟「自動儲存」區段。 在&#x200B;**[!UICONTROL Auto save after this event]**&#x200B;方塊中，指定用戶端程式庫中已定義的自訂事件。 按一下&#x200B;**[!UICONTROL 「確定」]**。

