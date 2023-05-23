---
title: 為移動設備創作頁面
description: 當創作移動頁面時，以模擬移動設備的方式顯示頁面。 創作頁面時，可以在多個模擬器之間切換以查看最終用戶在訪問頁面時看到的內容。
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 為移動設備創作頁面{#authoring-a-page-for-mobile-devices}

當創作移動頁面時，以模擬移動設備的方式顯示頁面。 創作頁面時，可以在多個模擬器之間切換以查看最終用戶在訪問頁面時看到的內容。

根據設備的功能將設備分組到類別特徵、智慧和觸摸以呈現頁面。 當終端用戶訪問移動頁面時，AEM檢測設備併發送對應於其設備組的表示。

>[!NOTE]
>
>要基於現有標準站點建立移動站點，請建立標準站點的即時副本。 (請參閱 [為不同渠道建立即時拷貝](/help/sites-administering/msm-livecopy.md)。)
>
>開AEM發人員可以建立新設備組。 (請參閱 [建立設備組篩選器。](/help/sites-developing/groupfilters.md))

請按下列步驟編寫移動頁面：

1. 在瀏覽器中，轉到 **站點管理** 控制台。
1. 開啟 **產品** 頁 **網站** > **Geometrixx移動演示網站** > **英語**。

1. 切換到其他模擬器。 為此，您可以：

   * 按一下頁面頂部的設備表徵圖。
   * 按一下 **編輯** 按鈕 **側腳** 並在下拉菜單中選擇設備。

1. 拖放 **文本和影像** 從Sidek的Mobile頁籤到頁面的元件。
1. 編輯元件並添加一些文本。 按一下 **確定** 的子菜單。

該頁面與以下內容相同：

![行動電話](assets/mobileipademu.png)

>[!NOTE]
>
>當從移動設備請求作者實例上的頁面時，模擬器被禁用。 然後，可以使用啟用觸摸的UI完成創作。
