---
title: 設定頁面編輯的復原
description: 瞭解如何在AEM中設定頁面編輯的還原支援。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 1%

---

# 設定頁面編輯的復原{#configuring-undo-for-page-editing}

[OSGi服務](/help/sites-deploying/configuring-osgi.md) **Day CQ WCM還原設定** ( `com.day.cq.wcm.undo.UndoConfigService`)會公開數個屬性，這些屬性可控制編輯頁面的還原和重做命令的行為。

## 預設設定 {#default-configuration}

在標準安裝中，預設設定被定義為`sling:OsgiConfig`節點上的屬性：

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

此節點包含`cq.wcm.undo.whitelist`和`cq.wcm.undo.blacklist`屬性，其他屬性會採用預設值。

>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何專案。
>
>這是因為下次升級執行個體時，`/libs`的內容會被覆寫（當您套用Hotfix或Feature Pack時，這些內容很可能會被覆寫）。

## 設定還原與重做 {#configuring-undo-and-redo}

您可以為自己的執行個體設定這些OSGi服務屬性。

>[!NOTE]
>
>使用AEM時，有數種方法可管理此類服務的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得詳細資訊和建議的作法。

以下列出Web主控台中顯示的屬性，後面接著相對應的OSGi引數名稱，以及說明和預設值（如果適用）：

* **啟用**
( `cq.wcm.undo.enabled`)

   * **說明**：決定頁面作者是否可以復原和重做變更。
   * **預設**： `Selected`
   * **類型**：`Boolean`

* **路徑**
( `cq.wcm.undo.path`)

   * **描述**：儲存二進位還原資料的存放庫路徑。 當作者變更二進位資料（例如影像）時，原始版本的資料會保留在這裡。 還原對二進位資料的變更時，此二進位還原資料會還原至頁面。
   * **預設**： `/var/undo`
   * **類型**：`String`

  >[!NOTE]
  >
  >依預設，只有系統管理員可以存取`/var/undo`節點。 作者只有獲得存取二進位還原資料的許可權後，才能對二進位內容執行還原和重做操作。

* **分鐘 有效性**
( `cq.wcm.undo.validity`)

   * **描述**：儲存二進位還原資料的最短時間（小時）。 在此時段後，二進位資料即可刪除，以節省磁碟空間。
   * **預設**： `10`
   * **類型**：`Integer`

* **步驟**
( `cq.wcm.undo.steps`)

   * **描述**：還原歷程記錄中儲存的頁面動作數目上限。
   * **預設**： `20`
   * **類型**：`Integer`

* **持續性**
( `cq.wcm.undo.persistence`)

   * **描述**：持續復原歷程記錄的類別。 提供兩種持續性類別：

      * `CQ.undo.persistence.WindowNamePersistence`：使用window.name屬性儲存歷程記錄。
      * `CQ.undo.persistence.CookiePersistance`：使用Cookie保留歷史記錄。

   * **預設**： `CQ.undo.persistence.WindowNamePersistence`
   * **類型**：`String`

* **持續性模式**
( `cq.wcm.undo.persistence.mode`)

   * **描述**：決定何時保留復原歷程記錄。 選取此選項可在每次編輯頁面後保留復原歷史記錄。 清除此選項後，只有在發生頁面重新載入時（例如，使用者導覽至其他頁面）才會持續存在。

     保留復原歷史記錄會使用網頁瀏覽器資源。 如果您的使用者瀏覽器對頁面編輯的反應很慢，請嘗試在頁面重新載入時保留復原歷史記錄。

   * **預設**： `Selected`
   * **類型**：`Boolean`

* **標籤模式**
( `cq.wcm.undo.markermode`)

   * **說明**：指定在復原或重做發生時，要用來指示哪些段落受到影響的視覺提示。 下列值有效：

      * flash：段落的選取指示器會暫時閃爍。
      * select：段落被選取。

   * **預設**： `flash`
   * **類型**：`String`

* **好元件**
( `cq.wcm.undo.whitelist`)

   * **說明**：您想要受復原和重做命令影響的元件清單。 當元件路徑可透過還原/重做正常運作時，將其新增至此清單。 附加星號(&amp;amp；ast；)以指定一組元件：

      * 下列值會指定基礎文字元件：

        `foundation/components/text`

      * 下列值會指定所有基礎元件：

        `foundation/components/*`

   * 當對不在此清單中的元件發出復原或重做命令時，會出現一則訊息，指出該命令可能不可靠。

   * **預設**：屬性已填入AEM提供的許多元件。
   * **類型**：`String[]`

* **錯誤的元件**
( `cq.wcm.undo.blacklist`)

   * **描述**：您不想受復原命令影響的元件和/或元件作業清單。 使用復原命令新增無法正常運作的元件和元件操作：

      * 當您想要復原歷程記錄中沒有元件的任何作業（例如，`collab/forum/components/post`）時，請新增元件路徑
      * 如果您想要從復原歷程記錄中省略特定作業（其他作業運作正常），請附加冒號(：)和作業至路徑，例如`collab/forum/components/post:insertParagraph.`

  >[!NOTE]
  >
  >當操作在此清單上時，它仍會新增到復原歷史記錄中。 使用者無法復原復原歷程記錄中&#x200B;**錯誤元件**&#x200B;作業之前的作業。

   * 典型的操作名稱如下：

      * `insertParagraph`：元件已新增至頁面。
      * `removeParagraph`：已刪除元件。
      * `moveParagraph`：段落已移至其他位置。
      * `updateParagraph`：段落屬性已變更。

   * **預設**：屬性已填入數個元件作業。
   * **類型**：`String[]`
