---
title: 產品摘要
seo-title: 產品摘要
description: 瞭解AEM產品摘要。
seo-description: 瞭解AEM產品摘要。
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Product Feed {#product-feed}

AEM與 [Search&amp;Promote整合](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html) ，可讓您：

* 使用eCommerce API，獨立於基礎資料庫結構和商務平台。
* 運用Search&amp;Promote的「索引連接器」功能，以XML格式提供產品饋送。
* 運用Search&amp;Promote的「遠端控制」功能，執行產品饋送的隨選或排程要求
* 不同Search&amp;Promote帳戶的動態消息產生，設定為雲端服務設定。

您必須擁有有效帳戶，並 [設定與Search&amp;Promote的連線](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote)。 您還必須驗證您使用的資料中 [心](/help/sites-administering/search-and-promote.md#configuring-the-data-center) ，並確保已配置**Remote伺服器URI **。

## 設定產品摘要 {#set-up-the-product-feed}

您必須先輸入網站根目錄和識別碼屬性。 要執行此操作：

1. 導覽至您的Search&amp;Promote設定。
1. 按一 **[!UICONTROL 下編輯]**。
1. 按一下「索 **[!UICONTROL 引連接器饋送設定]** 」標籤。
1. 輸入「 **[!UICONTROL Web站點根目錄]** 」和「 **[!UICONTROL 標識符」屬性]**。

   >[!NOTE]
   >
   >例 **[!UICONTROL 如]** ，網站根目錄是您電子商務網站的根目錄 `/content/geometrixx-outdoors/en`。
   >
   >Identifier屬 **[!UICONTROL 性是]** JCR屬性，可唯一識別產品： `identifier`。

1. 按一下 **[!UICONTROL 確定]**。

然後，您也必須先在Web主控台中編輯兩個設定，才能產生產品饋送。

### 為Geometrixx設定Day CQ Search&amp;Promote產品Crawler實作 {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. 導覽至 [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 按一 **[!UICONTROL 下Geometrixx的Day CQ Search&amp;Promote產品Crawler實作]**。
1. 指定此Crawler所連結的Search&amp;Promote帳戶號碼。 它將用於查找此Crawler使用的雲服務配置。
1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

### 為Geometrixx設定Day CQ Search&amp;Promote產品摘要產生器 {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. 導覽至 [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 按一 **[!UICONTROL 下Geometrixx的Day CQ Search&amp;Promote產品饋送產生器]**。
1. 指定此產生器所連結的Search&amp;Promote帳戶號碼。 它將用於查找此生成器使用的雲服務配置。
1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

## 排程產品摘要 {#schedule-the-product-feed}

若要啟用排程的動態消息產生，您必須為其設定排程器。
排程器會設定為您特定Search&amp;Promote雲端服務設定的子項設定。

1. 導覽至您的Search&amp;Promote設定。
1. 按一下「 **[!UICONTROL Scheduler configuration]** (計畫程式配 **[!UICONTROL 置)」旁邊的+]**。
1. 輸入頁 **[!UICONTROL 面作者]** 可辨識的標題和唯一 **[!UICONTROL 名稱]**。
1. 按一下&#x200B;**[!UICONTROL 「建立」]**。對話方塊隨即開啟。

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. 輸入「 **[!UICONTROL Remote Control Password（遠程控制密碼）]**」。 這是您在Search&amp;Pronote帳戶中設定的密碼。

   >[!NOTE]
   >
   >這不是您Search&amp;Promote帳戶的密碼。 您可以登入您的Search&amp;Promote帳戶並前往索引，然後前往遠端控制項，以尋找並變 **[!UICONTROL 更此密]** 碼 ****。

1. 選中 **[!UICONTROL 啟用計畫]** 框。
1. 選擇一個 **[!UICONTROL 計畫]**。 這是實際的動態消息產生排程。
1. 啟用 **[!UICONTROL 隨選索引]** 。 此功能可用來手動呼叫Search&amp;Promote索引。 如果 **[!UICONTROL 勾選「請求完整產品饋送]** 」,Search&amp;Promote將會請求完整的產品饋送。 否則，會要求增量產品饋送。

   >[!NOTE]
   >
   >隨選索引功能可運用Search&amp;Promote的「遠端控制」功能。 呼叫遠端索引時，索引不會立即啟動，但會使用遠端控制功能將索引請求張貼至Search&amp;Promote。

1. 按一下 **[!UICONTROL 確定]**。

現在，您已設定好所有項目，所以可以看到XML頁面，其中包含所設定網站根目錄下的所有產品： [http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full)。
