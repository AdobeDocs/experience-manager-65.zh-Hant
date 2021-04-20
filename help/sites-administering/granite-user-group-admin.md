---
title: Granite Operations —— 使用者與群組管理
seo-title: Granite Operations —— 使用者與群組管理
description: 瞭解Granite使用者和群組管理。
seo-description: 瞭解Granite使用者和群組管理。
uuid: 7b6b7767-712c-4cc8-8d90-36f26280d6e3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 95ab2e54-0f8d-49e0-ad20-774875f6f80a
exl-id: f3477d21-7e9a-4588-94e8-496bc42434a8
feature: Security
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 4%

---

# Granite Operations - User and Group Administration{#granite-operations-user-and-group-administration}

當Granite整合JCR API規格的CRX Repository實作時，它擁有自己的使用者和群組管理。

這些帳戶是[帳戶](/help/sites-administering/security.md)的基礎AEM，如果／從[ AEM Users console](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console)存取帳戶時，將反映使用Granite管理所做的任何帳戶變更(例如`http://localhost:4502/useradmin`)。 您也可AEM以從「使用者控制台」管理權限和其AEM他特定資訊。

Granite使用者和群組管理主控台都可從觸控最佳化UI的&#x200B;**[Tools](/help/sites-administering/tools-consoles.md)**&#x200B;主控台取得：

![chlimage_1-72](assets/chlimage_1-72a.png)

從「工具」控制台選擇&#x200B;**Users**&#x200B;或&#x200B;**Groups**&#x200B;將開啟相應的控制台。 在這兩種方式中，您都可以使用點按方塊，然後從工具列執行動作，或透過&#x200B;**Name**&#x200B;下方的連結開啟帳戶詳細資訊。

* [使用者管理](#user-administration)

   ![chlimage_1-73](assets/chlimage_1-73a.png)

   **Users**&#x200B;控制台列出：

   * 用戶名
   * 使用者登入名稱（帳戶名稱）
   * 帳戶已獲得的任何標題

* [群組管理](#group-administration)

   ![chlimage_1-74](assets/chlimage_1-74a.png)

   **Groups**&#x200B;控制台清單：

   * 群組名稱
   * 群組說明
   * 群組中的使用者／群組數

## 用戶管理{#user-administration}

### 添加新用戶{#adding-a-new-user}

1. 使用&#x200B;**Add User**&#x200B;表徵圖：

   ![](do-not-localize/chlimage_1-1.png)

1. 將開啟&#x200B;**建立用戶**&#x200B;表單：

   ![chlimage_1-75](assets/chlimage_1-75a.png)

   您可以在此處輸入帳戶的使用者詳細資訊（大多為標準和自我說明）:

   * **ID**

      這是使用者帳戶的唯一識別碼。 它是強制的，不能包含空格。

   * **電子郵件地址**
   * **密碼**

      密碼是強制的。

   * **重新鍵入密碼**

      這是強制性的，因為確認密碼是必要的。

   * **名字**
   * **姓氏**
   * **電話號碼**
   * **職稱**
   * **街道**
   * **行動**
   * **城市**
   * **郵遞區號**
   * **國家/地區**
   * **狀態**
   * **標題**
   * **性別**
   * **關於**
   * **帳戶設定**

      * **狀**
態您可以將帳戶標幟為 
**活動** 或非 **活動**。
   * **相片**

      您可以在這裡上傳像片，以做為頭像。

      接受的檔案類型: `.jpg .png .tif .gif`

      首選大小：`240x240px`

   * **新增使用者至群組**

      使用選擇下拉式清單來選擇使用者應為其成員的群組。 選擇後，在保存前按名稱使用&#x200B;**X**&#x200B;以取消選擇。

   * **群組**

      使用者目前為其成員的群組清單。 儲存前，請使用&#x200B;**X**&#x200B;名稱來取消選取。


1. 定義用戶帳戶使用時：

   * **取消** 以中止註冊。
   * **薩** 韋托完成註冊。建立使用者帳戶時，將會收到訊息。

### 編輯現有用戶{#editing-an-existing-user}

1. 從「使用者控制台」的使用者名稱下方的連結存取使用者詳細資料。

1. 您現在可以編輯詳細資料，如[新增使用者](#adding-a-new-user)中。

1. 從「使用者控制台」的使用者名稱下方的連結存取使用者詳細資料。

1. 您現在可以編輯詳細資料，如[新增使用者](#adding-a-new-user)中。

### 更改現有用戶的密碼{#changing-the-password-for-an-existing-user}

1. 從「使用者控制台」的使用者名稱下方的連結存取使用者詳細資料。

1. 您現在可以編輯詳細資料，如[新增使用者](#adding-a-new-user)中。 在「**帳戶設定**」下，**更改密碼**&#x200B;的連結。

   ![chlimage_1-76](assets/chlimage_1-76a.png)

1. 將開啟&#x200B;**更改密碼**&#x200B;對話框。 輸入並重新鍵入新密碼以及密碼。 使用&#x200B;**OK**&#x200B;確認更改。

   ![chlimage_1-77](assets/chlimage_1-77a.png)

   訊息會確認密碼已變更。

### 快速組分配{#quick-group-assignment}

1. 使用點按方塊來標幟一或多個使用者。
1. 使用&#x200B;**Groups**&#x200B;圖示：

   ![](do-not-localize/chlimage_1-2.png)

   要開啟組選擇下拉清單：

   ![chlimage_1-78](assets/chlimage_1-78a.png)

1. 在選擇方塊中，您可以選取或取消選取使用者帳戶應屬於的群組。

1. 當您指派或未指派群組時，群組會視需要使用：

   * **取消** 以中止更改
   * **薩韋** 托確認更改

### 刪除現有用戶詳細資訊{#deleting-existing-user-details}

1. 使用點按方塊來標幟一或多個使用者。
1. 使用&#x200B;**Delete**&#x200B;圖示刪除使用者詳細資料：

   ![](do-not-localize/chlimage_1-3.png)

1. 系統會要求您確認刪除，然後會傳送訊息確認實際刪除已發生。

## 群組管理{#group-administration}

### 添加新組{#adding-a-new-group}

1. 使用「新增群組」圖示：

   ![](do-not-localize/chlimage_1-4.png)

1. **建立組**&#x200B;表單將開啟：

   ![chlimage_1-79](assets/chlimage_1-79a.png)

   您可以在此處輸入組詳細資訊：

   * **ID**

      這是群組的唯一識別碼。 這是必填項目，不能包含空格。

   * **名稱**

      群組名稱；它將顯示在「組」控制台中。

   * **說明**

      群組的說明。

   * **新增成員到群組**

      使用選擇下拉式清單來選取要新增至群組的使用者。 選擇後，在保存前按名稱使用&#x200B;**X**&#x200B;以取消選擇。

   * **群組成員**

      群組中的使用者清單。 儲存前，請使用&#x200B;**X**&#x200B;名稱來取消選取。

1. 定義群組後，請使用：

   * **取消** 以中止註冊。
   * **薩** 韋托完成註冊。建立群組時，將會收到訊息。

### 編輯現有組{#editing-an-existing-group}

1. 從群組主控台中群組名稱下的連結存取群組詳細資料。

1. 您現在可以編輯並儲存詳細資料，如[新增群組](#adding-a-new-group)。

### 複製現有組{#copying-an-existing-group}

1. 使用點按方塊來標幟群組。
1. 使用&#x200B;**Copy**&#x200B;圖示來複製群組詳細資訊：

   ![](do-not-localize/chlimage_1-5.png)

1. **編輯群組設定**&#x200B;表單將會開啟。

   群組ID與原始ID相同，但前置詞為`Copy of`。 由於ID不能包含空格，因此您必須編輯此項目。 所有其他細節都會與原稿相同。

   您現在可以編輯並儲存詳細資料，如[新增群組](#adding-a-new-group)。

### 刪除現有組{#deleting-an-existing-group}

1. 使用點按方塊來標幟一或多個群組。
1. 使用&#x200B;**Delete**&#x200B;圖示刪除群組詳細資訊：

   ![](do-not-localize/chlimage_1-6.png)

1. 系統會要求您確認刪除，然後會傳送訊息確認實際刪除已發生。
