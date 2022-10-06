---
title: 資料存放庫廢棄項目收集
seo-title: Data Store Garbage Collection
description: 了解如何配置資料儲存垃圾回收以釋放磁碟空間。
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

當移除常規WCM資產時，可從節點階層移除對基礎資料儲存記錄的參考，但資料儲存記錄本身仍會保留。 這個未參考的資料存放區記錄會變成「無法保留」。 在存在大量垃圾資產的情況下，將其清除是有益的，以便保留空間並優化備份和檔案系統維護效能。

WCM應用程式大多傾向於收集資訊，但刪除資訊的頻率卻差不多。 雖然新增了新影像，甚至取代了舊版本，但版本控制系統仍保留舊影像，並支援視需要還原。 因此，我們認為添加到系統中的大多數內容都被有效地永久儲存。 那麼，儲存庫中「垃圾」的典型來源是什麼？

AEM會將存放庫用作許多內部和內部管理活動的儲存：

* 已建立和下載的包
* 為發佈複製建立的臨時檔案
* 工作流程裝載
* 在DAM呈現期間暫時建立的資產

當這些臨時對象中的任何一個足夠大，需要在資料儲存中儲存時，以及當該對象最終被淘汰時，資料儲存記錄本身將保持為「垃圾」。 在典型的WCM製作/發佈應用程式中，此類型最大的垃圾來源通常是發佈啟動程式。 將資料複製到Publish時，如果首先以名為「Durbo」的有效資料格式收集集合，並儲存在下方的儲存庫中 `/var/replication/data`. 資料包通常大於資料儲存的臨界大小閾值，因此最終儲存為資料儲存記錄。 複製完成時， `/var/replication/data` 已刪除，但資料儲存記錄仍為「垃圾」。

可恢復垃圾的另一個來源是包。 與其他所有內容一樣，包資料儲存在儲存庫中，因此儲存在資料儲存中的包大於4KB。 在開發項目過程中或一段時間內，在維護系統的同時，可以多次構建和重建包，每個構建都產生新的資料儲存記錄，同構前一個構建的記錄。

## 資料儲存垃圾收集如何運作？ {#how-does-data-store-garbage-collection-work}

如果儲存庫已配置外部資料儲存， [資料儲存垃圾收集會自動執行](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 作為每週維護窗口的一部分。 系統管理員也可以 [手動執行資料儲存垃圾收集](#running-data-store-garbage-collection) 視需要。 通常，建議定期執行資料儲存垃圾收集，但在規劃資料儲存垃圾收集時應考慮以下因素：

* 資料儲存垃圾收集需要時間，可能會影響效能，因此應據此進行規劃。
* 刪除資料儲存垃圾記錄不會影響正常效能，因此這不是效能最佳化。
* 如果儲存利用率和備份時間等相關因素不是問題，則資料儲存垃圾收集可能會安全地延遲。

資料儲存垃圾收集器首先在進程開始時記錄當前時間戳。 然後，使用多通標籤/掃描模式算法進行收集。

在第一階段，資料儲存垃圾收集器執行所有儲存庫內容的全面遍歷。 對於引用資料儲存記錄的每個內容對象，它將檔案置於檔案系統中，執行元資料更新 — 修改「上次修改的」或MTIME屬性。 此時，此階段存取的檔案會比初始基線時間戳記更新。

在第二階段，資料儲存垃圾收集器以與「查找」大致相同的方式遍歷資料儲存的物理目錄結構。 它檢查了檔案的「上次修改」或MTIME屬性，並作出以下決定：

* 如果MTIME比初始基線時間戳更新，則在第一階段找到檔案，或是在收集程式進行期間新增至存放庫的全新檔案。 其中任何一種情況都認為記錄有效，不得刪除檔案。
* 如果MTIME早於初始基線時間戳，則檔案不是活動引用的檔案，它被視為可移除垃圾。

此方法適用於具有私人資料存放區的單一節點。 但是，資料儲存可能會被共用，如果是這表示系統不會檢查來自其他存放庫的資料儲存記錄的潛在活動即時參考，且可能會錯誤移除作用中的參考檔案。 在規劃任何垃圾收集之前，系統管理員必須了解資料儲存的共用性質，並且只有在知道資料儲存不是共用的情況下，才使用簡單的內置資料儲存垃圾收集過程。

>[!NOTE]
>
>在叢集或共用資料存放區設定（含Mongo或Segment Tar）中執行垃圾收集時，記錄檔可能會顯示無法刪除某些Blob ID的警告。 這是因為以前垃圾收集中刪除的blob ID被沒有ID刪除資訊的其他群集或共用節點重新錯誤引用。 因此，執行垃圾收集時，會在嘗試刪除上次執行中已刪除的ID時記錄警告。 此行為不會影響效能或功能。

## 運行資料儲存垃圾收集 {#running-data-store-garbage-collection}

根據運行AEM的資料儲存設定，運行資料儲存垃圾收集有三種方法：

1. 透過 [修訂清除](/help/sites-deploying/revision-cleanup.md)  — 通常用於節點儲存清理的垃圾收集機制。

1. 透過 [資料儲存垃圾收集](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard)  — 專用於外部資料儲存的垃圾收集機制，可在Operations Dashboard上使用。
1. 透過 [JMX控制台](/help/sites-administering/jmx-console.md).

如果同時將TarMK用作節點儲存和資料儲存，則修訂清除可用於垃圾收集節點儲存和資料儲存。 但是，如果配置了外部資料儲存（如檔案系統資料儲存），則必須將資料儲存垃圾收集與修訂清除分開顯式觸發。 資料儲存垃圾收集可通過Operations Dashboard或JMX控制台觸發。

下表顯示需要用於AEM 6中所有支援的資料存放區部署的資料存放區垃圾收集類型：

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
   <td>修訂清除（二進位檔與區段存放區內連結）</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>外部檔案系統</td>
   <td><p>通過Operations Dashboard執行資料儲存垃圾收集任務</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>通過Operations Dashboard執行資料儲存垃圾收集任務</p> <p>JMX控制台</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>外部檔案系統</td>
   <td><p>通過Operations Dashboard執行資料儲存垃圾收集任務</p> <p>JMX控制台</p> </td>
  </tr>
 </tbody>
</table>

### 透過Operations Dashboard執行資料儲存垃圾收集 {#running-data-store-garbage-collection-via-the-operations-dashboard}

內置的每週維護窗口，可通過 [操作儀表板](/help/sites-administering/operations-dashboard.md)，包含一個內建任務，可在週日凌晨1:00觸發資料儲存垃圾收集。

如果您需要在此時間之外執行資料儲存垃圾收集，則可透過Operations Dashboard手動觸發。

運行資料儲存垃圾收集之前，您應檢查當時是否沒有運行任何備份。

1. 開啟操作儀表板，方法為 **導覽** -> **工具** -> **操作** -> **維護**.
1. 按一下或點選 **每週維護窗口**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. 選取 **資料儲存垃圾收集** 任務，然後按一下或點選 **執行** 表徵圖。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 資料儲存垃圾收集會執行，其狀態會顯示在控制面板中。

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>只有在配置了外部檔案資料儲存時，才會顯示資料儲存垃圾收集任務。 請參閱 [在AEM 6中配置節點儲存區和資料儲存區](/help/sites-deploying/data-store-config.md#file-data-store) 以了解如何設定檔案資料儲存。

### 通過JMX控制台運行資料儲存垃圾收集 {#running-data-store-garbage-collection-via-the-jmx-console}

本節介紹如何通過JMX控制台手動運行資料儲存垃圾回收。 如果您的安裝是在沒有外部資料儲存的情況下設定的，則這不適用於您的安裝。 請改為參閱下方的如何執行修訂清除的指示 [維護儲存庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>如果您使用外部資料存放區執行TarMK，則需要先執行修訂清除，垃圾收集才能有效。

運行垃圾收集：

1. 在Apache Felix OSGi Management Console中，反白顯示 **主要** 索引標籤和選取 **JMX** 的下一頁。
1. 下一步，搜尋並按一下 **存放庫管理員** MBean(或轉至 `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`)。
1. 按一下 **startDataStoreGC(boolean markOnly)**.
1. 輸入&quot;`true`」 `markOnly` 參數（如有需要）:

   | **選項** | **說明** |
   |---|---|
   | boolean markOnly | 設為true，在標籤和掃描操作中僅標籤參照而不掃描。 在多個不同儲存庫之間共用基礎BlobStore時，將使用此模式。 對於所有其他情況，請將其設為false以執行完整的垃圾收集。 |

1. 按一下 **叫用**. CRX會執行垃圾收集，並指出其完成時間。

>[!NOTE]
>
>資料儲存垃圾收集將不會收集過去24小時內已刪除的檔案。

>[!NOTE]
>
>只有配置了外部檔案資料儲存時，資料儲存垃圾收集任務才會啟動。 如果尚未配置外部檔案資料儲存，則任務將返回消息 `Cannot perform operation: no service of type BlobGCMBean found` 叫用之後。 請參閱 [在AEM 6中配置節點儲存區和資料儲存區](/help/sites-deploying/data-store-config.md#file-data-store) 以了解如何設定檔案資料儲存。

## 自動資料儲存垃圾收集 {#automating-data-store-garbage-collection}

如果可能，當系統上的負載很小時（例如上午），應運行資料儲存垃圾收集。

內置的每週維護窗口，可通過 [操作儀表板](/help/sites-administering/operations-dashboard.md)，包含一個內建任務，可在週日凌晨1:00觸發資料儲存垃圾收集。 您還應檢查此時未運行任何備份。 維護視窗的開始可視需要透過控制面板加以自訂。

>[!NOTE]
>
>不同時運行它的原因是，還備份了舊（和未使用的）資料儲存檔案，因此，如果需要回滾到舊修訂版本，則二進位檔案仍在備份中。

如果您不想在Operations Dashboard的「每週維護時段」中執行資料儲存垃圾收集，也可以使用wget或curl HTTP用戶端來自動執行。 以下是如何使用curl自動備份的範例：

>[!CAUTION]
>
>在以下範例中 `curl` 命令可能需要為您的實例配置各種參數；例如，主機名稱( `localhost`)，埠( `4502`)，管理密碼( `xyz`)和各種參數，用於實際資料儲存垃圾收集。

以下是透過命令列叫用資料存放區垃圾收集的curl命令範例：

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

curl命令會立即傳回。

## 檢查資料儲存一致性 {#checking-data-store-consistency}

資料存放區一致性檢查會報告遺失但仍被參考的資料存放區二進位檔。 要啟動一致性檢查，請執行以下步驟：

1. 轉到JMX控制台。 有關如何使用JMX控制台的資訊，請參見 [這篇文章](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. 搜尋 **BlobGarbageCollection** Mbean，然後按一下。
1. 按一下 `checkConsistency()` 連結。

一致性檢查完成後，訊息會顯示報告為遺失的二進位檔數。 如果數字大於0，請檢查 `error.log` 有關缺少二進位檔的詳細資訊。

以下範例說明記錄檔中如何報告遺失的二進位檔：

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
