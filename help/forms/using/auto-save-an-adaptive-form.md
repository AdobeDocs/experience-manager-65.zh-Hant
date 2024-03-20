---
title: 自動儲存最適化表單
description: 您可以設定最適化表單，以根據事件或預先定義的時間間隔自動開始儲存內容
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: ff9bf466-228d-40e6-9389-15c1f2ed1d2e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 7%

---

# 自動儲存最適化表單 {#auto-save-an-adaptive-form}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

您可以設定最適化表單，以根據事件或預先定義的時間間隔自動開始儲存內容。 依預設，最適化表單的內容會在使用者動作時儲存，例如按下儲存按鈕時。 自動儲存選項非常實用：

* 自動為匿名和登入的使用者儲存內容
* 儲存表單內容而不需要使用者介入或使用者介入很小
* 開始根據使用者事件儲存表單內容
* 在指定的時間間隔後重複儲存表單內容

## 為最適化表單啟用自動儲存 {#enable-autosave-for-an-adaptive-form}

對於最適化表單，不會立即啟用自動儲存選項。 您可以從以下位置啟用自動儲存選項： **自動儲存** 最適化表單的屬性中的區段。 此 **自動儲存** 一節也提供幾個其他設定選項。 執行以下步驟，為最適化表單啟用並設定自動儲存選項：

1. 若要存取屬性中的自動儲存區段，請選取元件，然後選取 ![欄位層級](assets/field-level.png) > **[!UICONTROL 最適化表單容器]**，然後選取 ![cmppr](assets/cmppr.png).
1. 在 **[!UICONTROL 自動儲存]** 部分， **[!UICONTROL 啟用]** 自動儲存選項。
1. 在 **[!UICONTROL 最適化表單事件]** 方塊中，指定1或TRUE會在表單載入瀏覽器時自動開始儲存表單。 您也可以為事件指定條件運算式，觸發並傳回true時，此運算式就會開始儲存表單的內容。
1. 指定觸發器。 系統會根據您的設定觸發自動儲存。 您的選項有：

   * **[!UICONTROL 基於時間：]** 選取選項，以根據特定時間間隔開始儲存內容。
   * **[!UICONTROL 以事件為基礎：]** 選取選項，以便在觸發事件時開始儲存內容。

   當您選取觸發器時，會啟用「策略組態」方塊。 策略設定方塊可讓您：

   * 如果選取，請指定時間間隔 **[!UICONTROL 基於時間]** 觸發器。
   * 如果您選取「 」，請指定事件名稱 **[!UICONTROL 基於事件]** 觸發器。

   您也可以建立自己的自訂策略並新增至清單中。 如需詳細資訊，請參閱 [實施自訂策略以自動儲存表單](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. （僅限以時間為基礎的自動儲存）執行下列步驟，設定「以時間為基礎的自動儲存」選項。

   1. 在 **[!UICONTROL 在此間隔自動儲存]** 方塊，以秒為單位指定時間間隔。 表單會在間隔方塊中指定的秒數過後重複儲存。

1. （僅限事件式自動儲存）執行下列步驟，設定事件式自動儲存的選項。

   1. 在 **在此事件後自動儲存** 方塊，指定 [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 事件。 每次運算式評估為TRUE時，都會儲存表單。

1. （選用）若要自動為匿名使用者儲存內容，請選取 **啟用匿名使用者的自動儲存** 選項，然後按一下 **[!UICONTROL 確定]**.

   >[!NOTE]
   >
   >若要讓自動儲存選項適用於匿名使用者，請務必將Forms通用設定服務設定為允許所有使用者預覽、驗證及簽署表單。
   >
   >若要設定服務，請前往AEM Web主控台設定，網址為 `https://server:port/system/console/configMgr` 並編輯 **[!UICONTROL Forms通用設定服務]** 以選擇 **[!UICONTROL 所有使用者]** 中的選項 **[!UICONTROL 允許]** 欄位並儲存設定。

## 實施自訂策略以啟用最適化表單的自動儲存 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

您可以實作自訂事件以觸發自動儲存功能。 執行以下步驟來建立及實施自訂事件：

1. 建立使用者端程式庫和使用者端程式庫資料夾。 如需詳細步驟，請參閱 [使用使用者端資料庫檔案](/help/sites-developing/clientlibs.md).

   例如，以下指令碼會使用自訂 `emailFocusChange`觸發自動儲存功能的事件：

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
   >類別屬性是在建立使用者端程式庫資料夾時定義。 讓指派給類別屬性的值隨時待命。

1. 以作者模式開啟最適化表單。

1. 在編輯模式中，選取元件，然後選取 ![欄位層級](assets/field-level.png) > **[!UICONTROL 最適化表單容器]**，然後選取 ![cmppr](assets/cmppr.png).
1. 在屬性中，開啟 **[!UICONTROL 基本]** 區段。 在 **[!UICONTROL 使用者端資料庫類別]** 方塊中，輸入建立使用者端資料庫資料夾時定義的類別屬性值。
1. 開啟自動儲存區段。 在 **[!UICONTROL 在此事件後自動儲存]** 方塊中，指定已在使用者端程式庫中定義的自訂事件。 按一下&#x200B;**[!UICONTROL 「確定」]**。
