---
title: 為頁面編輯配置撤消
seo-title: Configuring Undo for Page Editing
description: 瞭解如何在中配置「撤消」頁面編輯支AEM持。
seo-description: Learn how to configure Undo support for page editing in AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# 為頁面編輯配置撤消{#configuring-undo-for-page-editing}

的 [OSGi服務](/help/sites-deploying/configuring-osgi.md)  **第CQ WCM天撤消配置** ( `com.day.cq.wcm.undo.UndoConfigService`)顯示幾個控制編輯頁面的撤消和重做命令行為的屬性。

## 預設設定 {#default-configuration}

在標準安裝中，預設設定定義為 `sling:OsgiConfig`節點：

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

此節點包含 `cq.wcm.undo.whitelist` 和 `cq.wcm.undo.blacklist` 屬性，對於其它屬性，將採用預設值。

>[!CAUTION]
>
>你 ***必須*** 沒有改變 `/libs` 路徑。
>
>這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時很可能被覆蓋）。

## 配置撤消和重做 {#configuring-undo-and-redo}

您可以為自己的實例配置這些OSGi服務屬性。

>[!NOTE]
>
>使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

以下列出Web控制台中顯示的屬性，後跟相應OSGi參數的名稱，以及說明和預設值（如適用）:

* **啟用**
( 
`cq.wcm.undo.enabled`)

   * **說明**:確定頁面作者是否可以撤消和重做更改。
   * **預設**: `Selected`
   * **類型**: `Boolean`

* **路徑**
( 
`cq.wcm.undo.path`)

   * **說明**:保存二進位還原資料的儲存庫路徑。 當作者更改二進位資料（如影像）時，資料的原始版本將保留在此處。 當對二進位資料的更改被撤消時，此二進位撤消資料將恢復到頁面。
   * **預設**: `/var/undo`
   * **類型**: `String`

   >[!NOTE]
   >
   >預設情況下，只有管理員才能訪問 `/var/undo` 的下界。 作者只有在獲得訪問二進位撤消資料的權限後才能對二進位內容執行撤消和重做操作。

* **最小值. 有效性**
( 
`cq.wcm.undo.validity`)

   * **說明**:二進位還原資料儲存的最小時間（以小時為單位）。 在此時間段之後，二進位資料可用於刪除，以節省磁碟空間。
   * **預設**: `10`
   * **類型**: `Integer`

* **步驟**
( 
`cq.wcm.undo.steps`)

   * **說明**:在撤消歷史記錄中儲存的最大頁操作數。
   * **預設**: `20`
   * **類型**: `Integer`

* **持久性**
( 
`cq.wcm.undo.persistence`)

   * **說明**:繼續撤消歷史記錄的類。 提供了兩個持久性類：

      * `CQ.undo.persistence.WindowNamePersistence`:使用window.name屬性保留歷史記錄。
      * `CQ.undo.persistence.CookiePersistance`:使用Cookie保留歷史記錄。
   * **預設**: `CQ.undo.persistence.WindowNamePersistence`
   * **類型**: `String`


* **持久性模式**
( 
`cq.wcm.undo.persistence.mode`)

   * **說明**:確定何時保留撤消歷史記錄。 選擇此選項可在每頁編輯後保留撤消歷史記錄。 清除此選項僅在重新載入頁面（例如，用戶導航到其他頁面）時才會持續。

      保留撤消歷史記錄使用Web瀏覽器資源。 如果用戶的瀏覽器對頁面編輯反應緩慢，請嘗試在重新載入頁面時保留撤消歷史記錄。

   * **預設**: `Selected`
   * **類型**: `Boolean`

* **標籤模式**
( 
`cq.wcm.undo.markermode`)

   * **說明**:指定在撤消或重做發生時用於指示哪些段落受到影響的可視提示。 以下值有效：

      * 快閃記憶體：段落的選擇指示器暫時閃爍。
      * 選擇：選擇段落。
   * **預設**: `flash`
   * **類型**: `String`


* **良好的元件**
( 
`cq.wcm.undo.whitelist`)

   * **說明**:要受撤消和重做命令影響的元件清單。 當元件路徑與撤消/重做一起正常工作時，將其添加到此清單。 添加星號(&amp;ast;)以指定一組元件：

      * 以下值指定基礎文本元件：

         `foundation/components/text`

      * 以下值指定所有基礎元件：

         `foundation/components/*`
   * 當撤消或重做發出到不在此清單中的元件時，將顯示一條消息，指出該命令可能不可靠。

   * **預設**:該屬性填充了許多提供的AEM元件。
   * **類型**: `String[]`


* **壞元件**
( 
`cq.wcm.undo.blacklist`)

   * **說明**:不想受撤消命令影響的元件和/或元件操作的清單。 使用undo命令添加不能正常操作的元件和元件操作：

      * 例如，當不希望元件的任何操作在撤消歷史記錄中時添加元件路徑 `collab/forum/components/post`
      * 如果希望撤消歷史記錄中省略特定操作，請向路徑追加冒號(:)和操作（例如，其它操作正確運行） `collab/forum/components/post:insertParagraph.`

   >[!NOTE]
   >
   >當某個操作在此清單上時，它仍被添加到撤消歷史記錄中。 用戶無法撤消早於 **錯誤元件** 還原歷史記錄中的操作。

   * 典型操作名稱如下：

      * `insertParagraph`:元件將添加到頁面。
      * `removeParagraph`:元件將被刪除。
      * `moveParagraph`:該段落將移到其他位置。
      * `updateParagraph`:段落屬性已更改。
   * **預設**:該屬性填充了多個元件操作。
   * **類型**: `String[]`
