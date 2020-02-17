---
title: 在AEM Forms應用程式中使用自動儲存
seo-title: 在AEM Forms應用程式中使用自動儲存
description: 瞭解如何在AEM Forms應用程式中使用自動儲存功能，讓您避免資料遺失。
seo-description: 瞭解如何在AEM Forms應用程式中使用自動儲存功能，讓您避免資料遺失。
uuid: 00fe6a10-1a72-443d-a840-0415dc769199
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2c71cc28-b7c8-4785-9fc2-b47fa80cbd70
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 在AEM Forms應用程式中使用自動儲存{#using-autosave-in-aem-forms-app}

當使用者在Adobe Experience Manager Forms應用程式中輸入資料時，自動儲存功能會定期儲存資料。 AEM Forms應用程式中的自動儲存功能可協助您避免在應用程式意外關閉時遺失資料。

您的應用程式可能會意外關閉：

* 如果您的裝置因電池不足而關閉
* 如果使用者殺了應用程式
* 如果發生意外當機

您可以指定應用程式儲存輸入資料的間隔。

>[!NOTE]
>
>審慎地選擇自動保存頻率。 頻繁的自動儲存操作可能會對您裝置的效能產生明顯影響。

執行下列步驟，在AEM Forms應用程式中使用自動儲存功能：

1. 登入應用程式，並導覽至「設定> **一般」**。
1. 在「一般」畫面中，使用「 **自動儲存頻率** 」選項，選取您希望應用程式儲存輸入資料的間隔。
   [ 設 ![定自動儲存頻率](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. 當您重新啟動應用程式並使用相同的使用者登入時，系統會提示您使用「復原未儲存的工作」對話方塊還原您的工作。 在「恢 **復未保存的任務** 」對話框中按一下「確定」以繼續使用保存的任務。 您可以按一 **下「取消** 」，刪除與上次觸發的自動儲存相對應的已儲存資料，並開始使用新工作。

   當您按一下「 **確定**」時，系統會還原工作，其資料會與應用程式當機前觸發的最新自動儲存相對應。 它包括表單資料和與任務關聯的所有附件。
   [![](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)******&#x200B;恢復任&#x200B;**務A進行中的表格** B.應用程式已強制關 **閉C.** App，並在「恢復未保存的任務」對話框 **D中重新啟動。以原始資料還原的表單

