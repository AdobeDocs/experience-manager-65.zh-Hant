---
title: 製作行動裝置的頁面
seo-title: 製作行動裝置的頁面
description: 製作行動頁面時，頁面的顯示方式會模擬行動裝置。 在編寫頁面時，您可以在多個模擬器之間切換，以查看使用者在存取頁面時看到的內容。
seo-description: 製作行動頁面時，頁面的顯示方式會模擬行動裝置。 在編寫頁面時，您可以在多個模擬器之間切換，以查看使用者在存取頁面時看到的內容。
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 製作行動裝置的頁面{#authoring-a-page-for-mobile-devices}

製作行動頁面時，頁面的顯示方式會模擬行動裝置。 在編寫頁面時，您可以在多個模擬器之間切換，以查看使用者在存取頁面時看到的內容。

裝置會根據裝置的功能，分組為類別功能、智慧型和觸控，以呈現頁面。 當使用者存取行動頁面時，AEM會偵測裝置並傳送對應其裝置群組的表示法。

>[!NOTE]
>
>若要根據現有的標準網站建立行動網站，請建立標準網站的即時副本。 (請參 [閱「建立不同渠道的即時副本](/help/sites-administering/msm-livecopy.md)」)。
>
>AEM開發人員可以建立新的裝置群組。 (請參 [閱建立裝置群組篩選器](/help/sites-developing/groupfilters.md))。

請依照下列程式來製作行動頁面：

1. 在您的瀏覽器中，前往網 **站管理** 主控台。
1. 開啟「 **Websites** >> **Geometrixx Mobile Demo Site** > **English」(網站>>Geometrixx行動展示網站** >英文)下 ****&#x200B;的「Products」（產品）頁面。

1. 切換至不同的模擬器。 若要這麼做，您可以：

   * 按一下頁面頂端的裝置圖示。
   * 按一 **下Sidekick中的Edit** （編輯） **按鈕** ，然後在下拉式選單中選取裝置。

1. 將Text &amp; Image **** 元件從Sidekick的Mobile標籤拖放至頁面。
1. 編輯元件並新增一些文字。 按一下 **確定** ，保存更改。

頁面外觀與下列相同：

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>當從行動裝置請求作者實例上的頁面時，模擬器被禁用。 然後，您就可使用觸控式UI來製作內容。

