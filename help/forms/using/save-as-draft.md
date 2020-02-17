---
title: 將任務或表單另存為草稿
seo-title: 將任務或表單另存為草稿
description: 在AEM Forms應用程式中儲存工作或表單草稿副本的步驟
seo-description: 在AEM Forms應用程式中儲存工作或表單草稿副本的步驟
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 將任務或表單另存為草稿 {#saving-a-task-or-form-as-a-draft}

另存為草稿選項將保存任務或表單的快照以及在關聯表單中填充的資料。 您也可以從範本建立草稿。 草稿會儲存在行動裝置中，並與Adobe Experience Manager Forms伺服器同步，以供日後擷取。

您可以 [更新表單](/help/forms/using/working-with-form.md)、 [在表單上加上注](/help/forms/using/add-attachments.md) 解，並加上筆記。 當您繼續更新表格時，建議將它儲存為草稿。 若是您決定稍後提交已填妥的表格，將表格儲存為草稿會很有幫助。

若要針對儲存在表單入口網站上的表單啟用另存為草稿功能，請參 [閱將HTML5表單另存為草稿](/help/forms/using/saving-html5-form-draft.md)。
若要設定最適化表單的提交，請參 [閱草稿和提交元件](/help/forms/using/draft-submission-component.md)。 （與AEM Forms JEE伺服器同步的表格無效）。

要建立草稿，請開啟表單並點選「另 **存為草稿**![」(Save as Draft](assets/save-as-draft.png)Save-as-draft)。 提供草稿的名稱，然後點選「儲 **存」**。 草稿會儲存在「草稿」檔案夾中，並與伺服器同步。 如果應用程式已離線，它會儲存在「Outbox」檔案夾中。

如果您隨後更新對應的表格，則會立即反映變更。 在將AEM Forms應用程式與AEM Forms伺服器同步時，草稿會上傳至AEM Forms伺服器。 此外，草稿會從「輸出」方塊移至「工作」或「草稿」檔案夾。 編輯表徵圖會出現在旁邊。

當您繼續處理多個工作和起始點並儲存時，草稿會儲存。 每次您的應用程式與AEM Forms伺服器同步時，草稿就會儲存至伺服器。 它可確保您隨時都能根據上次儲存的日期和時間來復原草稿。 例如，如果您重新安裝應用程式或變更行動裝置，可以從伺服器下載草稿。

## 刪除草稿 {#delete-a-draft}

草稿資料夾會列出所有草稿。 您可以使用「刪除草稿」選項，從行動裝置和伺服器永久刪除草稿。

無法使用刪除從任務建立的草稿的選項。 刪除從任務建立的草稿時，將放棄該任務。

您可以在離線和線上模式中捨棄草稿。 在離線模式中放棄草稿時，只有在與伺服器的連線還原時，才會從伺服器刪除草稿。

執行以下步驟以刪除草稿：

1. 在AEM Forms應用程式中，導覽至 **Forms。**
1. 從「 **搜尋** 」旁的下拉式清單中選取「草稿」。
1. 含有編輯圖示的表 ![單edit-draft-app](assets/edit-draft-app.png) 表示草稿。 點選草稿旁的水準省略號。
1. 在點選水準省略號時出現的選項中，點選「刪除草稿」 **(Delete Draft**)。

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
