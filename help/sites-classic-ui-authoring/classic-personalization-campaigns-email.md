---
title: 電子郵件營銷
seo-title: E-mail Marketing
description: 電子郵件營銷（例如，新聞稿）是任何營銷活動的重要部分，因為您使用它們將內容推送到您的銷售線索。 在AEM中，您可以根據現有內容創AEM建新聞稿，並添加特定於新聞稿的新內容。
seo-description: E-mail marketing (for example, newsletters) are an important part of any marketing campaign as you use them to push content to your leads. In AEM, you can create newsletters from existing AEM content as well as add new content, specific to the newsletters.
uuid: 565943bf-fe37-4d5c-98c3-7c629c4ba264
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 69ca5acb-83f9-4e1b-9639-ec305779c931
docset: aem65
exl-id: a1d8b74e-67eb-4338-9e8e-fd693b1dbd48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 1%

---

# 電子郵件營銷{#e-mail-marketing}

>[!NOTE]
>
>Adobe不打算進一步增強SMTP服務發送的開啟/退貨（無法交付）的電子郵件AEM跟蹤功能。
>建議是 [利用Adobe Campaign和AEM](/help/sites-administering/campaign.md)。

電子郵件營銷（例如，新聞稿）是任何營銷活動的重要部分，因為您使用它們將內容推送到您的銷售線索。 在AEM中，您可以根據現有內容創AEM建新聞稿，並添加特定於新聞稿的新內容。

建立後，您可以立即或在其他預定時間（通過使用工作流）將新聞通訊發送給特定的用戶組。 此外，用戶可以按自己選擇的格式訂閱新聞稿。

此外，還AEM允許您管理新聞稿功能，包括維護主題、歸檔新聞稿和查看新聞稿統計資訊。

>[!NOTE]
>
>在Geometrixx中，新聞稿模板會自動開啟電子郵件編輯器。 您可以將電子郵件編輯器用於其他要在其中發送電子郵件的模板，例如邀請。 每當從繼承頁面時，電子郵件編輯器都會顯示 **mcm/元件/新聞稿/頁**。

本文檔介紹了在中建立新聞稿的基AEM礎。 有關如何處理電子郵件營銷的更詳細資訊，請參閱以下文檔：

* [建立有效的新聞簡報登錄頁](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [管理訂閱](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [向電子郵件服務提供商發佈電子郵件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [跟蹤已跳轉的電子郵件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>如果您更新電子郵件提供商、執行航班test或發送新聞稿，則如果新聞稿未首先發佈到「發佈」實例或「發佈」實例不可用，則這些操作將失敗。 請確保發佈新聞簡報，並確保「發佈」實例已啟動並正在運行。

## 建立新聞稿體驗 {#creating-a-newsletter-experience}

>[!NOTE]
>
>電子郵件通知需要通過osgi配置進行配置。 請參閱 [配置電子郵件通知。](/help/sites-administering/notification.md)

1. 在左窗格中選擇新市場活動，或在右窗格中按兩下它。

1. 使用表徵圖選擇清單視圖：

   ![](do-not-localize/mcm_icon_listview-1.png)

1. 按一下 **新建……**

   可以指定 **標題**。 **名稱** 創造的經驗類型，在這種情況下，新聞簡訊。

   ![mcm_createselleter](assets/mcm_createnewsletter.png)

1. 按一下&#x200B;**建立**。

1. 新對話框將立即開啟。 您可以在此處輸入新聞稿的屬性。

   的 **預設收件人清單** 是必填欄位，因為它構成了新聞稿的觸點(請參閱 [使用清單](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists) )的正平方根。

   ![mcm_newellesterdialog](assets/mcm_newnewsletterdialog.png)

   * **從名稱**
應作為新聞稿發件人出現的名稱。

   * **發件人地址**
應作為新聞稿發件人顯示的郵件地址。

   * **主題**
通訊的主題。

   * **答復**
應為已發送的新聞簡報提供答復的郵件地址。

   * **說明**
新聞稿的說明。

   * **準時**
按時發送新聞稿。

   * **預設收件人清單**
應接收新聞稿的預設清單。
   可以在以後從 **屬性……** 對話框。

1. 按一下 **確定** 來保存。

## 將內容添加到新聞稿 {#adding-content-to-newsletters}

您可以像在任何元件中一樣將內容（包括動態內容）添加到新聞AEM稿中。 在Geometrixx中，新聞簡報模板具有某些元件，可用於添加和修改新聞簡報中的內容。

1. 在MCM中，按一下 **市場活動** 頁籤，並按兩下要添加內容或編輯的新聞稿。 新聞稿開始。

1. 如果元件不可見，請轉至「設計」視圖，然後在開始編輯之前啟用必要的元件（例如新聞簡訊元件）。
1. 根據需要輸入任何新文本、影像或其他元件。 在Geometrixx示例中，有4個元件可用：文本、影像、標題和2列。 根據您的設定方式，您的新聞稿可能包含的元件或多或少。

   >[!NOTE]
   >
   >使用變數對新聞稿進行個性化設定。 在Geometrixx新聞簡報中，變數可在文本元件中找到。 變數的值從用戶配置檔案中的資訊中繼承。

   ![mcm_seltrey_content](assets/mcm_newsletter_content.png)

1. 要插入變數，請從清單中選擇變數，然後按一下 **插入**。 變數從「配置檔案」填充。

## 個性化新聞稿 {#personalizing-newsletters}

通過在新聞稿的「文本」元件中插入預定義變數，您可以個性化新聞稿。 變數的值從用戶配置檔案中的資訊中繼承。

您還可以通過使用客戶上下文並載入配置檔案來模擬新聞簡報的個性化方式。

要個性化新聞稿並模擬其外觀：

1. 在MCM中，開啟要自定義設定的新聞稿。

1. 開啟要個性化的文本元件。

1. 將游標置於要顯示變數的位置，然後從下拉清單中選擇變數，然後按一下 **插入**。 根據需要對任意多個變數執行此操作，然後按一下 **確定**。

   ![mcm_seltrey_variables](assets/mcm_newsletter_variables.png)

1. 要模擬變數在發送時的外觀，請按CTRL+ALT+c開啟客戶端上下文並選擇 **載入**。 從要載入其配置檔案的清單中選擇用戶，然後按一下 **確定**。

   您載入的配置檔案中的資訊已填充了變數。

   ![mc_seltrest_testvariables](assets/mc_newsletter_testvariables.png)

## 在不同的電子郵件客戶端中測試新聞稿 {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>在發送新聞稿之前，請在以下位置檢查第一天CQ連結外部化程式的OSGi配置 `https://localhost:4502/system/console/configMgr`。
>
>預設情況下，參數的值為 `localhost:4502` 如果運行實例的埠已更改，則操作無法完成。

在常用的電子郵件用戶端之間切換，可查看銷售機會端所看到的 Newsletter 外觀。預設情況下，您的新聞稿在未選擇任何電子郵件客戶端的情況下開啟。

目前，您可以在以下電子郵件客戶端中查看新聞稿：

* 雅虎郵件
* Gmail
* Hotmail
* Thunderbird
* Microsoft2007展望
* Apple郵報

要在客戶端之間切換，請按一下相應表徵圖查看該電子郵件客戶端中的新聞稿：

1. 在MCM中，開啟要自定義設定的新聞稿。

1. 按一下頂欄中的電子郵件客戶端，查看該客戶端中的新聞稿。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 對要查看的任何其他電子郵件客戶端重複此步驟。

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 自定義新聞稿設定 {#customizing-newsletter-settings}

儘管只有授權用戶才能發送新聞稿，但您應自定義以下內容：

* 主題行，以便用戶希望開啟您的電子郵件，同時確保您的新聞稿不會最終被標籤為垃圾郵件。
* 「發件人」地址(例如noreply@geometrixx.com)，以便用戶從指定的地址接收電子郵件。

要自定義新聞稿設定，請執行以下操作：

1. 在MCM中，開啟要自定義設定的新聞稿。

   ![mcm_selletter_open](assets/mcm_newsletter_open.png)

1. 在新聞稿的頂部，按一下 **設定**。

   ![mcm_seltrey_settings](assets/mcm_newsletter_settings.png)
1. 輸入 **從** 電子郵件地址

1. 修改 **主題** 必要時。

1. 選擇 **預設收件人清單** 清單中。

1. 按一下&#x200B;**「確定」**。

   當您test或發送新聞稿時，收件人將收到具有指定電子郵件地址和主題的電子郵件。

## 飛行測試通訊 {#flight-testing-newsletters}

雖然飛行測試不是強制性的，但在您發送新聞稿之前，您可能需要test它以確保它看起來是您希望的。

飛行測試允許您執行以下操作：

* 查看中的新聞稿 [所有目標客戶](#testing-newsletters-in-different-e-mail-clients)。
* 驗證郵件伺服器設定是否正確。
* 確定電子郵件是否被標籤為垃圾郵件。 （確保將您自己包括在收件人清單中。）

>[!NOTE]
>
>如果您更新電子郵件提供商、執行航班test或發送新聞稿，則如果新聞稿未首先發佈到「發佈」實例或「發佈」實例不可用，則這些操作將失敗。 請確保發佈新聞簡報，並確保「發佈」實例已啟動並正在運行。

航班test通訊：

1. 從MCM開啟要test和發送的通訊。

1. 在新聞稿的頂部，按一下 **Test** 在發送前test。

   ![mcm_seltrey_testsettings](assets/mcm_newsletter_testsettings.png)

1. 輸入要發送新聞稿的test郵件地址，然後按一下 **發送**。 如果要更改配置檔案，請在客戶端上下文中載入另一個配置檔案。 通過按CTRL+ALT+c並選取「載入」(Load)和載入輪廓，可以執行此操作。

## 正在發送新聞稿 {#sending-newsletters}

>[!NOTE]
>
>Adobe不打算進一步增強SMTP服務發送的開啟/退貨（無法交付）的電子郵件AEM跟蹤功能。
>建議是 [利用Adobe Campaign和AEM](/help/sites-administering/campaign.md)。

您可以從新聞稿或清單中發送新聞稿。 描述了兩個過程。

>[!NOTE]
>
>在發送新聞稿之前，請在以下位置檢查第一天CQ連結外部化程式的OSGi配置 `https://localhost:4502/system/console/configMgr`。
>
>預設情況下，參數的值為 `localhost:4502` 如果運行實例的埠已更改，則操作無法完成。

>[!NOTE]
>
>如果您更新電子郵件提供商、執行航班test或發送新聞稿，則如果新聞稿未首先發佈到「發佈」實例或「發佈」實例不可用，則這些操作將失敗。 請確保發佈新聞簡報，並確保「發佈」實例已啟動並正在運行。

### 從市場活動發送新聞稿 {#sending-newsletters-from-a-campaign}

要從市場活動中發送新聞稿，請執行以下操作：

1. 從MCM開啟要發送的通訊。

   >[!NOTE]
   >
   >在發送之前，請確保您已按以下方式自定義了新聞稿的主題和來源電子郵件地址 [自定義其設定](#customizing-newsletter-settings)。
   >
   >
   >[試飛](#flight-testing-newsletters) 建議在發送前先發送新聞稿。

1. 在新聞稿的頂部，按一下 **發送**。 將開啟新聞簡報嚮導。

1. 在收件人清單中，選擇要接收新聞稿的清單，然後按一下 **下一個**。

   ![mcm_ellestersend](assets/mcm_newslettersend.png)

1. 已確認安裝完成。 按一下 **發送** 才能真正發通訊。

   ![mcm_extlestrysendconfirm](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >確保您是收件人之一，以確保收到新聞稿。

### 從清單發送新聞稿 {#sending-newsletters-from-a-list}

要從清單中發送新聞稿，請執行以下操作：

1. 在MCM中，按一下 **清單** 的下界。

   >[!NOTE]
   >
   >在發送之前，請確保您已按以下方式自定義了新聞稿的主題和來源電子郵件地址 [自定義其設定](#customizing-newsletter-settings)。 如果您從清單中發送新聞稿，則無法test;你 [飛行test](#flight-testing-newsletters) 如果你從新聞稿上寄來。

1. 選中要向其發送新聞稿的銷售線索清單旁邊的複選框。

1. 在 **工具** 菜單，選擇 **發送新聞稿**。 的 **發送新聞稿** 的下界。

   ![mcm_ellesttersendfromlist](assets/mcm_newslettersendfromlist.png)

1. 在 **新聞稿** 欄位，選擇要發送的新聞稿，然後按一下 **下一個**。

   ![mcm_ellestersenddialog](assets/mcm_newslettersenddialog.png)

1. 已確認安裝完成。 按一下 **發送** 將選定的新聞稿發送到指定的銷售線索清單。

   ![mcm_esslettersenddialog_confirmation](assets/mcm_newslettersenddialog_confirmation.png)

   您的新聞稿將發送給選定的收件人。

## 訂閱新聞簡報 {#subscribing-to-a-newsletter}

本節介紹如何訂閱新聞簡報。

### 訂閱新聞簡報 {#subscribing-to-a-newsletter-1}

要訂閱新聞簡報(以Geometrixx網站為例):

1. 按一下 **網站** 導航到Geometrixx **工具欄** 開啟它。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 在Geometrixx通訊中 **註冊** 欄位，然後按一下 **註冊**。 您現在訂閱了新聞稿。
