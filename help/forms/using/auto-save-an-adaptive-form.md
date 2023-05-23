---
title: 自動保存自適應表單
seo-title: Auto-save an adaptive form
description: 您可以配置自適應表單以基於事件或預定義時間間隔自動開始保存內容
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

# 自動保存自適應表單 {#auto-save-an-adaptive-form}

您可以配置一個自適應表單，以便根據事件或預定義的時間間隔自動開始保存內容。 預設情況下，自適應表單的內容會保存在用戶操作上，如按「保存」按鈕。 自動保存選項在以下方面非常有用：

* 自動為匿名用戶和登錄用戶保存內容
* 保存表單的內容而無需或用戶干預最少
* 開始基於用戶事件保存表單的內容
* 在指定時間間隔後重複保存表單的內容

## 為自適應表單啟用自動保存 {#enable-autosave-for-an-adaptive-form}

對於自適應表單，不會在框外啟用自動保存選項。 可以從 **自動保存** 的子菜單。 的 **自動保存** 部分還提供了其他幾個配置選項。 執行以下步驟以啟用和配置自適應表單的自動保存選項：

1. 要訪問屬性中的自動保存部分，請選擇一個元件，然後點擊 ![欄位級](assets/field-level.png) > **[!UICONTROL 自適應窗體容器]**，然後按一下 ![招商](assets/cmppr.png)。
1. 在 **[!UICONTROL 自動保存]** 的 **[!UICONTROL 啟用]** 自動保存。
1. 在 **[!UICONTROL 自適應窗體事件]** 框中，指定1或TRUE以在表單載入到瀏覽器中時自動開始保存表單。 您還可以為事件指定條件表達式，當觸發並返回true時，該表達式將開始保存表單的內容。
1. 指定觸發器。 根據您的配置觸發自動保存。 您的選項包括：

   * **[!UICONTROL 基於時間：]** 選擇選項以根據特定時間間隔開始保存內容。
   * **[!UICONTROL 基於事件：]** 選擇選項以在觸發事件時開始保存內容。

   選擇觸發器時，將啟用「策略配置」框。 「策略配置」框允許您：

   * 如果選擇，則指定時間間隔 **[!UICONTROL 基於時間]** 觸發器。
   * 如果選擇，請指定事件名稱 **[!UICONTROL 基於事件]** 觸發器。

   您還可以建立自定義策略並將其添加到清單中。 有關詳細資訊，請參閱 [實施自定義策略以自動保存表單](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)。

1. （僅限基於時間的自動保存）執行以下步驟來配置基於時間的自動保存選項。

   1. 在 **[!UICONTROL 在此間隔自動保存]** 框中，以秒為單位指定時間間隔。 在間隔框中指定的秒數過後，會重複保存表單。

1. （僅基於事件的自動保存）執行以下步驟來配置基於事件的自動保存選項。

   1. 在 **此事件後自動保存** 框，指定 [導橋](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 的子菜單。 每次表達式計算為TRUE時，都會保存表單。

1. （可選）要自動為匿名用戶保存內容，請選擇 **為匿名用戶啟用自動保存** ，然後按一下 **[!UICONTROL 確定]**。

   >[!NOTE]
   >
   >要使匿名用戶使用自動保存選項，請確保將Forms通用配置服務配置為允許所有用戶預覽、驗證和簽名表單。
   >
   >要配置服務，請轉AEM到Web控制台配置 `https://server:port/system/console/configMgr` 編輯 **[!UICONTROL Forms通用配置服務]** 的子菜單。 **[!UICONTROL 所有用戶]** 的上界 **[!UICONTROL 允許]** ，並保存配置。

## 實施自定義策略以啟用自動保存以適應表單 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

您可以實現自定義事件以觸發自動保存功能。 執行以下步驟建立並實施自定義事件：

1. 建立客戶端庫和客戶端庫資料夾。 有關詳細步驟，請參見 [使用客戶端庫文檔](/help/sites-developing/clientlibs.md)。

   例如，以下指令碼使用自定義 `emailFocusChange`觸發自動保存功能的事件：

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
   >在建立客戶端庫資料夾時定義類別屬性。 使分配給類別屬性的值保持方便。

1. 在作者模式下開啟自適應窗體。

1. 在編輯模式下，選擇一個元件，然後點擊 ![欄位級](assets/field-level.png) > **[!UICONTROL 自適應窗體容器]**，然後按一下 ![招商](assets/cmppr.png)。
1. 在屬性中，開啟 **[!UICONTROL 基本]** 的子菜單。 在 **[!UICONTROL 客戶端庫類別]** 框中，輸入在建立客戶端庫資料夾時定義的類別屬性的值。
1. 開啟「自動保存」部分。 在 **[!UICONTROL 此事件後自動保存]** 框中，指定客戶端庫中已定義的自定義事件。 按一下&#x200B;**[!UICONTROL 「確定」]**。
