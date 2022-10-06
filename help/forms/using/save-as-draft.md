---
title: 將任務或表單另存為草稿
seo-title: Saving a task or form as a draft
description: 在AEM Forms應用程式中儲存任務或表單草稿副本的步驟
seo-description: Steps to save a draft copy of a task or a form in the AEM Forms app
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
exl-id: b4a23b2e-ab18-402c-8dfa-2533ee692912
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 將任務或表單另存為草稿 {#saving-a-task-or-form-as-a-draft}

另存為草稿選項會儲存任務或表單的快照，以及在關聯表單中填入的資料。 也可以從模板建立草稿。 草稿會儲存在行動裝置中，並與Adobe Experience Manager Forms伺服器同步，以供稍後擷取。

您可以 [更新表單](/help/forms/using/working-with-form.md), [加上注釋](/help/forms/using/add-attachments.md) 照片和手寫筆記。 當您繼續更新表單時，建議將其儲存為草稿。 若是您決定稍後提交已填寫的表單，將其儲存為草稿會很有幫助。

若要為儲存在表單入口網站上的表單啟用另存為草稿功能，請參閱 [將HTML5表單儲存為草稿](/help/forms/using/saving-html5-form-draft.md).
若要設定適用性表單的提交，請參閱 [草稿和提交元件](/help/forms/using/draft-submission-component.md). (與AEM Forms JEE伺服器同步的表單無效。)

若要建立草稿，請開啟表單並點選 **另存為草稿** ![另存為草稿](assets/save-as-draft.png). 提供草稿的名稱，然後點選 **儲存**. 草稿會儲存在「草稿」資料夾中，並與伺服器同步。 如果應用程式離線，則會儲存在Outbox資料夾中。

如果您之後更新對應的表單，變更會立即顯示。 將AEM Forms應用程式與AEM Forms伺服器同步時，草稿即會上傳至AEM Forms伺服器。 此外，草稿會從Outbox移至Tasks或Drafts資料夾。 編輯圖示會隨即出現。

當您繼續處理多個任務和起始點並儲存它們時，草稿即會儲存。 每次您的應用程式與AEM Forms伺服器同步時，草稿都會儲存至伺服器。 它可確保您隨時都能根據上次儲存的日期和時間復原草稿。 例如，如果您重新安裝應用程式或變更行動裝置，可從伺服器下載草稿。

## 刪除草稿 {#delete-a-draft}

草稿資料夾會列出所有草稿。 您可以使用「刪除草稿」選項，從行動裝置和伺服器中永久刪除草稿。

無法刪除從任務建立的草稿的選項。 刪除從任務建立的草稿時，將放棄該任務。

您可以在離線和線上模式中捨棄草稿。 在離線模式中捨棄草稿時，草稿只會在與伺服器的連線還原時，從伺服器刪除。

執行下列步驟刪除草稿：

1. 在AEM Forms應用程式中，導覽至 **Forms。**
1. 選擇 **草稿** 從「搜尋」旁的下拉式清單。
1. 具有編輯圖示的表單 ![edit-draft-app](assets/edit-draft-app.png) 表示繪製。 點選草稿旁的水準刪節號。
1. 在點選水準省略號時顯示的選項中，點選 **刪除草稿**.
