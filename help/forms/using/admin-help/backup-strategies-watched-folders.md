---
title: 受監視資料夾的備份策略
seo-title: Backup strategies for watched folders
description: 本文檔介紹受監視的資料夾如何受不同備份和恢複方案的影響，這些方案的局限性和結果，以及如何最大限度地減少資料丟失。
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

本內容介紹受監視的資料夾如何受不同備份和恢複方案的影響，這些方案的局限性和結果，以及如何最大限度地減少資料丟失。

*監視資料夾* 是基於檔案系統的應用程式，它調用已配置的服務操作，這些操作在監視資料夾層次結構中的以下資料夾之一內操作檔案：

* 輸入
* 測試
* 輸出
* 失敗
* 保留

用戶或客戶端應用程式首先將檔案或資料夾刪除到輸入資料夾中。 然後，服務操作將檔案移入舞台資料夾進行處理。 服務執行指定操作後，會將修改的檔案保存在輸出資料夾中。 已成功處理的源檔案被移到保留資料夾，失敗的處理檔案被移到失敗資料夾。 當 `Preserve On Failure` 已啟用監視資料夾的屬性，已處理失敗的源檔案將移到保留資料夾。 (請參閱 [正在配置監視的資料夾終結點](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)。)

您可以通過備份檔案系統來備份受監視的資料夾。

>[!NOTE]
>
>此備份獨立於資料庫或文檔儲存備份和恢復過程。

## 監視資料夾的工作方式 {#how-watched-folders-work}

此內容描述受監視的資料夾檔案處理過程。 在制定恢復計畫之前，必須瞭解此過程。 在此示例中， `Preserve On Failure` 已啟用監視資料夾的屬性。 檔案按檔案到達的順序進行處理。

下表描述了在整個過程中對五個示例檔案(file1 、 file2 、 file3 、 file4 、 file5)的檔案操作。 在表中，x軸表示時間，如時間1或T1,y軸表示受監視資料夾層次結構中的資料夾，如輸入。

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
   <td><p>檔案1、檔案2、檔案3、檔案4</p></td>
   <td><p>file2 、 file3和file4</p></td>
   <td><p>檔案3，檔案4</p></td>
   <td><p>file4</p></td>
   <td><p>空</p></td>
   <td><p>file5</p></td>
   <td><p>空</p></td>
  </tr>
  <tr>
   <td><p>測試</p></td>
   <td><p>空</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>空</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>輸出</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>檔案1_輸出</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out 、 file2_out 、 file4_out</p></td>
   <td><p>file1_out 、 file2_out 、 file4_out</p></td>
  </tr>
  <tr>
   <td><p>失敗</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>file3_fail,file3 </p></td>
   <td><p>file3_fail,file3 </p></td>
   <td><p>file3_fail,file3 </p></td>
  </tr>
  <tr>
   <td><p>保留</p></td>
   <td><p>空</p></td>
   <td><p>空</p></td>
   <td><p>file1 </p></td>
   <td><p>檔案1，檔案2 </p></td>
   <td><p>檔案1，檔案2 </p></td>
   <td><p>檔案1、檔案2和檔案4 </p></td>
   <td><p>檔案1、檔案2和檔案4 </p></td>
  </tr>
 </tbody>
</table>

以下文本描述了每次的檔案操作：

**T1:** 四個示例檔案被放在輸入資料夾中。

**T2:** 服務操作將file1移入舞台資料夾進行操作。

**T3:** 服務操作將file2移入舞台資料夾進行操作。 它將file1的結果放在輸出資料夾中，並將file1移到preserve資料夾。

**T4:** 服務操作將file3放在舞台資料夾中進行操作。 它將file2的結果放在輸出資料夾中，並將file2放在preserve資料夾中。

**T5:** 服務操作將file4放在舞台資料夾中進行操作。 檔案3的操作失敗，服務操作將其放在failure資料夾中。

**T6:** 服務操作將檔案5放在輸入資料夾中。 它將file4的結果放在輸出資料夾中，將file4放在preserve資料夾中。

**T7:** 服務操作將檔案5放在舞台資料夾中進行操作。

## 備份受監視的資料夾 {#backing-up-watched-folders}

建議您將整個受監視的資料夾檔案系統備份到另一個檔案系統。

## 還原受監視的資料夾 {#restoring-watched-folders}

本節介紹如何還原受監視的資料夾。 受監視的資料夾通常調用在一分鐘內完成的短時進程。 在這種情況下，使用每小時執行一次的備份恢復受監視的資料夾不會防止資料丟失。

例如，如果在T1時執行備份，而伺服器在T7時出現故障，則檔案1、檔案2、檔案3和檔案4已被操作。 使用T1備份還原受監視的資料夾不會阻止資料丟失。

如果執行了更新的備份，則可以恢復檔案。 恢復檔案時，請考慮當前檔案所在的監視資料夾層次結構資料夾：

**階段：** 在還原受監視的資料夾後，將再次處理此資料夾中的檔案。

**輸入：** 在還原受監視的資料夾後，將再次處理此資料夾中的檔案。

**結果：** 未處理此資料夾中的檔案。

**輸出：** 未處理此資料夾中的檔案。

**保留：** 未處理此資料夾中的檔案。

## 最大限度地減少資料丟失的策略 {#strategies-to-minimize-data-loss}

以下策略可在還原受監視資料夾時最小化輸出和輸入資料夾資料丟失：

* 經常備份輸出和故障資料夾，以避免丟失結果和故障檔案。
* 備份監視資料夾以外的資料夾中的輸入檔案。 這樣可確保在恢復後檔案的可用性，以防在輸出或故障資料夾中找不到檔案。 確保檔案命名方案一致。

   例如，如果要將輸出與 `%F.`*擴展*，輸出檔案將與輸入檔案具有相同的名稱。 這有助於您確定哪些輸入檔案被操作，哪些檔案必須重新提交。 如果在結果資料夾中只看到file1out檔案，而沒有看到file2out、file3out和file4out，則必須重新提交file2、file3和file4。

* 如果可用的受監視資料夾備份時間比處理作業所花的時間要早，則應允許系統建立新受監視資料夾並自動將檔案放入輸入資料夾中。
* 如果最新的可用備份時間不夠，則備份時間小於處理檔案所用的時間，並且已恢復受監視的資料夾，則檔案會在以下不同階段之一處被操縱：

   * **階段1:** 在輸入資料夾中
   * **階段2:** 複製到階段資料夾，但尚未調用該進程
   * **階段3:** 複製到階段資料夾並調用該進程
   * **階段4:** 正在處理
   * **階段5:** 返回的結果

   如果檔案處於階段1中，則會處理它們。 如果檔案處於階段2或階段3中，請將它們置於輸入資料夾中，以便再次進行操作。

   >[!NOTE]
   >
   >如果對檔案進行多次操作，將防止資料丟失，但結果可能會重複。

## 結論 {#conclusion}

由於受監視資料夾的動態和不斷變化的性質，應在一天內備份的檔案上恢復受監視資料夾。 最佳做法是備份結果、將輸入資料夾儲存在伺服器上並跟蹤輸入檔案，以便在失敗時可以重新提交作業。
