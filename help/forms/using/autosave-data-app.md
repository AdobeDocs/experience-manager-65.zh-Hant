---
title: 在AEM Forms應用程式中使用自動儲存
description: 瞭解如何使用AEM Forms應用程式中的自動儲存功能，避免資料遺失。
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 在AEM Forms應用程式中使用自動儲存{#using-autosave-in-aem-forms-app}

當使用者在Adobe Experience Manager Forms應用程式中輸入資料時，自動儲存功能會定期儲存資料。 AEM Forms應用程式中的自動儲存功能可協助您在應用程式意外關閉時避免資料遺失。

您的應用程式可能會意外關閉：

* 如果您的裝置因電池電量不足而關機
* 如果使用者終止應用程式
* 如果發生非預期的當機

您可以指定應用程式儲存輸入資料的時間間隔。

>[!NOTE]
>
>謹慎選取自動儲存頻率。 頻繁的自動儲存作業可能會對裝置的效能造成明顯的影響。

執行以下步驟，在AEM Forms應用程式中使用自動儲存功能：

1. 登入應用程式，並瀏覽至&#x200B;**設定>一般**。
1. 在「一般」畫面中，使用&#x200B;**自動儲存頻率**&#x200B;選項，選取您希望應用程式儲存輸入資料的間隔。
   [![正在設定自動儲存頻率](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. 當您重新啟動應用程式並以同一個使用者登入時，系統會提示您使用「復原未儲存的工作」對話方塊來復原工作。 在[復原未儲存的工作]對話方塊中按一下[確定]&#x200B;**&#x200B;**&#x200B;以繼續使用已儲存的工作。 您可以按一下&#x200B;**取消**，刪除與上次觸發的自動儲存相對應的已儲存資料，並開始處理新工作。

   當您按一下&#x200B;**確定**&#x200B;時，工作會以與應用程式當機前觸發的最新自動儲存相對應的資料還原。 其中包含表單資料及與工作相關的所有附件。
   [![正在復原工作&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.**&#x200B;正在處理的表單&#x200B;**B.**&#x200B;應用程式已強制關閉&#x200B;**C.**&#x200B;應用程式已重新啟動，其中復原未儲存的工作對話方塊&#x200B;**D.**&#x200B;表單已還原為原始資料
