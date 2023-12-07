---
title: 為行動裝置編寫頁面
description: 編寫行動頁面時，頁面會以模擬行動裝置的方式顯示。 編寫頁面時，您可以在多個模擬器之間切換，以檢視一般使用者在存取頁面時看到的內容。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 為行動裝置編寫頁面{#authoring-a-page-for-mobile-devices}

編寫行動頁面時，頁面會以模擬行動裝置的方式顯示。 編寫頁面時，您可以在多個模擬器之間切換，以檢視一般使用者在存取頁面時看到的內容。

系統會根據裝置轉譯頁面的功能，將裝置分組為類別功能、智慧型和觸控。 當一般使用者存取行動頁面時，AEM會偵測裝置並傳送與其裝置群組相對應的表示。

>[!NOTE]
>
>若要根據現有標準網站建立行動網站，請建立標準網站的即時副本。 (請參閱 [建立不同頻道的即時副本](/help/sites-administering/msm-livecopy.md).)
>
>AEM開發人員可以建立新的裝置群組。 (請參閱 [正在建立裝置群組篩選器。](/help/sites-developing/groupfilters.md))

請使用下列程式來編寫行動頁面：

1. 在瀏覽器中，前往 **Siteadmin** 主控台。
1. 開啟 **產品** 下方頁面 **網站** >> **Geometrixx Mobile示範網站** >> **英文**.

1. 切換到不同的模擬器。 若要這麼做，您可以：

   * 按一下頁面頂端的裝置圖示。
   * 按一下 **編輯** 中的按鈕 **Sidekick** ，然後在下拉式選單中選取裝置。

1. 拖放 **文字與影像** 元件從頁面Sidekick的「行動」標籤進入。
1. 編輯元件並新增一些文字。 按一下 **確定** 以儲存變更。

此頁面看起來與以下專案相同：

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>從行動裝置請求製作執行個體上的頁面時，會停用模擬器。 接著，您就可以使用觸控式UI完成製作。
