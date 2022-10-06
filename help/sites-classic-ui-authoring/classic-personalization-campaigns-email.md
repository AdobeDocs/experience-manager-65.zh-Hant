---
title: 電子郵件行銷
seo-title: E-mail Marketing
description: 電子郵件行銷（例如，電子報）是任何行銷活動的重要部分，因為您使用這些行銷活動將內容推送至銷售機會。 在AEM中，您可以從現有的AEM內容建立電子報，並新增電子報專屬的新內容。
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

# 電子郵件行銷{#e-mail-marketing}

>[!NOTE]
>
>Adobe不打算進一步加強AEM SMTP服務所傳送之開啟/退信（無法傳送）的電子郵件追蹤。
>建議為 [運用Adobe Campaign及與AEM的整合](/help/sites-administering/campaign.md).

電子郵件行銷（例如，電子報）是任何行銷活動的重要部分，因為您使用這些行銷活動將內容推送至銷售機會。 在AEM中，您可以從現有的AEM內容建立電子報，並新增電子報專屬的新內容。

建立後，您可以立即或在其他排程時間（透過使用工作流程）將電子報傳送給特定使用者群組。 此外，使用者可以選擇的格式訂閱電子報。

此外，AEM還讓您管理電子報功能，包括維護主題、封存電子報和檢視電子報統計資料。

>[!NOTE]
>
>在Geometrixx中，電子報範本會自動開啟電子郵件編輯器。 您可以在其他要傳送電子郵件的範本（例如，邀請）中使用電子郵件編輯器。 每當頁面繼承自 **mcm/components/電子報/page**.

本檔案說明在AEM中建立電子報的基本知識。 有關如何使用電子郵件行銷的更多詳細資訊，請參閱以下文檔：

* [建立有效的電子報登陸頁面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [管理訂閱](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [向電子郵件服務提供者發佈電子郵件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [追蹤跳出的電子郵件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>如果您更新電子郵件提供者、進行飛行測試或傳送電子報，如果電子報未先發佈至「發佈」執行個體，或者「發佈」執行個體無法使用，則這些操作會失敗。 請務必發佈電子報，並確認Publish執行個體已開啟並執行。

## 建立電子報體驗 {#creating-a-newsletter-experience}

>[!NOTE]
>
>電子郵件通知需透過osgi設定來設定。 請參閱 [設定電子郵件通知。](/help/sites-administering/notification.md)

1. 在左窗格中選取新促銷活動，或在右窗格中按兩下它。

1. 使用圖示選取清單檢視：

   ![](do-not-localize/mcm_icon_listview-1.png)

1. 按一下 **新……**

   您可以指定 **標題**, **名稱** 和要建立的體驗類型；在此情況下，請參閱電子報。

   ![mcm_createnewsletter](assets/mcm_createnewsletter.png)

1. 按一下&#x200B;**建立**。

1. 新對話方塊將立即開啟。 您可以在此輸入電子報的屬性。

   此 **預設收件者清單** 是必填欄位，因為這會形成電子報的接觸點(請參閱 [使用清單](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists) 以取得清單的詳細資訊)。

   ![mcm_newnewsletterdialog](assets/mcm_newnewsletterdialog.png)

   * **從名稱**
應顯示為電子報寄件者的名稱。

   * **寄件者地址**
應顯示為電子報寄件者的郵件地址。

   * **主旨**
電子報的主題。

   * **回覆**
應處理已傳送電子報回覆的郵件地址。

   * **說明**
電子報說明。

   * **準時**
傳送電子報的準時。

   * **預設收件者清單**
應接收電子報的預設清單。
   稍後可從 **屬性……** 對話框。

1. 按一下 **確定** 儲存。

## 將內容新增至電子報 {#adding-content-to-newsletters}

您可以像在任何AEM元件中一樣，將內容（包括動態內容）新增至電子報。 在Geometrixx中，電子報範本有某些元件可用來新增和修改電子報中的內容。

1. 在MCM中，按一下 **行銷活動** 標籤，然後按兩下您要新增內容至或編輯的電子報。 電子報開啟。

1. 如果元件不可見，請前往「設計」檢視，並在您開始編輯前啟用必要的元件（例如電子報元件）。
1. 視情況輸入任何新文字、影像或其他元件。 在Geometrixx範例中，有4個元件可供使用：文字、影像、標題和2欄。 根據您的設定方式，電子報的元件可能會多或少。

   >[!NOTE]
   >
   >您使用變數來個人化電子報。 在Geometrixx電子報中，變數可在文字元件中使用。 變數的值繼承自使用者設定檔中的資訊。

   ![mcm_newsletter_content](assets/mcm_newsletter_content.png)

1. 若要插入變數，請從清單中選取變數，然後按一下 **插入**. 變數會從設定檔填入。

## 個人化電子報 {#personalizing-newsletters}

您可以在電子報的Text元件中插入預先定義的變數，以個人化電子報Geometrixx。 變數的值繼承自使用者設定檔中的資訊。

您也可以使用用戶端內容並載入設定檔，模擬電子報的個人化方式。

若要個人化電子報並模擬其外觀：

1. 從MCM開啟要自定義設定的電子報。

1. 開啟您要個人化的文字元件。

1. 將游標置於您希望變數顯示的位置，然後從下拉式清單中選取變數，然後按一下 **插入**. 視需要對變數執行此動作，然後按一下 **確定**.

   ![mcm_newsletter_variables](assets/mcm_newsletter_variables.png)

1. 若要模擬變數在傳送時的外觀，請按CTRL+ALT+c以開啟用戶端內容並選取 **載入**. 從您要載入其設定檔的清單中選取使用者，然後按一下 **確定**.

   您載入之設定檔的資訊已填入變數。

   ![mc_newsletter_testvariables](assets/mc_newsletter_testvariables.png)

## 在不同的電子郵件客戶端中測試電子報 {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>傳送電子報之前，請先檢查Day CQ Link Externalizer的OSGi設定() `https://localhost:4502/system/console/configMgr`.
>
>依預設，參數的值為 `localhost:4502` 如果已更改運行實例的埠，則無法完成和操作。

在常用的電子郵件用戶端之間切換，可查看銷售機會端所看到的 Newsletter 外觀。依預設，您的電子報會開啟，且未選取任何電子郵件用戶端。

目前，您可以在以下電子郵件客戶端中查看電子報：

* Yahoo郵件
* Gmail
* Hotmail
* Thunderbird
* Microsoft2007展望
* Apple Mail

若要在用戶端之間切換，請按一下對應的圖示，以檢視該電子郵件用戶端中的電子報：

1. 從MCM開啟要自定義設定的電子報。

1. 按一下頂端列中的電子郵件用戶端，查看該用戶端中的電子報外觀。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 對您要查看的任何其他電子郵件客戶端重複此步驟。

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 自訂電子報設定 {#customizing-newsletter-settings}

雖然只有授權的使用者可以傳送電子報，但您應自訂下列內容：

* 主旨行，讓使用者可以開啟您的電子郵件，同時確保電子報最後不會標示為垃圾訊息。
* 寄件者地址，例如noreply@geometrixx.com，讓使用者從指定的位址接收電子郵件。

若要自訂電子報設定：

1. 從MCM開啟要自定義設定的電子報。

   ![mcm_newsletter_open](assets/mcm_newsletter_open.png)

1. 在電子報頂端，按一下 **設定**.

   ![mcm_newsletter_settings](assets/mcm_newsletter_settings.png)
1. 輸入 **從** 電子郵件地址

1. 修改 **主旨** （如有必要）。

1. 選取 **預設收件者清單** 從下拉式清單中。

1. 按一下&#x200B;**「確定」**。

   當您測試或傳送電子報時，收件者會收到包含指定電子郵件地址和主旨的電子郵件。

## 飛行測試快訊 {#flight-testing-newsletters}

雖然飛行測試並非強制性，但在您發送電子報之前，您可能想要加以測試，以確保它以您想要的方式顯示。

飛行測試可讓您執行下列操作：

* 查看以下位置的電子報： [所有預期客戶](#testing-newsletters-in-different-e-mail-clients).
* 驗證郵件伺服器設定正確。
* 判斷您的電子郵件是否被標示為垃圾訊息。 （請務必將自己納入收件者清單中。）

>[!NOTE]
>
>如果您更新電子郵件提供者、進行飛行測試或傳送電子報，如果電子報未先發佈至「發佈」執行個體，或者「發佈」執行個體無法使用，則這些操作會失敗。 請務必發佈電子報，並確認Publish執行個體已開啟並執行。

要飛行測試快訊：

1. 在MCM中，開啟您要測試並傳送的電子報。

1. 在電子報頂端，按一下 **測試** 以在傳送前進行測試。

   ![mcm_newsletter_testsettings](assets/mcm_newsletter_testsettings.png)

1. 輸入要發送電子報的測試郵件地址，然後按一下 **傳送**. 如果要變更設定檔，請在用戶端內容中載入另一個設定檔。 要執行此操作，請按CTRL+ALT+c並選取「載入」並載入設定檔。

## 傳送電子報 {#sending-newsletters}

>[!NOTE]
>
>Adobe不打算進一步加強AEM SMTP服務所傳送之開啟/退信（無法傳送）的電子郵件追蹤。
>建議為 [運用Adobe Campaign及與AEM的整合](/help/sites-administering/campaign.md).

您可以從電子報或清單中傳送電子報。 描述了兩個過程。

>[!NOTE]
>
>傳送電子報之前，請先檢查Day CQ Link Externalizer的OSGi設定() `https://localhost:4502/system/console/configMgr`.
>
>依預設，參數的值為 `localhost:4502` 如果已更改運行實例的埠，則無法完成和操作。

>[!NOTE]
>
>如果您更新電子郵件提供者、進行飛行測試或傳送電子報，如果電子報未先發佈至「發佈」執行個體，或者「發佈」執行個體無法使用，則這些操作會失敗。 請務必發佈電子報，並確認Publish執行個體已開啟並執行。

### 從行銷活動傳送電子報 {#sending-newsletters-from-a-campaign}

若要從行銷活動內傳送電子報：

1. 在MCM中，開啟您要發送的電子報。

   >[!NOTE]
   >
   >在傳出之前，請確定您已自訂電子報的主旨，以及寄出的電子郵件地址(依 [自訂其設定](#customizing-newsletter-settings).
   >
   >
   >[飛行測試](#flight-testing-newsletters) 建議您先閱讀電子報再傳送。

1. 在電子報頂端，按一下 **傳送**. 電子報精靈隨即開啟。

1. 在收件者清單中，選取您要接收電子報的清單，然後按一下 **下一個**.

   ![mcm_newslettersend](assets/mcm_newslettersend.png)

1. 已確認安裝完成。 按一下 **傳送** 寄電子報。

   ![mcm_newslettersendconfirm](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >請確定您是其中一位收件者，以確保收到電子報。

### 從清單傳送電子報 {#sending-newsletters-from-a-list}

若要從清單傳送電子報：

1. 在MCM中，按一下 **清單** 在左側窗格中。

   >[!NOTE]
   >
   >在傳出之前，請確定您已自訂電子報的主旨，以及寄出的電子郵件地址(依 [自訂其設定](#customizing-newsletter-settings). 如果您從清單中傳送電子報，則無法測試電子報；您可以 [飛行試驗](#flight-testing-newsletters) 如果您從電子報傳送。

1. 選取您要傳送電子報的銷售機會清單旁的核取方塊。

1. 在 **工具** 菜單，選擇 **傳送電子報**. 此 **傳送電子報** 窗口。

   ![mcm_newslettersendfromlist](assets/mcm_newslettersendfromlist.png)

1. 在 **電子報** 欄位中，選取您要傳送的電子報，然後按一下 **下一個**.

   ![mcm_newslettersenddialog](assets/mcm_newslettersenddialog.png)

1. 已確認安裝完成。 按一下 **傳送** 將所選電子報發送到指定的銷售機會清單。

   ![mcm_newslettersenddialog_confirmation](assets/mcm_newslettersenddialog_confirmation.png)

   您的電子報會傳送給選取的收件者。

## 訂閱電子報 {#subscribing-to-a-newsletter}

本節說明如何訂閱電子報。

### 訂閱電子報 {#subscribing-to-a-newsletter-1}

若要訂閱電子報(以Geometrixx網站為例):

1. 按一下 **網站** 並導覽至Geometrixx **工具列** 然後開啟它。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 在Geometrixx電子報中 **註冊** 欄位，輸入您的電子郵件地址，然後按一下 **註冊**. 您現在已訂閱電子報。
