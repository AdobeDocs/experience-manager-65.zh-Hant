---
title: We.Retail全球化網站結構的嘗試
seo-title: We.Retail全球化網站結構的嘗試
description: 'null'
seo-description: 'null'
uuid: 5e5a809d-578f-4171-8226-cb65aa995754
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d674458c-d5f3-4dee-a673-b0777c02ad30
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---


# 在We.Retail{#trying-out-the-globalized-site-structure-in-we-retail}中嘗試全球化網站結構

We.Retail是以全球化網站結構建立的，提供語言母版，可即時複製至國家／地區特定網站。 一切都是現成可用的設定，讓您可嘗試此結構和內建的轉譯功能。

## 試用{#trying-it-out}

1. 從&#x200B;**全域導覽->網站**&#x200B;開啟網站主控台。
1. 切換至欄檢視（如果尚未啟用），然後選取「We.Retail」。 請注意瑞士、美國、法國等與語言大師課程並列的國家結構範例。

   ![chlimage_1-87](assets/chlimage_1-87a.png)

1. 選擇「瑞士」，並查看該國語言的語言根。 請注意，這些根下尚未包含任何內容。

   ![chlimage_1-88](assets/chlimage_1-88a.png)

1. 切換至清單檢視，查看國家／地區的語言副本都是即時副本。

   ![chlimage_1-89](assets/chlimage_1-89a.png)

1. 返回列視圖並按一下「語言主版」，查看帶有內容的語言主版根目錄。 請注意，只有英文版才有內容。

   We.Retail不附帶任何翻譯內容，但已準備好結構和配置，讓您演示翻譯服務。

   ![chlimage_1-90](assets/chlimage_1-90a.png)

1. 在選取「英文語言主版」後，在網站主控台中開啟「**參考**」邊欄，並選取「語言副本」。****

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 勾選&#x200B;**語言副本**&#x200B;標籤旁的核取方塊，以選取所有語言副本。 在滑軌的&#x200B;**更新語言copys**&#x200B;部分中，選擇&#x200B;**建立新翻譯項目**&#x200B;的選項。 為項目提供名稱，然後按一下&#x200B;**Update**。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 會針對每種語言翻譯建立專案。 在&#x200B;**Navigation -> Projects**&#x200B;下查看它們。

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 按一下德文可查看翻譯項目的詳細資訊。 請注意，狀態為&#x200B;**Draft**。 要使用Microsoft的翻譯服務啟動翻譯，請按一下&#x200B;**翻譯作業**&#x200B;標題旁的Chevron ，然後選擇&#x200B;**開始**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 翻譯項目開始。 按一下卡底部標有翻譯作業的省略號以查看詳細資訊。 狀態為&#x200B;**準備審核**&#x200B;的頁面已經由翻譯服務翻譯。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 選擇清單中的一個頁面，然後在工具欄中的&#x200B;**在站點中預覽**&#x200B;將開啟頁面編輯器中翻譯的頁面。

   ![chlimage_1-96](assets/chlimage_1-96.png)

>[!NOTE]
>
>此過程演示了與Microsoft機器翻譯的內置整合。 使用[AEM翻譯整合框架](/help/sites-administering/translation.md)，您可以與許多標準翻譯服務整合，以協調AEM的翻譯。

## 更多資訊 {#further-information}

如需詳細資訊，請參閱編寫檔案[多語言網站翻譯內容](/help/sites-administering/translation.md)以取得完整的技術詳細資訊。
