---
title: Granite作業 — 使用者和群組管理
description: 瞭解Granite使用者和群組管理。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: f3477d21-7e9a-4588-94e8-496bc42434a8
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 1%

---


# Granite作業 — 使用者和群組管理{#granite-operations-user-and-group-administration}

由於Granite納入CRX Repository的JCR API規格實作，因此有自己的使用者和群組管理。

這些帳戶是[AEM帳戶](/help/sites-administering/security.md)的基礎基礎，如果從[AEM使用者主控台](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) （例如`http://localhost:4502/useradmin`）存取帳戶，則會反映對Granite管理所做的任何帳戶變更。 您也可以從AEM使用者主控台管理許可權和其他AEM細節。

觸控最佳化UI的&#x200B;**[工具](/help/sites-administering/tools-consoles.md)**&#x200B;主控台提供Granite使用者和群組管理主控台：

![工具主控台](assets/chlimage_1-72a.png)

從[工具]主控台選擇&#x200B;**使用者**&#x200B;或&#x200B;**群組**&#x200B;可開啟適當的主控台。 在這兩種方式中，您都可以透過使用點按方塊，然後從工具列執行動作，或透過&#x200B;**Name**&#x200B;下的連結開啟帳戶詳細資料。

* [使用者管理](#user-administration)

  ![chlimage_1-73](assets/chlimage_1-73a.png)

  **使用者**&#x200B;主控台清單：

   * 使用者名稱
   * 使用者登入名稱（帳戶名稱）
   * 已指定帳戶的任何標題

* [群組管理](#group-administration)

  ![使用者管理主控台](assets/chlimage_1-74a.png)

  **群組**&#x200B;主控台清單：

   * 群組名稱
   * 群組說明
   * 群組中的使用者/群組數量

## 使用者管理 {#user-administration}

### 新增使用者 {#adding-a-new-user}

1. 使用&#x200B;**新增使用者**&#x200B;圖示：

   ![新增使用者圖示](do-not-localize/chlimage_1-1.png)

1. **建立使用者**&#x200B;表單開啟：

   ![使用者詳細資料表單](assets/chlimage_1-75a.png)

   您可以在此輸入帳戶的使用者詳細資訊（大部分為標準且無需另行說明）：

   * **識別碼**

     這是使用者帳戶的唯一識別碼。 此為必填欄位，不得包含空格。

   * **電子郵件地址**
   * **密碼**

     密碼為必填。

   * **Retype密碼**

     這是強制性的，因為確認密碼需要它。

   * **名字**
   * **姓氏**
   * **電話號碼**
   * **職稱**
   * **街道**
   * **行動裝置**
   * **城市**
   * **郵遞區號**
   * **國家/地區**
   * **狀態**
   * **標題**
   * **性別**
   * **關於**
   * **帳戶設定**

      * **狀態**
您可以將帳戶標幟為&#x200B;**使用中**&#x200B;或&#x200B;**非使用中**。

   * **像片**

     您可以在此處上傳像片，以作為顯示圖片。

     接受的檔案型別： `.jpg .png .tif .gif`

     偏好的大小： `240x240px`

   * **新增使用者至群組**

     使用選取下拉式清單來選取使用者應成為其成員的群組。 選取後，在儲存前使用名稱要取消選取的&#x200B;**X**。

   * **群組**

     使用者目前所屬的群組清單。 在儲存前，以名稱使用&#x200B;**X**&#x200B;以取消選取。

1. 當您已定義使用者帳戶時，使用：

   * **取消**&#x200B;以中止註冊。
   * **儲存**&#x200B;以完成註冊。 將使用訊息確認使用者帳戶的建立。

### 編輯現有使用者 {#editing-an-existing-user}

1. 從使用者控制檯使用者名稱下的連結存取使用者詳細資訊。

1. 您現在可以編輯詳細資料，如[新增使用者](#adding-a-new-user)。

1. 從使用者控制檯使用者名稱下的連結存取使用者詳細資訊。

1. 您現在可以編輯詳細資料，如[新增使用者](#adding-a-new-user)。

### 變更現有使用者的密碼 {#changing-the-password-for-an-existing-user}

1. 從使用者控制檯使用者名稱下的連結存取使用者詳細資訊。

1. 您現在可以編輯詳細資料，如[新增使用者](#adding-a-new-user)。 在&#x200B;**帳戶設定**&#x200B;下有&#x200B;**變更密碼**&#x200B;的連結。

   ![帳戶設定對話方塊](assets/chlimage_1-76a.png)

1. **變更密碼**&#x200B;對話方塊開啟。 輸入並重新輸入新密碼以及您的密碼。 使用&#x200B;**確定**&#x200B;確認變更。

   ![變更密碼對話方塊](assets/chlimage_1-77a.png)

   訊息會確認密碼已變更。

### 快速群組指派 {#quick-group-assignment}

1. 使用點按方塊標示一或多個使用者。
1. 使用&#x200B;**群組**&#x200B;圖示：

   ![使用「群組」圖示](do-not-localize/chlimage_1-2.png)

   若要開啟群組選取下拉式清單：

   ![群組選擇器](assets/chlimage_1-78a.png)

1. 在選取方塊中，您可以選取或取消選取使用者帳戶應屬於的群組。

1. 當您已指派或未指派群組時，視需要使用：

   * **取消**&#x200B;以中止變更
   * **儲存**&#x200B;以確認變更

### 刪除現有的使用者詳細資訊 {#deleting-existing-user-details}

1. 使用點按方塊標示一或多個使用者。
1. 使用&#x200B;**刪除**&#x200B;圖示來刪除使用者詳細資訊：

   ![刪除現有的使用者詳細資料](do-not-localize/chlimage_1-3.png)

1. 系統會要求您確認刪除，然後才會顯示訊息，確認已實際刪除。

## 群組管理 {#group-administration}

### 新增群組 {#adding-a-new-group}

1. 使用「新增群組」圖示：

   ![新增群組](do-not-localize/chlimage_1-4.png)

1. **建立群組**&#x200B;表單開啟：

   ![群組詳細資料表單](assets/chlimage_1-79a.png)

   您可以在此輸入群組詳細資料：

   * **識別碼**

     這是群組的唯一識別碼。 此為必填欄位，不能包含空格。

   * **名稱**

     群組的名稱，顯示在「群組」主控台中。

   * **說明**

     群組的說明。

   * **新增成員至群組**

     使用選取下拉式清單來選取要新增至群組的使用者。 選取後，在儲存前使用名稱要取消選取的&#x200B;**X**。

   * **群組成員**

     群組中的使用者清單。 在儲存前，以名稱使用&#x200B;**X**&#x200B;以取消選取。

1. 定義群組後，請使用：

   * **取消**&#x200B;以中止註冊。
   * **儲存**&#x200B;以完成註冊。 將使用訊息確認群組的建立。

### 編輯現有群組 {#editing-an-existing-group}

1. 從「群組」主控台中群組名稱下方的連結存取群組詳細資料。

1. 您現在可以在[新增群組](#adding-a-new-group)中編輯並儲存詳細資料。

### 複製現有群組 {#copying-an-existing-group}

1. 使用點按方塊標示群組。
1. 使用&#x200B;**複製**&#x200B;圖示來複製群組詳細資料：

   ![複製現有群組](do-not-localize/chlimage_1-5.png)

1. 將開啟&#x200B;**編輯群組設定**&#x200B;表單。

   群組ID將與原始的相同，但前置詞為`Copy of`。 編輯此ID，因為它不能包含空格。 所有其他細節與原始細節相同。

   您現在可以在[新增群組](#adding-a-new-group)中編輯並儲存詳細資料。

### 刪除現有群組 {#deleting-an-existing-group}

1. 使用點按方塊標幟一或多個群組。
1. 使用&#x200B;**刪除**&#x200B;圖示來刪除群組詳細資料：

   ![正在刪除現有的群組](do-not-localize/chlimage_1-6.png)

1. 系統會要求您確認刪除，然後才會顯示訊息，確認已實際刪除。
