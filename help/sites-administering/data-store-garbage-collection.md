---
title: 資料存放庫廢棄項目收集
seo-title: Data Store Garbage Collection
description: 瞭解如何配置資料儲存垃圾回收以釋放磁碟空間。
seo-description: Learn how to configure Data Store Garbage Collection to free up disk space.
uuid: 49488a81-986a-4d1a-96c8-aeb6595fc094
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5b1e46c5-7e56-433e-b62e-2a76ea7be0fd
docset: aem65
exl-id: 0dc4a8ce-5b0e-4bc9-a6f5-df2a67149e22
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 0%

---

# 資料存放庫廢棄項目收集 {#data-store-garbage-collection}

當移除常規WCM資產時，對基礎資料儲存記錄的引用可以從節點層次中移除，但資料儲存記錄本身仍然保持。 此未引用的資料儲存記錄隨後變為「垃圾」，無需保留。 在存在大量垃圾資產的情況下，有利於清除這些垃圾資產以保留空間，優化備份和檔案系統維護效能。

在大多數情況下，WCM應用程式往往收集資訊，但刪除資訊的頻率幾乎不是那麼高。 雖然新映像被添加，甚至會取代舊版本，但版本控制系統仍保留舊映像，並支援在需要時恢復到舊映像。 因此，我們認為添加到系統中的大部分內容被有效地永久儲存。 那麼，我們可能想要清理的儲存庫中「垃圾」的典型來源是什麼？

AEM將儲存庫用作儲存，用於許多內部和內部管理活動：

* 生成和下載的包
* 為發佈複製建立的臨時檔案
* 工作流負載
* 在DAM呈現期間臨時建立的資產

當這些臨時對象中的任何一個足夠大，需要在資料儲存中儲存，並且當對象最終被棄用時，資料儲存記錄本身將保持為「垃圾」。 在典型的WCM作者/發佈應用程式中，此類垃圾的最大來源通常是發佈激活過程。 將資料複製到「發佈」時，如果首先以名為「Durbo」的高效資料格式以集合形式收集並儲存在儲存庫中， `/var/replication/data`。 資料束通常大於資料儲存的臨界大小閾值，因此最後儲存為資料儲存記錄。 複製完成後， `/var/replication/data` 刪除，但資料儲存記錄仍為「垃圾」。

另一個可恢復垃圾來源是包。 與其他所有內容一樣，包資料儲存在儲存庫中，因此儲存在資料儲存中的包大於4KB。 在開發項目過程中或在維護系統的過程中，可以多次構建和重建包，每次構建都會生成新的資料儲存記錄，同時保留以前構建的記錄。

## 資料儲存垃圾收集是如何工作的？ {#how-does-data-store-garbage-collection-work}

如果儲存庫已配置有外部資料儲存， [資料儲存垃圾收集將自動運行](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 作為「每週維護」窗口的一部分。 系統管理員也 [手動運行資料儲存垃圾回收](#running-data-store-garbage-collection) 根據需要。 通常，建議定期執行資料儲存垃圾收集，但在規劃資料儲存垃圾收集時應考慮以下因素：

* 資料儲存垃圾收集需要時間，並可能影響效能，因此應相應地進行規劃。
* 刪除資料儲存垃圾記錄不會影響正常效能，因此這不是效能優化。
* 如果不考慮儲存利用率和備份時間等相關因素，則資料儲存垃圾收集可能會被安全地延遲。

當進程開始時，資料儲存垃圾收集器首先記錄當前時間戳。 然後，使用多遍標籤/掃描模式算法執行該收集。

在第一階段，資料儲存垃圾收集器執行對所有儲存庫內容的全面遍歷。 對於引用資料儲存記錄的每個內容對象，它都將檔案定位在檔案系統中，執行元資料更新 — 修改「上次修改」或MTIME屬性。 此時，此階段訪問的檔案將比初始基線時間戳更新。

在第二階段，資料儲存垃圾收集器以與「查找」大致相同的方式遍歷資料儲存的物理目錄結構。 它檢查了檔案的「上次修改時間」或MTIME屬性，並作出以下確定：

* 如果MTIME比初始基線時間戳新，則在第一階段找到該檔案，或者是收集過程進行期間添加到儲存庫的全新檔案。 在其中一種情況下，記錄被視為活動，檔案不得刪除。
* 如果MTIME早於初始基線時間戳，則檔案不是活動引用的檔案，它被視為可移除垃圾。

該方法適用於具有專用資料儲存的單個節點。 但是，資料儲存可能是共用的，如果是，則表示不會檢查其他儲存庫對資料儲存記錄的潛在活動即時引用，並且可能會錯誤地刪除活動引用的檔案。 在規劃任何垃圾收集之前，系統管理員必須瞭解資料儲存的共用性質，並且只有在知道資料儲存未共用時才使用簡單的內置資料儲存垃圾收集過程。

>[!NOTE]
>
>在群集或共用資料儲存設定（使用Mongo或Segment Tar）中執行垃圾收集時，日誌可能會顯示無法刪除某些Blob ID的警告。 這是因為先前垃圾收集中刪除的Blob ID被沒有ID刪除資訊的其他群集或共用節點錯誤地再次引用。 因此，當執行垃圾收集時，它會在嘗試刪除上次運行中已刪除的ID時記錄警告。 此行為不影響效能或功能。

## 運行資料儲存垃圾收集 {#running-data-store-garbage-collection}

根據正在運行的資料儲存設定，有三種運行資料儲存垃圾收集AEM的方法：

1. 通過 [修訂版清除](/help/sites-deploying/revision-cleanup.md)  — 通常用於節點儲存清理的垃圾回收機制。

1. 通過 [資料儲存垃圾收集](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard)  — 特定於外部資料儲存的垃圾回收機制，可在「操作控制板」中使用。
1. 通過 [JMX控制台](/help/sites-administering/jmx-console.md)。

如果TarMK同時用作節點儲存和資料儲存，則版本清理可用於節點儲存和資料儲存的垃圾收集。 但是，如果將外部資料儲存配置為（如檔案系統資料儲存），則必須將資料儲存垃圾收集與修訂版清除分開顯式觸發。 資料儲存垃圾收集可以通過操作儀表板或JMX控制台觸發。

下表顯示了資料儲存垃圾收集類型，該類型需要用於6中所有受支援的資料儲存部署AEM:

<table>
 <tbody>
  <tr>
   <td><strong>節點存放區</strong><br /> </td>
   <td><strong>資料儲存</strong></td>
   <td><strong>垃圾收集機制</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>TarMK</td>
   <td>修訂版清除（二進位檔案與段儲存內聯）</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>外部檔案系統</td>
   <td><p>通過操作面板執行資料儲存垃圾收集任務</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>蒙戈DB</td>
   <td>蒙戈DB</td>
   <td><p>通過操作面板執行資料儲存垃圾收集任務</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>蒙戈DB</td>
   <td>外部檔案系統</td>
   <td><p>通過操作面板執行資料儲存垃圾收集任務</p> <p>JMX控制台</p> </td>
  </tr>
 </tbody>
</table>

### 通過操作儀表板運行資料儲存垃圾收集 {#running-data-store-garbage-collection-via-the-operations-dashboard}

內置的每週維護窗口，可通過 [操作儀表板](/help/sites-administering/operations-dashboard.md)，包含一個內置任務，以在星期日的上午1點觸發資料儲存垃圾收集。

如果您需要在此時間之外運行資料儲存垃圾收集，則可以通過操作儀表板手動觸發。

在運行資料儲存垃圾收集之前，您應檢查當時是否沒有運行任何備份。

1. 開啟操作儀表板 **導航** -> **工具** -> **操作** -> **維護**。
1. 按一下或點擊 **每週維護窗口**。

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 選擇 **資料儲存垃圾收集** 任務，然後按一下或點擊 **運行** 表徵圖

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 資料儲存垃圾收集運行，其狀態顯示在儀表板中。

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>只有在配置了外部檔案資料儲存時，才可看到「資料儲存垃圾收集」任務。 請參閱 [在6中配置節點儲存和數AEM據儲存](/help/sites-deploying/data-store-config.md#file-data-store) 的子菜單。

### 通過JMX控制台運行資料儲存垃圾收集 {#running-data-store-garbage-collection-via-the-jmx-console}

本節介紹通過JMX控制台手動運行資料儲存垃圾收集。 如果安裝時沒有外部資料儲存，則這不適用於安裝。 請參閱下面有關如何運行修訂版清除的說明 [維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。

>[!NOTE]
>
>如果您正在使用外部資料儲存運行TarMK，則必須先運行修訂版清理，以便垃圾收集有效。

要運行垃圾收集，請執行以下操作：

1. 在Apache Felix OSGi管理控制台中，選中 **主** 頁籤 **JMX** 的子菜單。
1. 接下來，搜索並按一下 **儲存庫管理器** MBean(或轉到 `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`)。
1. 按一下 **startDataStoreGC（布爾markOnly）**。
1. 輸入&quot;`true`的 `markOnly` 參數（如果需要）:

   | **選項** | **說明** |
   |---|---|
   | 布爾標籤僅 | 設定為true時，僅標籤參照，在標籤和掃描操作中不掃描。 當基礎BlobStore在多個不同的儲存庫之間共用時，將使用此模式。 對於所有其它情況，將其設定為false以執行完全垃圾收集。 |

1. 按一下 **調用**。 CRX運行垃圾收集，並指示它何時完成。

>[!NOTE]
>
>資料儲存垃圾收集不會收集過去24小時內已刪除的檔案。

>[!NOTE]
>
>只有配置了外部檔案資料儲存時，資料儲存垃圾收集任務才會啟動。 如果尚未配置外部檔案資料儲存，則任務將返回消息 `Cannot perform operation: no service of type BlobGCMBean found` 調用後。 請參閱 [在6中配置節點儲存和數AEM據儲存](/help/sites-deploying/data-store-config.md#file-data-store) 的子菜單。

## 自動化資料儲存垃圾收集 {#automating-data-store-garbage-collection}

如果可能，應在系統負載較小時運行資料儲存垃圾收集。

內置的每週維護窗口，可通過 [操作儀表板](/help/sites-administering/operations-dashboard.md)，包含一個內置任務，以在星期日的上午1點觸發資料儲存垃圾收集。 您還應檢查此時是否未運行任何備份。 維護窗口的啟動可以根據需要通過儀表板進行自定義。

>[!NOTE]
>
>不同時運行它的原因是，舊（和未使用的）資料儲存檔案也會備份，因此，如果需要回滾到舊修訂，二進位檔案仍在備份中。

如果您不想在操作控制板的每週維護窗口中運行資料儲存垃圾收集，也可以使用wget或curl HTTP客戶端自動執行。 以下是如何使用curl自動備份的示例：

>[!CAUTION]
>
>在以下示例中 `curl` 命令可能需要為實例配置各種參數；例如，主機名( `localhost`)，埠( `4502`)，管理密碼( `xyz`)和實際資料儲存垃圾收集的各種參數。

下面是通過命令行調用資料儲存垃圾收集的示例curl命令：

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

curl命令立即返回。

## 檢查資料儲存一致性 {#checking-data-store-consistency}

資料儲存一致性檢查將報告任何缺少但仍被引用的資料儲存二進位檔案。 要開始一致性檢查，請執行以下步驟：

1. 轉到JMX控制台。 有關如何使用JMX控制台的資訊，請參見 [這篇文章](/help/sites-administering/jmx-console.md#using-the-jmx-console)。
1. 搜索 **BlobGarbageCollection** Mbean並按一下它。
1. 按一下 `checkConsistency()` 的子菜單。

一致性檢查完成後，將顯示報告為缺少的二進位檔案數。 如果數字大於0，請檢查 `error.log` 的子目錄。

在下面，您將找到一個示例，說明如何在日誌中報告缺少的二進位檔案：

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
