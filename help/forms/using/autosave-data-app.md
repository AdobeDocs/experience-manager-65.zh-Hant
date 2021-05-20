---
title: 在AEM Forms應用程式中使用自動儲存
seo-title: 在AEM Forms應用程式中使用自動儲存
description: 了解如何使用AEM Forms應用程式中的自動儲存功能，以避免資料遺失。
seo-description: 了解如何使用AEM Forms應用程式中的自動儲存功能，以避免資料遺失。
uuid: 00fe6a10-1a72-443d-a840-0415dc769199
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2c71cc28-b7c8-4785-9fc2-b47fa80cbd70
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 在AEM Forms應用程式中使用自動儲存{#using-autosave-in-aem-forms-app}

使用者在Adobe Experience Manager Forms應用程式中輸入資料時，自動儲存功能會定期儲存資料。 AEM Forms應用程式中的自動儲存功能可協助您避免意外關閉應用程式時遺失資料。

您的應用程式可能會意外關閉：

* 如果設備因電池不足而關閉
* 如果使用者殺了應用程式
* 如果發生意外的當機

您可以指定應用程式儲存輸入資料的間隔。

>[!NOTE]
>
>審慎選取自動儲存頻率。 頻繁的自動保存操作可能會對設備的效能產生明顯的影響。

執行下列步驟以使用AEM Forms應用程式中的自動儲存功能：

1. 登入應用程式，並導覽至&#x200B;**設定>一般**。
1. 在「一般」畫面中，使用&#x200B;**自動儲存頻率**選項，選取您希望應用程式儲存輸入資料的間隔。
   [ ![設定自動儲存頻率](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. 當您重新啟動應用程式並以相同的使用者登入時，系統會提示您使用「復原未儲存的任務」對話方塊還原您的任務。 在「恢復未保存的任務」對話框中按一下「**確定**」以繼續使用保存的任務。 您可以按一下&#x200B;**取消**&#x200B;刪除與上次觸發的自動儲存相對應的已儲存資料，並開始處理新任務。

   當您按一下&#x200B;**確定**時，系統會使用應用程式當機前觸發的最新自動儲存對應的資料，來還原工作。 它包括表單資料和與任務關聯的所有附件。
   [ ![正在恢&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**復任務** A.B. **應用程式已強制關閉C.** App, **並重新啟動** 「恢復未儲存的任務」對話 **框D.** 表單已還原為原始資料
