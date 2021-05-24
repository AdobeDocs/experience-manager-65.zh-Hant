---
title: 產品摘要
seo-title: 產品摘要
description: 了解AEM產品摘要。
seo-description: 了解AEM產品摘要。
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
exl-id: 11a3d636-040a-40bb-ad35-6b8430a81a49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 1%

---

# 產品摘要{#product-feed}

AEM與[Search&amp;Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html)整合，並可讓您：

* 使用eCommerce API，不受基礎存放庫結構和商務平台影響。
* 運用Search&amp;Promote的「索引連接器」功能，以XML格式提供產品摘要。
* 運用Search&amp;Promote的「遠端控制」功能，執行產品摘要的隨選或排程請求
* 不同Search&amp;Promote帳戶的摘要產生（設定為雲端服務設定）。

您需要有有效的帳戶，並且要[配置與Search&amp;Promote](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote)的連接。 您還必須驗證是否使用正確的[資料中心](/help/sites-administering/search-and-promote.md#configuring-the-data-center)，並確保已配置**Remote伺服器URI **。

## 設定產品摘要{#set-up-the-product-feed}

您必須先輸入網站根目錄和識別碼屬性。 要執行此操作：

1. 導覽至您的Search&amp;Promote設定。
1. 按一下「**[!UICONTROL 編輯]**」。
1. 按一下「**[!UICONTROL 索引連接器摘要設定]**」標籤。
1. 輸入&#x200B;**[!UICONTROL 網站根]**&#x200B;和&#x200B;**[!UICONTROL 標識符屬性]**。

   >[!NOTE]
   >
   >**[!UICONTROL 網站根]**&#x200B;是電子商務網站的根，例如`/content/geometrixx-outdoors/en`。
   >
   >**[!UICONTROL Identifier屬性]**&#x200B;是可唯一識別產品的JCR屬性：`identifier`。

1. 按一下&#x200B;**[!UICONTROL 「確定」]**。

然後，您也必須在Web主控台中編輯兩個設定，才能產生產品摘要。

### 為Geometrixx{#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}配置Day CQSearch&amp;Promote產品Crawler實施

1. 導覽至[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 按一下&#x200B;**[!UICONTROL 針對Geometrixx]**&#x200B;的Day CQSearch&amp;Promote產品編目程式實作。
1. 指定此Crawler連結的Search&amp;Promote帳號。 它將用於查找此Crawler使用的雲服務配置。
1. 按一下「**[!UICONTROL 儲存]**」。

### 為Geometrixx{#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}設定Day CQSearch&amp;Promote產品摘要產生器

1. 導覽至[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 按一下&#x200B;**[!UICONTROL Geometrixx]**&#x200B;的Day CQSearch&amp;Promote產品摘要產生器。
1. 指定此生成器連結的Search&amp;Promote帳號。 它將用於查找此生成器使用的雲服務配置。
1. 按一下「**[!UICONTROL 儲存]**」。

## 排程產品摘要{#schedule-the-product-feed}

若要啟用排程摘要產生，您必須為其設定排程器。
排程器會設定為您特定Search&amp;Promote雲端服務設定的子設定。

1. 導覽至您的Search&amp;Promote設定。
1. 按一下&#x200B;**[!UICONTROL 排程器配置]**&#x200B;旁的&#x200B;**[!UICONTROL +]**。
1. 輸入頁面作者可辨識的&#x200B;**[!UICONTROL Title]**，以及唯一的&#x200B;**[!UICONTROL Name]**。
1. 按一下&#x200B;**[!UICONTROL 建立]**。對話方塊隨即開啟。

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. 輸入&#x200B;**[!UICONTROL 遠程控制密碼]**。 這是您在Search&amp;Pronote帳戶中設定的密碼。

   >[!NOTE]
   >
   >這不是您Search&amp;Promote帳戶的密碼。 您可以登入Search&amp;Promote帳戶，然後前往&#x200B;**[!UICONTROL Index]**，然後前往&#x200B;**[!UICONTROL Remote control]**，找到並更改此密碼。

1. 選中&#x200B;**[!UICONTROL 啟用調度]**&#x200B;框。
1. 選擇&#x200B;**[!UICONTROL Schedule]**。 這是實際的摘要產生排程。
1. 啟用或不啟用&#x200B;**[!UICONTROL 按需索引]**。 此功能可用來手動呼叫Search&amp;Promote索引。 如果勾選「**[!UICONTROL 要求完整產品摘要]**」 ,Search&amp;Promote會要求完整產品摘要。 否則，會要求增量產品摘要。

   >[!NOTE]
   >
   >按需索引功能利用了Search&amp;Promote的遠程控制功能。 調用遠程索引時，索引不會立即啟動，但將使用遠程控制功能向Search&amp;Promote發佈索引請求。

1. 按一下&#x200B;**[!UICONTROL 「確定」]**。

現在您已配置了所有內容，您可以看到一個XML頁，其中包含配置的網站根目錄下的所有產品：[http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full)。
