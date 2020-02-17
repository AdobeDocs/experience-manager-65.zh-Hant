---
title: 建立和管理表單中資產的審核
seo-title: 建立和管理表單中資產的審核
description: '「審閱」是一種機制，可讓一位或多位審閱者對表單中可用的資產加上註解。 '
seo-description: '「審閱」是一種機制，可讓一位或多位審閱者對表單中可用的資產加上註解。 '
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 建立和管理表單中資產的審核{#creating-and-managing-reviews-for-assets-in-forms}

## 評論 {#review}

「審閱」是一種機制，可讓一位或多位審閱者對表單中可用的資產加上註解。

## 設定審核 {#setting-up-a-review}

1. 導覽至「表單」索引標籤並選取表單。
1. 如果資產沒有進行中的審核，「動作列」中會顯 ![示「開始審核」aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 圖示。 按一下「開始 ![檢閱」aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 圖示。
1. 輸入以下資訊：

   * 審核名稱：強制，可包含英數字元、連字型大小或底線。
   * 查看說明：可選，說明要審查的目的／內容。
   * 審查截止日期：可選，審核結束的日期。 在截止日期之後，任務將顯示為「逾期」。
   * 審核者：至少必須有一個。 使用組合方塊新增審核者。 鍵入一個名稱會列出所有匹配的名稱；選取名稱，然後按一下「新增」。

1. 填寫所有剩餘的詳細資訊，然後按一下「開始」。

### 設定審核時發生的動作 {#actions-that-occur-when-a-review-is-set-up}

本節介紹建立或設定審閱時的情況。

1. 將建立新的審閱任務並將其分配給審閱的發起者。
1. 所有審核者都會獲指派審核工作。 該任務將出現在其「通知」部分。 審核者可以按一下通知，或轉到收件箱查看任務。 審核者可以按一下以開啟審核任務、查看表單並開始添加註釋。

   ![審核者通知警報](assets/noti.png)

   審核者通知警報

1. 資產的發起者和審核者可以使用注釋框。 其他人可以檢視留言，但無法撰寫留言。

## 管理審核 {#managing-a-review}

>[!NOTE]
>
>只能修改進行中的審核。 無法修改已完成的審核。

1. 導覽至「表單」索引標籤並選取表單。

1. 如果資產有正在進行的審核，而您是審核的發起者，則「動作列」會顯示「管理審核 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 」圖示。 只有審閱啟動器才能管理（更新／結束）審閱。

   按一下「管 ![理檢閱」aem6forms_review_chat_](assets/aem6forms_review_chat_comment.png)commenticon。

   對於啟動器以外的用戶，「管理審閱」表徵圖被禁用。

1. 您會看到一個顯示資訊的畫面：

   * **審核名稱**:無法編輯。

   * **查看說明**:可供編輯。

   * **審查截止日期**:可供編輯。 您可以將截止日期修改為超過目前日期和時間的任何日期和時間。

   * **審核者**:可供編輯。 您可以新增或移除審核者。 如果工作逾期未完成，您只能在將期限延長到目前日期之後新增審核者。

1. 編輯必要的欄位，然後按一下「更新」。

   ![在任務管理器中查看更新狀態](assets/tskmgr.png)

   在任務管理器中查看更新狀態

1. 要結束審閱，請按一下「結束」。

### 修改審核時發生的動作 {#actions-that-occur-when-a-review-is-modified}

本節將說明在「審閱」結束／修改時會發生什麼情況：

1. 如果修改了「審閱」說明，則會更新審閱者和發起者的相應任務。
1. 如果修改了「審閱」(Review)期限，則審閱者的相應任務將更新為新日期。

1. 如果刪除了審核者：

   ![刪除審核者](assets/removeduser.png)

   刪除審核者

   1. 如果未完成，則會終止指派的任務。
   1. 審閱者無法再對資產加上註解。

1. 如果已添加審核者：

   ![添加審核者](assets/addedreviewer.png)

   添加審核者

   1. 將建立審閱任務並將其分配給新添加的審閱者。
   1. 新添加的審閱者可以為資產添加註釋。

1. 審核結束時：

   1. **審核者**:對於每個審核者，與審核相關的未完成任務將終止。 在審閱者的「通知」部分中，該任務不再顯示為「待定」。
   1. **啟動器**:分配給Review Initiator的任務已標籤為完成。 該任務將從審閱啟動器的「通知」部分中刪除。
   1. **全部**:該審閱將顯示在「上一個審閱」(Previous Reviews)部分。 不能再加入任何意見。

