---
title: 為頁面編輯設定還原
seo-title: 為頁面編輯設定還原
description: 了解如何在AEM中設定「復原」支援以編輯頁面。
seo-description: 了解如何在AEM中設定「復原」支援以編輯頁面。
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# 為頁面編輯設定還原{#configuring-undo-for-page-editing}

[OSGi服務](/help/sites-deploying/configuring-osgi.md) **Day CQ WCM Undo Configuration**(`com.day.cq.wcm.undo.UndoConfigService`)公開了幾個屬性，這些屬性控制用於編輯頁面的還原和重做命令的行為。

## 預設設定 {#default-configuration}

在標準安裝中，預設設定定義為`sling:OsgiConfig`節點上的屬性：

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

此節點包含`cq.wcm.undo.whitelist`和`cq.wcm.undo.blacklist`屬性，對於其他屬性，則使用預設值。

>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
>
>這是因為下次升級執行個體時會覆寫`/libs`的內容（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。

## 配置還原和重做{#configuring-undo-and-redo}

您可以為自己的執行個體設定這些OSGi服務屬性。

>[!NOTE]
>
>使用AEM時，有數種方法可管理這類服務的組態設定；如需詳細資訊和建議實務，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md) 。

以下列出Web控制台中顯示的屬性，後跟相應OSGi參數的名稱，以及說明和預設值（如適用）:

* **啟用**
( 
`cq.wcm.undo.enabled`)

   * **說明**:判斷頁面作者是否可以還原和重做變更。
   * **預設**:  `Selected`
   * **類型**:  `Boolean`

* **路徑**
( 
`cq.wcm.undo.path`)

   * **說明**:保存二進位還原資料的儲存庫路徑。當作者變更二進位資料（例如影像）時，原始版本的資料會保存在此處。 當取消對二進位資料的更改時，此二進位還原資料將還原到頁面。
   * **預設**:  `/var/undo`
   * **類型**:  `String`

   >[!NOTE]
   >
   >預設情況下，只有管理員可以訪問`/var/undo`節點。 作者必須獲得存取二進位還原資料的權限，才能對二進位內容執行還原和重做操作。

* **最小值. 有效性**
( 
`cq.wcm.undo.validity`)

   * **說明**:儲存二進位還原資料的最小時間（以小時為單位）。在此時段之後，可刪除二進位資料，以節省磁碟空間。
   * **預設**:  `10`
   * **類型**:  `Integer`

* **步驟**
( 
`cq.wcm.undo.steps`)

   * **說明**:還原歷史記錄中儲存的頁面動作數上限。
   * **預設**:  `20`
   * **類型**:  `Integer`

* **持續性**
( 
`cq.wcm.undo.persistence`)

   * **說明**:持續還原歷史記錄的類。提供了兩個持久類：

      * `CQ.undo.persistence.WindowNamePersistence`:使用window.name屬性保存歷史記錄。
      * `CQ.undo.persistence.CookiePersistance`:使用Cookie保存歷史記錄。
   * **預設**:  `CQ.undo.persistence.WindowNamePersistence`
   * **類型**:  `String`


* **持續模式**
( 
`cq.wcm.undo.persistence.mode`)

   * **說明**:決定何時會保存還原歷史記錄。選擇此選項可在每次頁面編輯後保留還原歷史記錄。 清除此選項，僅在頁面重新載入發生時持續存在（例如，使用者導覽至不同頁面）。

      持續還原歷史記錄使用網頁瀏覽器資源。 如果使用者的瀏覽器對頁面編輯動作反應緩慢，請嘗試在頁面重新載入時保留還原歷史記錄。

   * **預設**:  `Selected`
   * **類型**:  `Boolean`

* **標籤模式**
( 
`cq.wcm.undo.markermode`)

   * **說明**:指定用於指示在撤消或重做發生時影響哪些段落的視覺提示。下列值有效：

      * flash:段落的選擇指標暫時閃爍。
      * 選擇：已選擇該段。
   * **預設**:  `flash`
   * **類型**:  `String`


* **良好的元件**
( 
`cq.wcm.undo.whitelist`)

   * **說明**:要受撤消和重做命令影響的元件清單。當元件路徑正確運作且有還原/重做時，請將其新增至此清單。 附加星號(&amp;ast;)以指定一組元件：

      * 以下值指定基礎文本元件：

         `foundation/components/text`

      * 以下值指定所有基礎元件：

         `foundation/components/*`
   * 對不在此清單中的元件發出撤消或重做時，將顯示一條消息，指明該命令可能不可靠。

   * **預設**:屬性會填入AEM提供的許多元件。
   * **類型**:  `String[]`


* **元件錯誤**
( 
`cq.wcm.undo.blacklist`)

   * **說明**:您不想受撤消命令影響的元件和/或元件操作的清單。使用undo命令添加行為不正確的元件和元件操作：

      * 當您不希望元件在撤消歷史記錄（例如`collab/forum/components/post`）中執行任何操作時，添加元件路徑
      * 當您想要從還原歷史記錄中忽略該特定操作（其他操作正確運作）時，請附加冒號(:)和操作至路徑，例如`collab/forum/components/post:insertParagraph.`

   >[!NOTE]
   >
   >當此清單上有操作時，該操作仍被添加到撤消歷史記錄中。 用戶無法撤消還原歷史記錄中早於&#x200B;**壞元件**&#x200B;操作的操作。

   * 典型操作名如下：

      * `insertParagraph`:元件會新增至頁面。
      * `removeParagraph`:元件即會刪除。
      * `moveParagraph`:該段被移到其他位置。
      * `updateParagraph`:段落屬性被更改。
   * **預設**:屬性中會填入數個元件操作。
   * **類型**:  `String[]`
