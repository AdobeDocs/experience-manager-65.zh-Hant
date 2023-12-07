---
title: 將任務或表單儲存為草稿
description: 在AEM Forms應用程式中儲存任務或表單草稿副本的步驟
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b4a23b2e-ab18-402c-8dfa-2533ee692912
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 將任務或表單儲存為草稿 {#saving-a-task-or-form-as-a-draft}

另存為草稿選項可儲存任務或表單的快照以及在相關表單中填寫的資料。 您也可以從範本建立草稿。 草稿會儲存在行動裝置內，並與Adobe Experience Manager Forms伺服器同步，以供稍後擷取。

您可以 [更新表單](/help/forms/using/working-with-form.md)， [加上註釋](/help/forms/using/add-attachments.md) 包含像片與手寫筆記。 當您繼續更新表單時，建議將其儲存為草稿。 若您決定稍後再提交已填寫的表單，則將其儲存為草稿會很有幫助。

若要為儲存在表單入口網站上的表單啟用另存為草稿功能，請參閱 [將HTML5表單儲存為草稿](/help/forms/using/saving-html5-form-draft.md).
若要設定最適化表單的提交方式，請參閱 [草稿和提交元件](/help/forms/using/draft-submission-component.md). (對與AEM Forms JEE伺服器同步的表單無效。)

若要建立草稿，請開啟表單並選取 **另存為草稿** ![另存為草稿](assets/save-as-draft.png). 提供草稿的名稱並選取 **儲存**. 草稿會儲存在「草稿」資料夾中，並與伺服器同步。 如果應用程式離線，則會將其儲存在Outbox資料夾中。

如果您在之後更新對應的表單，變更會立即反映出來。 將AEM Forms應用程式與AEM Forms伺服器同步時，草稿會上傳至AEM Forms伺服器。 此外，草稿會從「寄件匣」移至「工作」或「草稿」資料夾。 其旁邊會顯示編輯圖示。

當您繼續處理多個任務和起點並儲存它們時，草稿就會儲存。 每次您的應用程式與AEM Forms伺服器同步時，草稿都會儲存至伺服器。 這可確保您隨時可以根據上次儲存的日期和時間復原草稿。 例如，如果您重新安裝應用程式或變更行動裝置，則可以從伺服器下載草稿。

## 刪除草稿 {#delete-a-draft}

草稿資料夾會列出所有草稿。 您可以使用「刪除草稿」選項，從行動裝置和伺服器永久刪除草稿。

刪除從任務建立的草稿的選項無法使用。 刪除從任務建立的草稿時，該任務會放棄。

您可以在離線和線上模式中捨棄草稿。 在離線模式下捨棄草稿時，僅當與伺服器的連線恢復時，草稿才會從伺服器中刪除。

執行以下步驟來刪除草稿：

1. 在AEM Forms應用程式中，導覽至 **Forms。**
1. 選取 **草稿** 從「搜尋」旁的下拉式清單。
1. 具有編輯圖示的表單 ![edit-draft-app](assets/edit-draft-app.png) 表示草稿。 選取拔模旁邊的水準省略符號。
1. 在您選取水準省略符號時顯示的選項中，選取 **刪除草稿**.
