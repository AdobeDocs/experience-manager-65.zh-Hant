---
title: 受監視資料夾的備份策略
seo-title: Backup strategies for watched folders
description: 本文檔介紹受不同備份和恢複方案影響的監視資料夾、這些方案的限制和結果，以及如何將資料丟失降至最低。
seo-description: This document describes how watched folders are affected by different backup and recovery scenarios, the limitations and outcomes of these scenarios, and how to minimize data loss.
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
exl-id: 0d36160a-29fa-4cc4-a0ff-fc681d3e040e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 2%

---

# 受監視資料夾的備份策略 {#backup-strategies-for-watched-folders}

本內容介紹了受不同備份和恢複方案影響的觀看資料夾、這些方案的限制和結果，以及如何將資料丟失降至最低。

*監看資料夾* 是基於檔案系統的應用程式，它調用已配置的服務操作，這些操作操作在監視的資料夾層次結構中的以下資料夾之一內操作檔案：

* 輸入
* 分段
* 輸出
* 失敗
* 保留

用戶或客戶端應用程式首先將檔案或資料夾放在輸入資料夾中。 然後，服務操作將檔案移入階段資料夾以進行處理。 服務執行指定操作後，會將修改的檔案保存到輸出資料夾中。 已成功處理的源檔案將移到保留資料夾，失敗的處理檔案將移到失敗資料夾。 當 `Preserve On Failure` 已啟用「監看」資料夾的屬性，失敗的已處理源檔案將移到「保留」資料夾。 (請參閱 [配置觀看的資料夾端點](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).)

通過備份檔案系統，可以備份已監視的資料夾。

>[!NOTE]
>
>此備份獨立於資料庫或文檔儲存備份和恢復過程。

## 監看資料夾的運作方式 {#how-watched-folders-work}

此內容說明已觀看的資料夾檔案操作程式。 在制定恢復計畫之前，必須了解此過程。 在此範例中， `Preserve On Failure` 屬性。 檔案會依檔案到達的順序進行處理。

下表描述了整個過程中五個示例檔案(file1、file2、file3、file4、file5)的檔案操作。 在表格中，x軸表示時間，如時間1或T1，而y軸表示監視資料夾層次結構內的資料夾，如輸入。

<table>
 <thead>
  <tr>
   <th><p>資料夾</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>輸入</p></td>
   <td><p>檔案1，檔案2，檔案3，檔案4</p></td>
   <td><p>檔案2，檔案3，檔案4</p></td>
   <td><p>檔案3，檔案4</p></td>
   <td><p>檔案4</p></td>
   <td><p>空白</p></td>
   <td><p>檔案5</p></td>
   <td><p>空白</p></td>
  </tr>
  <tr>
   <td><p>分段</p></td>
   <td><p>空白</p></td>
   <td><p>檔案1</p></td>
   <td><p>檔案2</p></td>
   <td><p>檔案3</p></td>
   <td><p>檔案4</p></td>
   <td><p>空白</p></td>
   <td><p>檔案5</p></td>
  </tr>
  <tr>
   <td><p>輸出</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out,file2_out</p></td>
   <td><p>file1_out,file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>失敗</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>file3_fail,file3 </p></td>
   <td><p>file3_fail,file3 </p></td>
   <td><p>file3_fail,file3 </p></td>
  </tr>
  <tr>
   <td><p>保留</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>檔案1 </p></td>
   <td><p>檔案1，檔案2 </p></td>
   <td><p>檔案1，檔案2 </p></td>
   <td><p>檔案1，檔案2，檔案4 </p></td>
   <td><p>檔案1，檔案2，檔案4 </p></td>
  </tr>
 </tbody>
</table>

以下文字說明每次的檔案操作：

**T1:** 四個範例檔案會放置在輸入資料夾中。

**T2:** 服務操作將檔案1移入舞台資料夾以進行操作。

**T3:** 服務操作將檔案2移入舞台資料夾以進行操作。 它將file1的結果放在輸出資料夾中，並將file1移動到preserve資料夾。

**T4:** 服務操作將檔案3放在舞台資料夾中以進行操作。 它會將file2的結果放在輸出資料夾中，並將file2放在保留資料夾中。

**T5:** 服務操作將檔案4放在舞台資料夾中進行操作。 檔案3的操作失敗，服務操作將其置於失敗資料夾中。

**T6:** 服務操作將檔案5放置在輸入資料夾中。 它會將file4的結果放在輸出資料夾中，將file4放在保留資料夾中。

**T7:** 服務操作將檔案5放在舞台資料夾中以進行操作。

## 備份監視的資料夾 {#backing-up-watched-folders}

建議您將整個監視的資料夾檔案系統備份到另一個檔案系統。

## 還原已監視的資料夾 {#restoring-watched-folders}

本節介紹如何還原受監視的資料夾。 受監視的資料夾通常會叫用一分鐘內完成的短期程式。 在這種情況下，使用每小時完成的備份來還原受監視的資料夾不會防止資料丟失。

例如，如果在T1執行備份，而伺服器在T7執行失敗，則檔案1、檔案2、檔案3和檔案4已被操作。 使用T1進行的備份還原受監視的資料夾無法防止資料丟失。

如果執行了更新的備份，則可以恢復檔案。 還原檔案時，請考慮當前檔案所在的監視資料夾層次結構資料夾：

**階段：** 恢復監視的資料夾後，將再次處理此資料夾中的檔案。

**輸入：** 恢復監視的資料夾後，將再次處理此資料夾中的檔案。

**結果：** 不會處理此資料夾中的檔案。

**輸出：** 不會處理此資料夾中的檔案。

**保留：** 不會處理此資料夾中的檔案。

## 將資料丟失降至最低的策略 {#strategies-to-minimize-data-loss}

下列策略可在還原受監視的資料夾時，將輸出和輸入資料夾資料的遺失降至最低：

* 頻繁備份輸出和故障資料夾（如每小時），以避免丟失結果和故障檔案。
* 備份監視資料夾以外的資料夾中的輸入檔案。 這樣可確保恢復後的檔案可用性，以防在輸出資料夾或失敗資料夾中找不到檔案。 請確定您的檔案命名配置一致。

   例如，如果您要使用 `%F.`*擴充功能*，輸出檔案的名稱將與輸入檔案相同。 這可協助您判斷要處理哪些輸入檔案，以及必須重新提交哪些輸入檔案。 如果在結果資料夾中只看到file1out檔案，而沒有看到file2out、file3out和file4out，則必須重新提交file2、file3和file4。

* 如果可用的觀看資料夾備份時間早於處理作業所花費的時間，則應允許系統建立新的觀看資料夾，並自動將檔案放入輸入資料夾。
* 如果最新的可用備份時間不夠，則備份時間少於處理檔案所花費的時間，並且已恢復監視的資料夾，則會在以下不同階段之一操作檔案：

   * **階段1:** 在輸入資料夾中
   * **第2階段：** 複製到階段資料夾，但尚未調用該進程
   * **第3階段：** 複製到階段資料夾，並調用該進程
   * **第4階段：** 正在操縱
   * **第5階段：** 返回的結果

   如果檔案處於階段1中，則將操作它們。 如果檔案處於階段2或階段3中，請將它們置於輸入資料夾中，以便再次進行操作。

   >[!NOTE]
   >
   >如果檔案操作多次，將防止資料丟失，但結果可能重複。

## 結論 {#conclusion}

由於受監視資料夾的性質是動態的，而且不斷變化，因此應使用一天內備份的檔案來恢復受監視的資料夾。 最佳做法是備份結果、將輸入資料夾儲存在伺服器上，以及跟蹤輸入檔案，以便在出現故障時可以重新提交作業。
