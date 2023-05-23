---
title: 在AEM Forms應用中使用自動保存
seo-title: Using autosave in AEM Forms app
description: 瞭解如何在AEM Forms應用中使用自動保存功能，以避免資料丟失。
seo-description: Learn how to use autosave feature in AEM Forms app that lets you avoid data loss.
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
source-wordcount: '294'
ht-degree: 0%

---

# 在AEM Forms應用中使用自動保存{#using-autosave-in-aem-forms-app}

當用戶在Adobe Experience Manager Forms應用中輸入資料時，自動保存功能會定期保存資料。 AEM Forms應用中的自動保存功能可幫助您避免應用程式意外關閉時丟失資料。

你的應用可能意外關閉：

* 如果設備因電池電量不足而關閉
* 如果用戶殺掉應用
* 如果發生意外崩潰

您可以指定應用保存輸入資料的間隔。

>[!NOTE]
>
>明智地選擇自動保存頻率。 頻繁的自動保存操作會對設備的效能產生明顯影響。

執行以下步驟以在AEM Forms應用中使用自動保存功能：

1. 登錄到應用，然後導航到 **設定>常規**。
1. 在「常規」螢幕中，使用 **自動保存頻率** 選項，選擇希望應用保存輸入資料的間隔。
   [ ![設定自動保存頻率](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. 當您重新啟動應用並以同一用戶登錄時，系統會提示您使用「恢復未保存的任務」對話框還原任務。 按一下 **確定** 在「恢復未保存的任務」對話框中，繼續處理保存的任務。 您可以按一下 **取消** 刪除與上次觸發的自動保存相對應的已保存資料，然後開始處理新任務。

   按一下 **確定**，使用與應用程式崩潰前觸發的最新自動保存相對應的資料還原任務。 它包括表單資料和與任務關聯的所有附件。
   [ ![正在恢復任務&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**答：** 正在進行的表格 **B** 應用已強制關閉 **C.** 應用程式已重新啟動，但「恢復未保存的任務」對話框 **D** 用原始資料還原的表單
