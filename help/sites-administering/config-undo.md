---
title: 設定頁面編輯的還原
seo-title: 設定頁面編輯的還原
description: 瞭解如何在AEM中設定「復原」頁面編輯支援。
seo-description: 瞭解如何在AEM中設定「復原」頁面編輯支援。
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定頁面編輯的還原{#configuring-undo-for-page-editing}

OSGi服務 [](/help/sites-deploying/configuring-osgi.md) Day CQ WCM Undo Configuration **(**`com.day.cq.wcm.undo.UndoConfigService`)會公開數個屬性，這些屬性可控制編輯頁面時的還原和重做指令行為。

## 預設設定 {#default-configuration}

在標準安裝中，預設設定定義為節點上的 `sling:OsgiConfig`屬性：

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

此節點包 `cq.wcm.undo.whitelist` 含和 `cq.wcm.undo.blacklist` 屬性，對於其他屬性，則採用預設值。

>[!CAUTION]
>
>您 ***不得*** 更改路徑中的任 `/libs` 何內容。
>
>這是因為下次升級 `/libs` 實例時會覆寫的內容（套用修補程式或功能套件時可能會覆寫）。

## 配置還原和重做 {#configuring-undo-and-redo}

您可以為自己的實例配置這些OSGi服務屬性。

>[!NOTE]
>
>使用AEM時，有幾種方法可管理此類服務的組態設定；如需詳 [細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

以下列出Web控制台中顯示的屬性，後跟相應OSGi參數的名稱，以及說明和預設值（如果適用）:

* **Enable**( `cq.wcm.undo.enabled`)

   * **說明**:決定頁面作者是否可以還原和重做變更。
   * **預設值**: `Selected`
   * **類型**: `Boolean`

* **路徑**( `cq.wcm.undo.path`)

   * **說明**:保存二進位還原資料的儲存庫路徑。 當作者變更二進位資料（例如影像）時，資料的原始版本會保留在此處。 當對二進位資料的變更被復原時，此二進位復原資料會復原至頁面。
   * **預設值**: `/var/undo`
   * **類型**: `String`
   >[!NOTE]
   >
   >預設情況下，只有管理員可以訪問該 `/var/undo` 節點。 只有在作者獲得存取二進位還原資料的權限後，才能對二進位內容執行還原和重做作業。

* **最小值. validity**( `cq.wcm.undo.validity`)

   * **說明**:二進位還原資料儲存的最小時間，以小時為單位。 在此時段後，可刪除二進位資料以節省磁碟空間。
   * **預設值**: `10`
   * **類型**: `Integer`

* **步驟**( `cq.wcm.undo.steps`)

   * **說明**:還原歷史記錄中儲存的最大頁面操作數。
   * **預設值**: `20`
   * **類型**: `Integer`

* **永續性**( `cq.wcm.undo.persistence`)

   * **說明**:持續還原歷史記錄的類別。 提供了兩個持久性類：

      * `CQ.undo.persistence.WindowNamePersistence`:使用window.name屬性持續記錄。
      * `CQ.undo.persistence.CookiePersistance`:使用Cookie持續記錄。
   * **預設值**: `CQ.undo.persistence.WindowNamePersistence`
   * **類型**: `String`


* **永續性模式**( `cq.wcm.undo.persistence.mode`)

   * **說明**:確定何時保存還原歷史記錄。 選取此選項，可在每次編輯頁面後持續還原歷史記錄。 清除此選項，僅在頁面重新載入發生時（例如，使用者導覽至不同頁面）持續存在。

      持續還原歷史記錄使用網頁瀏覽器資源。 如果您使用者的瀏覽器對頁面編輯反應緩慢，請嘗試在頁面重新載入時保留還原歷史記錄。

   * **預設值**: `Selected`
   * **類型**: `Boolean`

* **標籤模式**( `cq.wcm.undo.markermode`)

   * **說明**:指定在還原或重做發生時，用於指示哪些段落受影響的視覺提示。 下列值有效：

      * flash:段落的選擇指標會暫時閃爍。
      * 選擇：選取段落。
   * **預設值**: `flash`
   * **類型**: `String`


* **良好的元件**( `cq.wcm.undo.whitelist`)

   * **說明**:要受撤消和重做命令影響的元件清單。 當元件路徑在還原／重做下正常運作時，將元件路徑新增至此清單。 附加星號(&amp;ast;)以指定一組元件：

      * 以下值指定基礎文本元件：

         `foundation/components/text`

      * 以下值指定所有基礎元件：

         `foundation/components/*`
   * 對不在此清單中的元件發出撤消或重做時，將顯示一條消息，指出該命令可能不可靠。

   * **預設值**:屬性會填入AEM提供的許多元件。
   * **類型**: `String[]`


* **元件錯誤**( `cq.wcm.undo.blacklist`)

   * **說明**:不想受撤消命令影響的元件和／或元件操作的清單。 使用undo命令添加不正確的元件和元件操作：

      * 當您不希望元件在還原歷史記錄中執行任何操作時，添加元件路徑，例如 `collab/forum/components/post`
      * 當您想要從還原歷史記錄中忽略特定操作時，將冒號(:)和操作附加到路徑（例如，其他操作可正確運作） `collab/forum/components/post:insertParagraph.`
   >[!NOTE]
   >
   >在此清單上執行操作時，該操作仍會添加到還原歷史記錄中。 用戶不能撤消在撤消歷史記錄中比「不 **良元件** 」操作早的操作。

   * 典型操作名如下：

      * `insertParagraph`:元件會新增至頁面。
      * `removeParagraph`:將刪除元件。
      * `moveParagraph`:段落會移動到不同的位置。
      * `updateParagraph`:段落屬性會變更。
   * **預設值**:屬性會填入數個元件作業。
   * **類型**: `String[]`




