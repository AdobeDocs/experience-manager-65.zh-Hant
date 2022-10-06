---
title: 在We.Retail中嘗試全球化網站結構
seo-title: Trying out the Globalized Site Structure in We.Retail
description: 在We.Retail中嘗試全球化網站結構
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
ht-degree: 0%

---

# 在We.Retail中嘗試全球化網站結構{#trying-out-the-globalized-site-structure-in-we-retail}

We.Retail已透過全球化網站結構建立，提供可即時複製至特定國家/地區網站的語言主版。 一切皆已設定為現成可用，讓您可以試用此結構和內建的翻譯功能。

## 試試 {#trying-it-out}

1. 從開啟網站主控台 **全局導航 — >站點**.
1. 切換至欄檢視（如果尚未啟用），然後選取We.Retail。 請注意與瑞士、美國、法國等國一起沿著語言母版一起建立的國家結構範例。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. 選擇瑞士，並查看該國語言的語言根源。 請注意，這些根底下尚未有任何內容。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. 切換至清單檢視，查看國家/地區的語言副本均為即時副本。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 返回列視圖，然後按一下「語言主版」，查看包含內容的語言主根。 請注意，只有英文有內容。

   We.Retail不提供任何翻譯內容，但已建立結構和配置，允許您演示翻譯服務。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 在選取「英文語言主版」後，開啟 **參考** 在sites控制台中邊欄，並選取 **語言副本**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 勾選 **語言副本** 標籤以選擇所有語言副本。 在 **更新語言副本** ，選取 **建立新的翻譯專案**. 提供專案的名稱，然後按一下 **更新**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 系統會為每個語言翻譯建立專案。 在下方檢視 **導覽 — >專案**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 按一下德文查看翻譯項目的詳細資訊。 請注意，狀態為 **草稿**. 若要使用Microsoft的翻譯服務開始翻譯，請按一下 **翻譯工作** 標題和選取 **開始**.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 翻譯專案隨即開始。 按一下卡底部標示為「翻譯工作」的刪節號，查看詳細資訊。 狀態為的頁面 **準備審核** 已經由翻譯處翻譯。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 在清單中選取其中一個頁面，然後 **在網站中預覽** 在工具列中，開啟頁面編輯器中翻譯的頁面。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>此程式顯示與Microsoft機器翻譯的內建整合。 使用 [AEM翻譯整合架構](/help/sites-administering/translation.md)，您可以與許多標準翻譯服務整合，以協調AEM的翻譯。

## 更多資訊 {#further-information}

有關詳細資訊，請參閱創作文檔 [轉譯多語言網站的內容](/help/sites-administering/translation.md) 以取得完整的技術詳細資訊。
