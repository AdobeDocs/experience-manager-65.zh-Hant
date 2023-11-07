---
title: Granite作業 — 使用者和群組管理
seo-title: Granite Operations - User and Group Administration
description: 瞭解Granite使用者和群組管理。
seo-description: Learn about Granite user and group administration.
uuid: 7b6b7767-712c-4cc8-8d90-36f26280d6e3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 95ab2e54-0f8d-49e0-ad20-774875f6f80a
exl-id: f3477d21-7e9a-4588-94e8-496bc42434a8
feature: Security
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 4%

---


# Granite作業 — 使用者和群組管理{#granite-operations-user-and-group-administration}

由於Granite納入JCR API規格的CRX存放庫實作，因此有自己的使用者和群組管理。

這些帳戶是 [AEM帳戶](/help/sites-administering/security.md) 而透過Granite管理所做的任何帳戶變更將會反映在從 [AEM使用者主控台](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) (例如， `http://localhost:4502/useradmin`)。 您也可以從AEM使用者主控台管理許可權和其他AEM細節。

Granite使用者和群組管理主控台都可從 **[工具](/help/sites-administering/tools-consoles.md)** 觸控最佳化UI的控制檯：

![工具主控台](assets/chlimage_1-72a.png)

選擇其中一項 **使用者** 或 **群組** 從「工具」主控台開啟適當的主控台。 在這兩種模式中，您都可以透過點按方塊，然後從工具列執行動作，或透過下的連結開啟帳戶詳細資訊，來採取動作 **名稱**.

* [使用者管理](#user-administration)

  ![chlimage_1-73](assets/chlimage_1-73a.png)

  此 **使用者** 主控台清單：

   * 使用者名稱
   * 使用者登入名稱（帳戶名稱）
   * 已指定帳戶的任何標題

* [群組管理](#group-administration)

  ![使用者管理主控台](assets/chlimage_1-74a.png)

  此 **群組** 主控台清單：

   * 群組名稱
   * 群組說明
   * 群組中的使用者/群組數量

## 使用者管理 {#user-administration}

### 新增使用者 {#adding-a-new-user}

1. 使用 **新增使用者** 圖示：

   ![「新增使用者」圖示](do-not-localize/chlimage_1-1.png)

1. 此 **建立使用者** 表單開啟次數：

   ![使用者詳細資料表單](assets/chlimage_1-75a.png)

   您可以在此輸入帳戶的使用者詳細資訊（大部分為標準且無需另行說明）：

   * **ID**

     這是使用者帳戶的唯一識別碼。 此為必填欄位，不得包含空格。

   * **電子郵件地址**
   * **密碼**

     密碼為必填。

   * **重新鍵入密碼**

     這是強制性的，因為確認密碼需要它。

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

      * **狀態**
您可以將帳戶標幟為 **主要** 或 **非使用中**.

   * **相片**

     您可以在此處上傳像片，以作為顯示圖片。

     接受的檔案類型: `.jpg .png .tif .gif`

     偏好大小： `240x240px`

   * **新增使用者至群組**

     使用選取下拉式清單來選取使用者應成為其成員的群組。 選取後，使用 **X** 儲存前取消選取的名稱。

   * **群組**

     使用者目前所屬的群組清單。 使用 **X** 儲存前取消選取的名稱。

1. 當您已定義使用者帳戶時，使用：

   * **取消** 以中止註冊。
   * **儲存** 以完成註冊。 將使用訊息確認使用者帳戶的建立。

### 編輯現有使用者 {#editing-an-existing-user}

1. 從使用者控制檯使用者名稱下的連結存取使用者詳細資訊。

1. 您現在可以在中編輯詳細資料 [新增使用者](#adding-a-new-user).

1. 從使用者控制檯使用者名稱下的連結存取使用者詳細資訊。

1. 您現在可以在中編輯詳細資料 [新增使用者](#adding-a-new-user).

### 變更現有使用者的密碼 {#changing-the-password-for-an-existing-user}

1. 從使用者控制檯使用者名稱下的連結存取使用者詳細資訊。

1. 您現在可以在中編輯詳細資料 [新增使用者](#adding-a-new-user). 在 **帳戶設定** 有一個連結 **變更密碼**.

   ![帳戶設定對話方塊](assets/chlimage_1-76a.png)

1. 此 **變更密碼** 對話方塊開啟。 輸入並重新輸入新密碼以及您的密碼。 使用 **確定** 以確認變更。

   ![變更密碼對話方塊](assets/chlimage_1-77a.png)

   訊息會確認密碼已變更。

### 快速群組指派 {#quick-group-assignment}

1. 使用點按方塊標示一或多個使用者。
1. 使用 **群組** 圖示：

   ![使用「群組」圖示](do-not-localize/chlimage_1-2.png)

   若要開啟群組選取下拉式清單：

   ![群組選擇器](assets/chlimage_1-78a.png)

1. 在選取方塊中，您可以選取或取消選取使用者帳戶應屬於的群組。

1. 當您已指派或未指派群組時，視需要使用：

   * **取消** 中止變更
   * **儲存** 確認變更

### 刪除現有的使用者詳細資訊 {#deleting-existing-user-details}

1. 使用點按方塊標示一或多個使用者。
1. 使用 **刪除** 圖示可刪除使用者詳細資訊：

   ![刪除現有的使用者詳細資訊](do-not-localize/chlimage_1-3.png)

1. 系統會要求您確認刪除，然後才會顯示訊息，確認已實際刪除。

## 群組管理 {#group-administration}

### 新增群組 {#adding-a-new-group}

1. 使用「新增群組」圖示：

   ![新增群組](do-not-localize/chlimage_1-4.png)

1. 此 **建立群組** 表單開啟次數：

   ![群組詳細資料表單](assets/chlimage_1-79a.png)

   您可以在此輸入群組詳細資料：

   * **ID**

     這是群組的唯一識別碼。 此為必填欄位，不能包含空格。

   * **名稱**

     群組的名稱，顯示在「群組」主控台中。

   * **說明**

     群組的說明。

   * **新增成員到群組**

     使用選取下拉式清單來選取要新增至群組的使用者。 選取後，使用 **X** 儲存前取消選取的名稱。

   * **群組成員**

     群組中的使用者清單。 使用 **X** 儲存前取消選取的名稱。

1. 定義群組後，請使用：

   * **取消** 以中止註冊。
   * **儲存** 以完成註冊。 將使用訊息確認群組的建立。

### 編輯現有群組 {#editing-an-existing-group}

1. 從「群組」主控台中群組名稱下方的連結存取群組詳細資料。

1. 您現在可以在中編輯並儲存詳細資料 [新增群組](#adding-a-new-group).

### 複製現有群組 {#copying-an-existing-group}

1. 使用點按方塊標示群組。
1. 使用 **複製** 圖示以複製群組詳細資料：

   ![複製現有群組](do-not-localize/chlimage_1-5.png)

1. 此 **編輯群組設定** 表單將會開啟。

   群組ID將會與原始相同，但前置詞為 `Copy of`. 您必須編輯此專案，因為ID不可包含空格。 所有其他詳細資料將與原始資料相同。

   您現在可以在中編輯並儲存詳細資料 [新增群組](#adding-a-new-group).

### 刪除現有群組 {#deleting-an-existing-group}

1. 使用點按方塊標幟一或多個群組。
1. 使用 **刪除** 圖示可刪除群組詳細資訊：

   ![刪除現有群組](do-not-localize/chlimage_1-6.png)

1. 系統會要求您確認刪除，然後才會顯示訊息，確認已實際刪除。
