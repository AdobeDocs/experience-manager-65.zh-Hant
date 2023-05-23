---
title: We.Retail的全球化網站結構嘗試
seo-title: Trying out the Globalized Site Structure in We.Retail
description: We.Retail的全球化網站結構嘗試
seo-description: null
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
exl-id: e1de20b0-6d7a-4bda-b62f-c2808fd0af28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 2%

---

# We.Retail的全球化網站結構嘗試{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail是利用一個全球化的網站結構建立的，提供一個語言母版，可以即時複製到特定國家的網站。 一切都是現成設定，以便您可以嘗試使用此結構和內置的翻譯功能。

## 嘗試 {#trying-it-out}

1. 從中開啟站點控制台 **全局導航 — >站點**。
1. 切換到列視圖（如果尚未處於活動狀態），然後選擇We.Retail。 請注意與語言碩士課程並列的瑞士、美國、法國等國家的國家結構示例。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. 選擇瑞士並查看該國語言的語言根。 請注意，這些根下面尚無任何內容。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. 切換到清單視圖，查看國家/地區的語言副本都是即時副本。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 返回列視圖，然後按一下「語言母版」，並查看包含內容的語言母版根。 請注意，只有英文包含內容。

   We.Retail不附帶任何翻譯內容，但已準備好結構和配置，讓您能夠演示翻譯服務。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 選擇「英語語言母版」後，開啟 **引用** 在站點控制台中進行連結並選擇 **語言副本**。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 勾選 **語言副本** 標籤以選擇所有語言副本。 在 **更新語言副本** 的 **新建翻譯項目**。 提供項目名稱，然後按一下 **更新**。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 為每個語言翻譯建立一個項目。 在下面查看 **導航 — >項目**。

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 按一下德語查看翻譯項目的詳細資訊。 請注意，狀態為 **草稿**。 要使用Microsoft的翻譯服務啟動翻譯，請按一下 **翻譯作業** 標題和選擇 **開始**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 翻譯項目開始。 按一下卡底部標有「翻譯作業」的省略號，查看詳細資訊。 具有狀態的頁面 **準備審閱** 已被翻譯處翻譯。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 選擇清單中的一個頁面，然後 **在站點中預覽** 的子菜單。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>該過程演示了與Microsoft機器翻譯的內置整合。 使用 [翻譯AEM整合框架](/help/sites-administering/translation.md)，您可以與許多標準翻譯服務整合，以協調翻譯AEM。

## 更多資訊 {#further-information}

有關詳細資訊，請參閱創作文檔 [翻譯多語言站點的內容](/help/sites-administering/translation.md) 詳細技術資訊。
