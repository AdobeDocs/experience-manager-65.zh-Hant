---
title: 受監視資料夾的備份策略
seo-title: 受監視資料夾的備份策略
description: 本文檔介紹受監視的資料夾如何受到不同備份和恢複方案的影響、這些方案的限制和結果，以及如何將資料丟失降至最低。
seo-description: 本文檔介紹受監視的資料夾如何受到不同備份和恢複方案的影響、這些方案的限制和結果，以及如何將資料丟失降至最低。
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 受監視資料夾的備份策略 {#backup-strategies-for-watched-folders}

本內容介紹受監視的資料夾如何受到不同備份和恢複方案的影響，這些方案的限制和結果，以及如何將資料丟失降至最低。

*Watched Folder* （監視資料夾）是基於檔案系統的應用程式，它調用已配置的服務操作，以在監視資料夾層次結構中的以下資料夾之一中操作檔案：

* 輸入
* 分段
* 輸出
* 失敗
* 保留

用戶或客戶端應用程式首先將檔案或資料夾放在輸入資料夾中。 然後，服務操作將檔案移入舞台資料夾進行處理。 服務執行指定操作後，會將修改的檔案保存到輸出資料夾中。 成功處理的源檔案將移到保留資料夾，失敗的處理檔案將移到失敗資料夾。 啟用監 `Preserve On Failure` 視資料夾的屬性後，失敗的處理源檔案將移到保留資料夾。 (請參閱 [設定監看的資料夾端點](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)。)

通過備份檔案系統，可以備份受監視的資料夾。

>[!NOTE]
>
>此備份獨立於資料庫或文檔儲存備份和恢復過程。

## 受監視的資料夾如何運作 {#how-watched-folders-work}

此內容說明受監視的資料夾檔案控製程式。 在制定恢復計畫之前，務必瞭解此過程。 在此範例中，已 `Preserve On Failure` 啟用監看資料夾的屬性。 檔案會依檔案送達的順序處理。

下表說明在整個程式中對五個範例檔案(file1、file2、file3、file4、file5)的檔案操作。 在表中，x軸表示時間，如時間1或T1,y軸表示受監視資料夾層次結構（如輸入）中的資料夾。

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
   <td><p>file1, file2, file3, file4</p></td>
   <td><p>file2, file3, file4</p></td>
   <td><p>file3, file4</p></td>
   <td><p>file4</p></td>
   <td><p>空白</p></td>
   <td><p>file5</p></td>
   <td><p>空白</p></td>
  </tr>
  <tr>
   <td><p>分段</p></td>
   <td><p>空白</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>空白</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>輸出</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>失敗</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
  </tr>
  <tr>
   <td><p>保留</p></td>
   <td><p>空白</p></td>
   <td><p>空白</p></td>
   <td><p>file1 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2, file4 </p></td>
   <td><p>file1, file2, file4 </p></td>
  </tr>
 </tbody>
</table>

以下文字說明每次的檔案操作：

**** T1:四個範例檔案會放在輸入檔案夾中。

**** T2:服務操作將file1移入舞台資料夾以進行操作。

**** T3:服務操作將file2移入舞台資料夾以進行操作。 它將file1的結果放在輸出資料夾中，並將file1移動到preserve資料夾。

**** T4:服務操作將file3放置在舞台資料夾中進行操作。 它將file2的結果放在輸出資料夾中，並將file2放在preserve資料夾中。

**** T5:服務操作將file4放置在舞台資料夾中進行操作。 對file3的操作失敗，服務操作將其放在failure資料夾中。

**** T6:服務操作將檔案5放在輸入資料夾中。 它將file4的結果放在輸出資料夾中，將file4放在preserve資料夾中。

**** T7:服務操作將檔案5放置在舞台資料夾中進行操作。

## 備份受監視的資料夾 {#backing-up-watched-folders}

建議您將整個受監視資料夾檔案系統備份到另一個檔案系統。

## 恢復受監視的資料夾 {#restoring-watched-folders}

本節介紹如何恢復受監視的資料夾。 受監視的資料夾通常會叫用在一分鐘內完成的短暫程式。 在這種情況下，使用每小時完成的備份恢復受監視的資料夾不會防止資料丟失。

例如，如果在T1備份時，伺服器在T7出現故障，則file1、file2、file3和file4已被操縱。 使用T1備份還原受監視的資料夾無法防止資料丟失。

如果執行了更新的備份，則可以恢復檔案。 恢復檔案時，請考慮當前檔案所在的監視資料夾層次資料夾：

**** 階段：此資料夾中的檔案在被監視的資料夾恢復後再次處理。

**** 輸入：此資料夾中的檔案在被監視的資料夾恢復後再次處理。

**** 結果：不處理此資料夾中的檔案。

**** 輸出：不處理此資料夾中的檔案。

**** 保留：不處理此資料夾中的檔案。

## 將資料丟失降至最低的策略 {#strategies-to-minimize-data-loss}

下列策略可在還原受監視的資料夾時，將輸出和輸入資料夾資料遺失降至最低：

* 頻繁備份輸出和故障資料夾（如每小時），以避免丟失結果和故障檔案。
* 備份監視資料夾以外的資料夾中的輸入檔案。 這樣可確保檔案在恢復後可用，以防在輸出或故障資料夾中找不到檔案。 確保檔案命名方案一致。

   例如，如果要以副檔名保存輸 `%F.`*出&#x200B;*，則輸出檔案的名稱將與輸入檔案相同。 這可協助您判斷哪些輸入檔案受到操控，哪些輸入檔案必須重新送出。 如果您在結果資料夾中只看到file1_out檔案，而沒有看到file2_out、file3_out和file4_out，則必須重新提交file2、file3和file4。

* 如果可用的監視資料夾備份比處理作業所花費的時間早，則應允許系統建立新的監視資料夾並自動將檔案放入輸入資料夾。
* 如果最新可用備份的時間不夠短，則備份時間小於處理檔案所花的時間，並且已恢復受監視的資料夾，則會在以下不同階段之一處理檔案：

   * **** 階段1:在輸入資料夾中
   * **** 階段2:複製到舞台資料夾，但尚未調用進程
   * **** 階段3:複製到舞台資料夾並調用進程
   * **** 階段4:正在進行的操作
   * **** 階段5:傳回結果
   如果檔案處於階段1中，則它們將被操縱。 如果檔案位於階段2或3中，請將檔案置於輸入檔案夾中，以便再次進行操作。

   **注意**:如果對檔案進行多次操作，則會防止資料丟失，但結果可能會重複。*

## 結論 {#conclusion}

由於受監視資料夾的動態性和不斷變化的性質，因此應使用在一天內備份的檔案恢復受監視資料夾。 最佳做法是備份結果、將輸入資料夾儲存在伺服器上，並跟蹤輸入檔案，以便在出現故障時重新提交作業。
