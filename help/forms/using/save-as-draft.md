---
title: 將任務或表單另存為草稿
seo-title: Saving a task or form as a draft
description: 在AEM Forms應用中保存任務或表單草稿副本的步驟
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

另存為草稿選項保存任務或表單的快照以及在關聯表單中填寫的資料。 也可以從模板建立繪製。 這些草稿將保存在移動設備中，並與Adobe Experience Manager Forms伺服器同步，以供以後檢索。

你可以 [更新表單](/help/forms/using/working-with-form.md)。 [為其添加註釋](/help/forms/using/add-attachments.md) 照片和筆記。 在您繼續更新表單時，建議將其另存為草稿。 對於您決定在以後某個時間點提交填充表單的情況，將其保存為草稿會有所幫助。

要為在表單門戶上保存的表單啟用另存為草稿功能，請參閱 [將HTML5窗體另存為草稿](/help/forms/using/saving-html5-form-draft.md)。
要配置自適應表單的提交，請參見 [草稿和提交部分](/help/forms/using/draft-submission-component.md)。 (對於與AEM FormsJEE伺服器同步的表單無效。)

要建立拔模，請開啟窗體並點擊 **另存為草稿** ![另存為草稿](assets/save-as-draft.png)。 提供草稿的名稱並點擊 **保存**。 草稿將保存在「草稿」資料夾中，並與伺服器同步。 如果應用程式處於離線狀態，則會將其保存在「發件箱」資料夾中。

如果隨後更新相應的表單，則會立即反映更改。 在將AEM Forms應用與AEM Forms伺服器同步時，草稿將上載到AEM Forms伺服器。 此外，草稿將從「發件箱」移到「任務」或「草稿」資料夾。 旁邊將顯示一個編輯表徵圖。

在您繼續處理多個任務和起始點並保存它們時，將保存草稿。 每次您的應用與AEM Forms伺服器同步時，草稿都會保存到伺服器。 它確保您可以隨時根據上次保存的日期和時間恢復草稿。 例如，如果重新安裝應用或更改移動設備，則可以從伺服器下載草稿。

## 刪除草稿 {#delete-a-draft}

草稿資料夾列出所有草稿。 可以使用「刪除草稿」選項從移動設備和伺服器中永久刪除草稿。

刪除從任務建立的草稿的選項不可用。 刪除從任務建立的草稿時，將放棄該任務。

您可以在離線和聯機模式下放棄草稿。 在離線模式下放棄草稿時，只有在恢復與伺服器的連接時，才會從伺服器中刪除草稿。

執行以下步驟以刪除繪製：

1. 在AEM Forms應用中，導航到 **Forms。**
1. 選擇 **草稿** 從「Search（搜索）」旁邊的下拉框中。
1. 帶有編輯表徵圖的窗體 ![編輯草稿應用](assets/edit-draft-app.png) 表示繪製。 按一下拔模旁的水準省略號。
1. 在按一下水準省略號時出現的選項中，按一下 **刪除草稿**。
