---
title: 為行動裝置製作頁面
seo-title: 為行動裝置製作頁面
description: 製作行動頁面時，頁面的顯示方式會模擬行動裝置。 編寫頁面時，您可以在多個模擬器之間切換，以查看使用者在存取頁面時所看到的內容。
seo-description: 製作行動頁面時，頁面的顯示方式會模擬行動裝置。 編寫頁面時，您可以在多個模擬器之間切換，以查看使用者在存取頁面時所看到的內容。
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 為行動裝置製作頁面{#authoring-a-page-for-mobile-devices}

製作行動頁面時，頁面的顯示方式會模擬行動裝置。 編寫頁面時，您可以在多個模擬器之間切換，以查看使用者在存取頁面時所看到的內容。

裝置會根據裝置呈現頁面的功能，分組為類別功能、智慧型和觸控。 當使用者存取行動頁面時，AEM會偵測裝置並傳送與其裝置群組對應的表示法。

>[!NOTE]
>
>若要根據現有標準網站建立行動網站，請建立標準網站的即時副本。 （請參閱[為不同通道建立即時副本](/help/sites-administering/msm-livecopy.md)。）
>
>AEM開發人員可以建立新裝置群組。 （請參閱[建立設備組篩選器。](/help/sites-developing/groupfilters.md)）

請依照下列程式製作行動頁面：

1. 在瀏覽器中，前往&#x200B;**Siteadmin**&#x200B;主控台。
1. 開啟&#x200B;**Products**&#x200B;頁面，位於&#x200B;**Websites** >> **Geometrixx行動示範網站** >> **English**&#x200B;下。

1. 切換至其他模擬器。 若要這麼做，您可以：

   * 按一下頁面頂端的裝置圖示。
   * 按一下&#x200B;**Sidekick**&#x200B;中的&#x200B;**編輯**&#x200B;按鈕，然後在下拉式功能表中選取裝置。

1. 將&#x200B;**Text &amp; Image**&#x200B;元件從Sidekick的「行動」標籤拖放至頁面。
1. 編輯元件並新增一些文字。 按一下&#x200B;**OK**&#x200B;以儲存變更。

頁面外觀與下列相同：

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>當從行動裝置要求製作執行個體上的頁面時，模擬器會停用。 接著，您就可以使用觸控式UI來完成編寫。
